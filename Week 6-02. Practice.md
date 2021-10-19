Keyer: 기본적으로 루미넌스 키어. red, green 등으로 바꾸면 플레이트의 레드, 그린 값이 알파채널이 됨.    
단, redscreen 같은 경우에는 다른 채널에서 red 값을 빼버리는 것.   
<br/>
Framehold node: 특정 프레임을 레퍼런스로 삼고 싶을 때 사용.     
Difference(alpha) node: 두 프레임의 차이를 알파값으로 빼냄. 크로마키 보다는 최종 컬러 점검 시 주로 사용.      

## Keylight     
시작할 때 스크린 컬러를 지정해줘야 함. 그린스크린인지, 블루스크린인지 등     
스크린의 한 픽셀을 지정해서 RGB 값 입력해주거나, 옆의 스포이드 기능을 활용하면 됨.      
하지만 알파 값이 고르지 못한 경우, ctrl+shift 키를 누르고 플레이트 상에서 알파로 뺄 영역을 드래그해주면 해당 영역의 평균 값이 알파로 빠짐.     
Screen Gain값을 조절할 수 있으나 알파채널이 원본을 잡아먹을 수도 있음. 
Screen Balance를 통해 레드와 블루의 밸런스 조정 가능.     
노드의 인풋 중 InM/OutM 등은 마스킹할 때 필요. 

**Screen Matte** 탭을 주로 사용.    
Clip Black, White 노브(파라미터) 조정 통해 알파 채널의 블랙과 화이트 값 조정 가능. 
Clip Black 값을 높이면 그 값보다 작거나 같은 것들은 전부 0으로 변함.    
Clip White 값을 낮추면 그 값보다 높거나 같은 것들은 전부 1으로 취급함.      

## Denoise     
기본적으로 좌측 하단을 레퍼런스로 삼고 있음. 레퍼런스 영역을 이동시켜주기.     
Tun Frequenceis - Tune Channel에서 Luminance Gain, Chrominance Gain 값을 조정하면 알파 채널의 노이즈가 부드러워짐.     
단, 너무 많이 값을 높일 경우 필요한 부분의 디테일도 뭉개지기 때문에 적절하게 활용하기.     
(유료 Denoise 플러그인: Neat Video)      

키를 뺀다 = 알파채널을 만든다.    

원본플레이트-Denoise-Keylight 연결 후 Copy 노드 생성, Keylight(A)랑 원본플레이트(B) 연결시키면 키라이트 작업하는 동안 달라진 원본 컬러와는 무관하게 원본과 알파채널을 연결시킬 수 있음.    
이후 Copy에 Premult 연결시키기    

## Primatte
fg: 그린을 뺄 플레이트, bg: 그린스크린 밑에 깔린 플레이트   
Operation 순서대로 작업이 진행됨.    
Smart Select BG color: 스포이드로 그린스크린 색 빼기     
Clean BG Noise: BG에 해당하는 노이즈들을 ctrl+클릭해서 알파로 빼줌.     
Clean FG Noise: 앞서 알파로 빼면서 FG로 남아야 하는 부분까지 넘어간 곳을 빼줌     
Spill(-): 스필을 없애주는 기능. 하지만 컬러 자체를 조정하는 기능이기 때문에 조심해서 사용해야.     

<br/>

.dng: 디지털 카메라로 촬영한 원본 파일인 raw 파일들(.cr2, .arw. ...)을 공용 포맷으로 바꿔놓은 것.


1. 소스 불러오기
2. Denoise 노드 달아서 수치 조정하며 노이즈 없애기
3. Keylight 생성
4. 스크린 색 스포이드로 지정
5. Screen Matte에서 Clip Black 값 조정하기
6. 여러 부분으로 나눠 알파채널 빼줘야 하면 2~4 반복
7. 헷갈릴 수도 있으니 각각 파트 별로 이름 달아주기!
8. Keymix 노드 생성
9. 왼쪽에 있는 Keylight(A), 베이스가 되는 Keylight(B)로 연결
10. Roto 노드 생성 후 mask 인풋으로 연결
11. A인풋에서 필요한 만큼 Roto로 영역 따주기
12. 이 Keymix 밑으로 또 Keymix 달아주면서 다른 Keylight들도 합쳐주기
13. Premult 노드 생성 후 마지막 Keylight에 연결
14. Checkerboard - Merge(over) 생성 후 Premult에 Keylight(A), Checkerboard(B) 연결
15. 확인해보면 키로 뺀 대상에서 블랙에 가까운 부분은 체커보드가 보임. 해당 영역 담당하는 Keylight로 가서 Clip white 미세하게 조절하면서 알파 완성해주기. 
16. 카메라가 움직이면서 로토도 따라서 애니메이션 되어야 함. 프레임 따라가면서 조정해주기. 

