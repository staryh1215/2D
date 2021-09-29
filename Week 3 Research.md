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


## Linear Workflow  
**찾아보기**  
제작할 때 리니어화 시켜서 제작해야 함.    
https://forum.reallusion.com/Topic308094.aspx  
https://blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=zinblue&logNo=140199808147  
https://frauniemand.tistory.com/8  


## ACES  
https://blog.frame.io/2019/09/09/guide-to-aces/  
https://www.oscars.org/science-technology/sci-tech-projects/aces  
https://learn.foundry.com/course/5515/view/color-management-fundamentals-aces-workflows-in-nuke  
https://blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=baekhyebin&logNo=222092359528  
http://journal.kobeta.com/%EC%B0%B8%EA%B4%80%EA%B8%B0-aces-%EC%8B%9C%EC%8A%A4%ED%85%9C/  
http://schoolofcolor.org/post-hdtv-part-2/

## Premultiplication  
Multipl 하기 전. 
https://www.schoolofmotion.com/blog/premultiplication/  
https://nanite.tistory.com/98  

**포토샵에서**   
https://limnu.com/premultiplied-alpha-primer-artists/  
https://forums.cgsociety.org/t/unpremultiplied-alpha-in-photoshop/1053929  
**누크에서**  
Premult / UnPremult  
Merge  
