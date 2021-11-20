## Chroma key
: 색상 차이를 이용해 움직이는 피사체를 다른 화면에 합성하는 화면 합성 기법.
[프로파간다, 영화사전, 2004](https://terms.naver.com/entry.naver?docId=350243&cid=42617&categoryId=42617)     
합성할 피사체를 단색 판을 배경으로 촬영한 후 그 화면에서 배경색을 제거하면 피사체만 남게 되는 원리를 이용한 것.    
이 때 배경이 되는 단색 판을 크로마 백(chroam back)이라고 함. 

주로 사용하는 색 - **Green**    
: 현재는 주로 초록/파란색을 사용하지만 사실 어느 색이든 사용할 수 있음.    
: 주로 초록/파란색을 사용하는 이유 - 사람의 피부색에 이 색의 비중이 적기 때문.      
  서양인들 중에서는 파란 눈을 가진 사람이 많기 때문에 그린 스크린을 많이 사용
[시선뉴스](https://www.sisunnews.co.kr/news/articleView.html?idxno=42927)

하지만 배경 색을 고를 때는 반드시 어떤 대상을 촬영하는지 고려하며 선택해야 함.       
![블루스크린과 그린스크린 비교](https://user-images.githubusercontent.com/90232599/137173602-a35affb3-c224-41cf-84f6-aa4869404d65.jpg)     
[김준수, "매트처리를 통한 영상합성에 있어서 크로마키 분석", 디자인지식저널 34, 2015.6]

**크로마키의 역사**    
[Hollywood's History of Faking It-The Evolution of Greenscreen Compositing](https://www.youtube.com/watch?v=H8aoUXjSfsI&ab_channel=FilmmakerIQ)

**크로마키 촬영**   
크로마키로 촬영할 때는 합성할 대상(사람)의 뒤에 있는 배경에 최대한 그림자가 지지 않고 단색을 유지하도록 조명을 쳐야 함.   
때문에 조명을 여러 개 사용하며 X자로 조명을 치는 편.    


**가상스튜디오**    
: 가상현실을 구현하기 위한 촬영 공간     
가상 스튜디오에서 촬영한 인물의 실사 화면에 컴퓨터 그래픽으로 제작한 영상을 가상의 공간에 위치시켜 3차원 영상을 구현     
스튜디오 설계 시 내부는 Green 혹은 Blue - 배경과 인물의 경계면을 구분해 매트(Matte)처리를 하기 위함 
벽면과 바닥의 경계는 _곡면_ 으로 처리하는데, 이는 조명으로 인한 벽면의 색상 차이를 최소화시키기 위함.      
[김준수, "디지털 영상합성에 있어서 크로마키와 디지털 색보정", 디지털디자인학연구, 2009.7]   


**Keyers**    
Utility    
1. Keyer: 간단하게 배경과 오브젝트를 분리할 때. 
2. HueKeyer: 지정한 색상을 알파로 빼버림.
3. Difference: A와 B 인풋의 차이를 바로 알파로 빼버림. 

(Big) Screen   
1. Keylight: 주로 많이 사용함
2. Ultimatte: 실제 기계 장비에도 들어있는 알고리즘. 방송국에서도 사용 중. 
3. Primatte: 실제 기계 장비에도 들어있는 알고리즘. 방송국에서도 사용 중. 
4. IBKGizmoV3: 인물 헤어와 같은 디테일이 많은 경우 사용. 소프트하게 빠짐. 하지만 크로마 배경이 촬영되지 않은 경우 어려울 가능성. 
5. ChromaKeyer: 색상을 지정해서 키로 빼는 것. 

모두 같은 것들. 하지만 촬영본들이 각각 다르기 때문에 다른 노드를 사용해주는 것. 

**Keyer로 모든 게 깔끔하게 알파로 빠지지 않음. 필요할 때는 Roto로 따로 작업을 해줘야 함.**

+ [Green Screen Plates](https://www.hollywoodcamerawork.com/green-screen-plates.html) 


## [Nuke - Keylight](https://learn.foundry.com/nuke/content/reference_guide/keyer_nodes/keylight.html)

배경에서 파란색/녹색 스필을 제거하려면 Despill Bias를 사용. 

**Input**   
1. bg: 블루/그린스크린을 대체하고 합성될 배경
2. OutM: Outside Mask, Garbage Matte. 배경에서 불필요한 요소들을 삭제하는 데에 사용됨
3. InM: Inside Mask, Holdout Matte. 전경(분리해서 사용할 개체)의 영역
4. Source: 키 작업을 할 전경(분리해서 사용할 개체) 이미지

**Control**
1. alphaBias: 화면의 색이 파란색이나 녹색이 아니고, 그래서 전경의 일부가 투명해지는 경우 사용. 전경 중 영향을 받는 부분의 색상을 선택.
2. despillBias: 전경의 주변에 남은 디스필들을 제거. 머리색과 피부색을 활용. 디스필에 alphabias가 활성화 되어 있어야만 사용 가능. 
3. gangBiases: alphabias 색을 despillbias 색으로 사용. 

**Keylight**   
1. insidecomponent: InM 인풋에서 Inside Mask로 사용할 요소들과 관련된 기능 조절. 
2. outsidecomponent: InM 인풋에서 Outside Mask로 사용할 요소들과 관련된 기능 조절. 

[Keying with Keylight](https://learn.foundry.com/nuke/content/comp_environment/keying_with_keylight/keying_keylight.html)    
[Keying with ChromaKeyer](https://learn.foundry.com/nuke/content/comp_environment/keying_with_chromakeyer/keying_chromakeyer.html)   
[Keying with Primatte](https://learn.foundry.com/nuke/content/comp_environment/keying_with_primatte/keying_primatte.html)   
[Keying with Ultimatte](https://learn.foundry.com/nuke/content/comp_environment/keying_with_ultimatte/keying_ultimatte.html)   


