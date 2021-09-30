## Gamma
화면의 밝기. 이미지를 제작했을 때 그것을 보여주는 모니터나 스캐너 등이 가진 밝기를 표현하는 곡선.  
감광 재료의 콘트라스트 상태를 나타내는 척도. 농도 변화 및 노광량의 변화를 수치로 나타낸 것.
[Propaeganda, 영화사전, 2004](https://terms.naver.com/entry.naver?docId=348766&cid=42617&categoryId=42617)   


우리가 사용하는 디바이스가 너무나도 다양하고, 디스플레이마다 표현할 수 있는 밝기, 색 영역이 각각 다름. 그런 것에서 오는 차이를 줄이기 위해 이해해야 함.   
Ex. CRT 모니터 감마 값 때문에 이미지 색상 구현 한계 생김.


원래 이미지가 갖고 있는 신호가 2지만 모니터 상에서 이미지가 1로 바뀌어 보인다면 1만큼 어둡게 보이는 것이기 때문에 gamma-correction 과정을 통해 이미지 자체의 값을 3으로 올려 최종적으로 2(원래 이미지가 가진 값)로 보이도록 하는 것.   
이렇게 원본 파일의 감마(중간톤)을 올려서 저장된 것이 sRGB, 이미지 중 대표적인 파일은 JPG    
이와 다르게 원본 파일을 그대로 저장하는 것을 **Linear** 라고 보면 됨. 대표적으로 Raw, HDR, EXR 등  


일반인들에게는 실제 보이는 그대로 모니터에서 보이는 게 중요하므로 Linear인 raw 보다, sRGB인 jpg를 더 많이 사용.    
하지만 그래픽 작업을 할 때는 원본 그대로 저장해야 함. 그래야 색 정보 뿐 아니라 빛 정보까지 담겨 있기 때문에 후반작업 시 보정할 수 있는 폭이 훨씬 넓어짐.   
JPG로 저장할 시 0~1 사이의 색 정보만 저장되며 때문에 이 이하, 이상의 값은 잘라냄. 그러나 Raw 파일은 흰색 위의 정보값(1 이상)까지 저장. 

JPG(sRGB) - gamma 2.2(중간톤이 밝게 저장됨, 하지만 모니터에서는 제대로 보임)    
RAW(Linear) - gamma 1(중간톤을 있는 그대로 저장. 모니터에서 어둡게 보임)

Ex. 마야에서 작업 시    
1. 실제 카메라: 현실의 이미지(gamma 1 - Linear)을 찍고 저장할 때 (gamma 2.2 - **sRGB**) 로 저장하기 때문에 현실과 똑같이 보임  
2. 예전 CG 카메라: Maya의 가상 이미지(gamma 1 - Linear)을 찍고 저장할 때 (gamma 1)로 저장하기 때문에 어둡게 보임    
3. 현재 CG 카메라: Maya의 가상 이미지(gamma 1 - Linear)을 찍고 저장할 때 (gamma 2.2 - **sRGB**) 로 저장하기 때문에 현실과 똑같이 보임  


하지만 작업할 때 jpg 소스를 사용할 때가 문제.   
jpg 소스는 이미 사진을 찍을 때 gamma 2.2가 적용되어 밝아져 있는 상태. 하지만 이를 마야 안(gamma 1)에서 작업 시 맞지 않음.   
때문에 소스 파일에 gamma correct 노드를 달아 0.454를 곱함 (2.2*0.454=1)   

이 과정을 거쳐 sRGB(gamma 2.2)에서 Linear(gamma 1)로 다시 돌려주는 것. 밝아졌던 중간 톤이 원래대로 돌아감.    
텍스쳐 감마를 1로 만든 다음 최종 아웃풋 전까지 gamma 1의 Linear 상태의 **원본으로 작업** 하는 것을 **Linear Workflow** 라고 함.   
[Maya Linear Workflow and Gamma](https://blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=zinblue&logNo=140199808147) 

http://rapapa.net/?p=3406      
https://news.samsungdisplay.com/1869/     

## Linear Workflow  
모든 그래픽 작업이 **선형 색 공간 Linear Color Space** 에서 이루어지는 방식.    
선형 색 공간과 감마 색 공간(Gamma Color Space) 의 차이에 대해 이해해야 함.   
<img src="https://user-images.githubusercontent.com/60923302/118788622-ecc46600-b8ce-11eb-843c-c985eb6be98e.png" width="300" height="300">

감마 색 공간이 선형 색 공간 보다 자연스러워 보임.    
사람의 눈은 어두운 색에 민감하기 때문에 색이 밝아지는 정도를 어두운 색이 밀집해 있는 왼쪽에서 더 민감하게 느끼고, 따라서 감마 색 공간의 그라데이션이 더 자엽스럽다 느껴지지만 실제 수학적으로 정확한 그라데이션은 선형 색 공간.     
선형 색 공간의 그라데이션을 감마 색 공간처럼 눈에 자연스럽게 만드려면 감마값Gamma를 조정해야 함.

jpg와 같은 이미지들은 자체적으로 감마 보정을 해 실제 데이터보다 밝게 저장함.    
이를 디스플레이 이미지는 다시 감마 보정을 하여 어둡게 만들어 우리가 원하던 원본 이미지를 출력하는 것.(감마 보정을 두 번 거침)  


감마 색 공간에서의 이미지들은 _이미 한 번 밝아진_ 이미지.   
선형 색 공간에서의 이미지(감마보정을 한 번 거친)들은 _원래 색상과 밝기로 되돌린_ 이미지. 때문에 선형 색 공간에서 작업을 하는 것이 권장됨. 이를 Linear Workflow 라고 하는 것.
[선형워크플로우란](https://kyoungwhankim.github.io/ko/blog/color_linearworkflow/)


https://forum.reallusion.com/Topic308094.aspx  
https://frauniemand.tistory.com/8  


## ACES - The Academy Color Encoding System   
**영상 표준 색 관리 시스템**   
영화나 TV를 제작하는 과정에서 색상 관리를 위해 정한 업계 표준. 디지털 카메라 및 여러 촬영 방식이 늘어남에 따라 소스마다 색 공간이 다르다는 문제점 발생. 때문에 이를 통일시켜 제작, 포스트 프로덕션에서 문제점을 보완할 수 있도록 제시된 색상 관리 및 이미지 교환 시스템.    
[방송기술저널, ACES 시스템을 활용한 HDR](http://journal.kobeta.com/%EC%B0%B8%EA%B4%80%EA%B8%B0-aces-%EC%8B%9C%EC%8A%A4%ED%85%9C/)


<img src="https://i1.wp.com/schoolofcolor.org/wp-content/uploads/2018/11/Post_HDTV_Workflow_Part_II_03.jpg?resize=768%2C866" width="300" height="400">

**ACES의 장점**   
1. 후반작업에서의 색보정 불확실성 제거 International Standard Transformation 
2. 넓은 색 공간과 색 심도 High Dynamic Rage + Wide Gamut: 16bit, 32bit, 25stop 이상의 규격을 가지고 있어 현존하는 모든 카메라의 다이나믹 레인지와 컬러 영역 커버 가능. 
3. 따라서 풍부한 색감과 계조 유지 가능
4. 화면지향 선형화Scene Referred Linearization 기술을 사용, 후반 작업에서 보다 자유로운 창작환경 제공    
[포스트 HDTV 시대 이후 영상기술 – ACES V1.0](http://schoolofcolor.org/post-hdtv-part-2/)

- Dynamic Range    
디지털 카메라의 이미지 센서는 일정한 밝기 이상의 빛에 노출되면 OETF 반응을 해 전기 에너지를 출력. 만약 입사되는 빛 에너지가 수용 가능한 범위를 넘으면 포화 상태가 되어 출력 전자량은 더 이상 증가하지 않게 된다.     
필름의 로그 노광 범위와 같은 개념. 

**꼭 보기**
[Foundry-Color Management Fundamentals & ACES Workflows in NUKE](https://learn.foundry.com/course/5515/view/color-management-fundamentals-aces-workflows-in-nuke)

https://blog.frame.io/2019/09/09/guide-to-aces/  
https://www.oscars.org/science-technology/sci-tech-projects/aces  

 

## Premultiplication  

![Premultiplication](https://images.schoolofmotion.com/w950/2af90e3d-2aad-41a2-bd03-c890772357d7/01.jpg)   
1. A는 위에 올라갈 물체, B는 배경.    

![Premultiplication](https://images.schoolofmotion.com/w950/1c2d6174-ce81-480b-bcd3-8046ad027d39/02.jpg)   
2. A에는 a라는 알파 채널이 있음.

누크의 node 창에서 "Merge" 노드를 만들고 A와 B를 연결시키면, 두 이미지가 겹쳐짐.    
Merge(over)의 공식은 [A+B(1-a]

![Premultiplication](https://images.schoolofmotion.com/w950/dc65137b-6759-4ec7-b30c-f4c6f171463a/05.jpg)

3. 이미지로 보면 이렇게 됨. 

위 공식에서 (1-a)란, A의 이미지에서 우리가 필요한 부분만을 잘라내는 것.   
알파채널에서 흰색은 1, 검정은 0, 회색은 0.5의 값을 가짐. 흰 색은 눈에 보이는 부분, 검은 색은 보이지 않는 부분이 됨. 

![Premultiplication](https://images.schoolofmotion.com/w950/85f72aa2-c843-4935-8299-1aae2a10eb1e/06.jpg)

4. 결과적으로 (1-a)는 이렇게 되는 것. 

5. 이후, 반전된 알파 채널(우리가 필요한 부분이 사라진 알파 채널)에 B를 곱함.   
앞서 말한 것처럼 알파 채널에서 흰색은 1, 검정은 0의 값을 가지기 때문에 B가 가지고 있는 값에 반전된 알파 채널의 검은 부분(=0)을 곱하게 되면 그 부분은 사라짐. 

![Premultiplication](https://images.schoolofmotion.com/w950/a3e606e5-f43d-4fcd-83b7-36c6e82ec253/11.jpg)    
![Premultiplication](https://images.schoolofmotion.com/w950/3dcedc20-81ec-424d-bd35-43ad973371cf/12.jpg)

6. 이제 A와 B(1-a)를 더하면 되지만, 이대로 더하게 되면 파란색 픽셀이 표시되어야 하는 곳이 하얗게 변함.   
파란색 픽셀에 노란색 픽셀을 추가하면 실제로는 1보다 큰 RGB 값을 갖게 되어 Superwhite가 되는 것.  

![Premultiplication](https://images.schoolofmotion.com/w950/a0349ac3-6fb7-41cf-8d92-1babe34bb67b/14.jpg)

7. 따라서, 이미지 A가 갖고 있던 알파 채널을 곱해서 우리가 필요한 노란색 부분만을 남겨야 함.

![Premultiplication](https://images.schoolofmotion.com/w950/256bd13d-4436-416f-b4c1-31c414cac6ab/15.jpg)

그래야만 우리가 의도했던 것과 같은 결과를 얻을 수 있음.    
7에서 이미지 A에 알파 채널을 곱하는 단계가 Premultiplication(Pre-multiplication/Premult node)
[What is Premultiplication?](https://www.schoolofmotion.com/blog/premultiplication/)

## RGBA
[알파 채널(투명도)의 두 가지 표현 방식](https://nanite.tistory.com/98)
RGBA에는 두 가지 형식이 있음.   
1. straight alpha(unassociated alpha; unmatted RGB+alpha)
2. premultiplied alpha(associated alpha; matted RGB+alpha)

**Straight alpha**   
straight alpha는 "non-premultiplied alpha" 또는 "unassociated alpha"라고도 부르며 흔하게 사용되는 알파 형식.   
이 방식에서의 RGBA는 알파 값만이 투명도를 나타내며 RGB는 각각 투명도에 관계 없이 빨강, 초록, 파랑의 강도만을 표현.    
![Straight alpha](https://t1.daumcdn.net/cfile/tistory/9975123B5C0FD14335)    
따라서 사진에서 볼 수 있다시피 RGB채널에서는 글자가 온전히 불투명하게 보이고, alpha 채널에서만 투명도가 적용됨. 

**Premultiplied alpha**    
premultiplied alpha는 associated alpha라고도 부르며, 이미지의 필터링/혼합에 적합.   
pre-multiplied가 의미하듯, 알파 값을 RGB에 미리 곱해둔 것.   
그렇기 때문에 RGB의 값은 그 자체로 색상 값과 투명도를 반영하고 있으며, 알파 값은 그래픽 처리를 위해 부수적으로 존재하게 됨.   
![Premultiplied alpha](https://t1.daumcdn.net/cfile/tistory/99C8A5495C0FD14314)  

포토샵에서는 작업의 편의성을 위해 non-premultiplied alpha 채널만을 활용하고 있음.   
누크에서는 합성 시에 premult node를 사용해 활용 가능.
