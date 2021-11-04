## Planar Tracker: 평면의 움직임을 트래킹하기
Roto 노드에 달려 있는 기능. Roto - Tracking 탭    
Tracker 노드가 아니라 roto에 달려있기 때문에 로토 shape를 따서 트래킹 할 수 있다는 것.   
<br/>
1. 원본 플레이트 - Denoise - Roto 순으로 연결
2. 로토로 따고 싶은 면(Ex. 표지판, 간판 등) 형태 잡아주기
3. 로토 노드 창의 shape을 딴 bazier 우클릭 후 Planar-track 선택(bazier가 폴더 속으로 들어가고, shape 색이 보라색으로 바뀜)
4. 이후는 다른 tracker 노드와 똑같이 진행하면 됨. (range 범위 설정, 자동 트래킹 실행 등)
5. 그러나 일반적으로 우리가 트래킹 하는 평면은 원래 사다리꼴 모양인 것이 아니라, perspective가 들어가서 모양이 틀어져 보이는 것.
6. 뷰어 상단의 그리드를 켜서 확인해보면 그리드 모양이 perspective와 맞지 않음 
7. 그리드 옆의 Correct Plane 버튼 누른 후, 나타나는 노란색 사각형을 우리가 설정하고 싶은 planar의 형태에 맞게 조정해주기
8. 그러면 그리드도 perspective에 맞게 변형됨
9. 바꾸고 싶은 이미지를 갖고 와서 shuffle 노드 달아서 알파만 빼주기
10. 로토 탭의 Planar Track Layer 선택 후 CornerPin2D(absolute) export 해주기
11. 바꾸고 싶은 이미지에 ConerPin2D 연결
12. ConerPin2D(A), 원본 플레이트(B) Merge(over) 노드로 연결
13. ConerPin2D - From 탭에서 set to input 클릭해주면 바뀜
14. ConerPin2D 노드에 EdgeBlur, Blur 등의 노드 달아서 자연스럽게 합쳐주기
15. Grain 노드를 달아도 됨. 픽셀에 노이즈를 넣어주는 것. 


## 3D Space
NODE: Scene - 마야에서 새로운 파일을 여는 것과 동일. Scene1, Scene2 ... = 1.mb, 2.mb ...   
NODE: Camera - 3D 공간을 바라보는 카메라    
NODE: ScanlineRender - 3D 공간을 2D로 볼 수 있도록 스캔해주는 노드    

## Camera Tracker
**CameraTracker**    
일반적으로 촬영된 영상 시퀀스를 활용하기 때문에 source - sequence로 설정해둠.   
Mask: 트래킹할 때 필요하지 않은 부분(Ex. 인물, 움직이는 차 등)을 로토로 잡아서 camera tracker에 연결해준 후, Mask Alpha로 설정해주면 해당 영역을 제외하고 트래킹함    
Camera Motion: 카메라가 움직이는지   
Lens Distortion: 플레이트를 촬영할 때 찍은 렌즈 왜곡 값. 모르면 Unknown   
Focal Length: 렌즈 화각. 모르면 Unknown   
Film Back Preset: 플레이트가 1920/1080이라고 하더라도 더 크게 찍어서 크롭한 건지 모르기 때문에 확실하지 않으면 Custom    

<br/>

**Settings**  

<br/>

**AutoTracks**     
VFX 수업에서 Tracking 하던 것과 동일.   

## MattePainting
포토샵에서 합성을 한 후 PSD로 저장, 누크에서 파일을 불러오면 PSD Options가 생기는데 이때, Breakout Layers를 해주면 레이어에 따라 분리됨.   
다만, 이 때 자동생성되는 Shuffle 노드는 구버전이기 때문에 잘 모르겠으면 Shuffle 노드를 새로 생성한 후, Input 값을 자동생성된 셔플 노드를 참고해 바꿔준 후 사용하면 됨.    

1. breakout layers 해서 만들어진 노드에 각각 premult를 붙이고, card로 연결.
2. Scene 노드에 연결해서 보면 모든 레이어가 겹쳐져서 보임
3. card 노드를 선택, 가장 멀리 있는 배경 레이어부터 z 값을 조정하며 거리감 조정해주기
4. 이후, camera의 translate-z 값을 조정해주면서 앞 뒤로 이동시켜보면 depth가 생김 