## IBK Gizmo / IBK Colour
IBK: Image Based Keying    
배우+배경 장면(A)을 촬영하고, 배우가 없는 배경(B)을 똑같이 따로 촬영함.   
IBK Gizmo의 fg에 (A)를 연결하고, IBK Colour 혹은 IBK Gizmo 노드의 C에 (B)플레이트를 얹으면 A와 B의 차이를 계산해서 알파채널을 뽑아냄.    

IBK Colour에서 스크린 유형(green/blue)을 결정하고 나면 그 색이 아닌 영역이 블랙으로 빠짐.    
size 노브를 조정해서 블랙의 영역을 없애주고, IBKGizmo의 bg에 연결시켜주면 그 차이를 이용해서 키가 빠짐.   
그렇지만 이런 과정을 통해서도 완벽하게 키가 빠지지는 않음. 빼내야 하는 대상의 영역에서 알파 값이 남아 있어 Checkerboard-Merge(over) 노드를 통해 보면 체커보드가 보이는 것으로 확인 가능.    
<br/>


## Soft Key / Hard Key

위와 같은 상황에서 활용되는 것이 Soft Key, Hard Key.    

**Soft Key**: 외부의 디테일    

**Hard Key**: Key를 따야 하는 내부의 영역. 완벽하게 알파가 1로 나와야 하는 부분.    
Keylight을 내부 영역에서 Clip black과 Clip White 수치를 조정해 알파로 빼줘도 됨. 

작업하다보면 Hard Key가 Soft Key보다 넓어지거나, 정해진 범위 밖으로 뚫고 나와 Soft Key의 영역을 침범하는 경우가 발생함. 이 때 Erode필터인 FilterErode 노드를 사용해 Hard Key 매트를 조금 더 내부로 사이즈를 줄여줌.      
Hard Key와 Soft Key의 분리가 너무 딱딱하면 Blur 노드를 통해 부드럽게 바꿔줄 수 있음. channel - alpha로 변경해서 사용해야 함.   

Soft Key와 Hard Key를 합쳐주는 방법: **ChannerMerge(alpha∪alpha)**    
그냥 copy를 쓰면 둘이 분리되는 것이 아니라 인풋이 그냥 넘어가기 때문에 사용X     
Soft Key와 hard Key를 합쳐준 ChannelMerge(A)랑 원본 플레이트(B)를 Copy로 연결시킴     

Premult 노드로 확인해보면 그린스크린 색이 많이 남아 있음.  
이 때 Despill 작업을 위해 사용해주는 노드가 HueCorrect(Copy와 원본 플레이트 사이에 연결시키기)       
HueCorrect 노드에서 그린 스크린 영역을 플레이트 상에서 지정한 후 그래프에서 색상 조정해주면 교정 가능.    
* 플레이트에서 고른 색만 그래프에서 조정하는 법: 뷰어 화면에서 교정할 색 지정 - HueCorrect 노드 그래프에서 ctrl+alt 누르면 해당 지점만 점 찍기 가능. 그대로 수치 낮춰주면 교정.    

그래도 아직 Despill이 있을 때 - **Despillmadness** 사용하기.    
그린스크린이 회색빛으로 바뀜 - 추출하는 플레이트에 묻은 색이 자연스러운 색상으로 변함. 

추출한 플레이트에 그린스크린 색이 묻어 있을 때 색상 디테일 살리는 방법: ColorSmear


<br/>

* Keyer는 여러 개를 써도 됨
* Keyer를 바꿔가면서 써도 됨
* Keymix를 통해서 여러 파트로 나눠서 작업해도 됨

<br/>

## Grade
Black point / White Point: Keylight의 Clip black / white와 유사한 기능.   
lift: linear 커브에서 가장 밝은 부분인 (1,1)은 그대로 둔 채 어두운 영역부터 값을 조정함.    
offset: 기존의 linear 커브와 평행하게 커브를 이동시키며 전체적인 명암 조정.    
gamma: 블랙(0,0), 화이트(1,1) 값은 고정한 채 중간 값만 조정. 
gain: 화이트를 기준으로 수치를 곱해주는 것. 
multiply: rgb 픽셀에 수치를 곱해주는 노브.    

## ColorCorrec
Shadow / Midtone / Highlight 조정    
Ranges 탭에서 각 영역의 범위 확인 가능    
