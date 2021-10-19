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
