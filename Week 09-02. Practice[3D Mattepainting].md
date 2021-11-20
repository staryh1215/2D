포토샵에서 합성한 매트페인팅 psd 파일을 누크로 불러오면 Breakout Layers 기능으로 레이어 별로 나눌 수 있음    
각 레이어 별로 필요한 경우에는 psd 파일을 불러온 후 그 아래에 Shuffle 노드를 달아 Input Layer에서 원하는 레이어를 선택하면 됨. 
 - 이 경우에 레이어 라밸링 할 때 레이어 입력을 하나하나 적는 게 아니라 [value in1] 을 입력하면 자동으로 라밸링 됨  
 
 <br/>
 
Edit Geo 노드를 활용해서 마야에서 vertex 조정하듯이 카드에 볼륨감을 줘서 입체감을 더할 수 있음    
1. card 노드 밑에 Edit geo 노드 생성 후 연결
2. card 노드의 rows/columns 잘게 쪼개주기
3. Edit geo 노드 선택 후, tab 키로 3D 뷰어로 전환하면 창 상단, 카메라 아이콘과 곡선 아이콘 사이에 node selection 아이콘이 있음
4. 이를 vertex selection, face selection 등으로 바꿔주면 선택할 수 있는 지점들이 생김
5. 그 옆의 곡선을 선택하면 soft selection 기능이 활성화되고, 범위를 지정하기
6. card 지오메트리를 원하는 대로 변형시키면서 입체감 더해주면 됨 

<br/>

이후 Color Correction 노드를 활용해서 saturation, contrast를 활용해서 멀리 있는 레이어가 흐려지도록 만들 수 있음    
하지만, 레이어가 많아지면 하나하나 설정하기 번거로워짐    
이 때 기준이 되는 레이어를 하나 선택하고, saturation과 contrast 값을 조정한 후 파라미터 옆의 곡선 아이콘을 선택, Copy - Copy Link 후 더 멀리 있는 레이어의 동일한 파라미터에 paste relative를 해주면 링크가 생김    
이렇게만 하면 똑같은 값이 입력됨 
곡선 아이콘 선택 후 Edit expression 선택, Expression으로 들어와 있는 값 옆에 *0.8, *0.7 등 1 이하의 값 입력해주면 참조 레이어의 값에 비례해 수치가 낮아짐    

<br/>

### Project 3D
평면의 이미지 하나를 가지고 3D 공간 만들기   

1. 이미지 불러오기
2. card, scene, camera, scanlinerender 노드 생성 후 연결. 단, 원본 이미지는 scene이 아니라 scanlinerender로 바로 연결하기
3. card에 grid 노드 생성 후 달아주기
4. 원본 이미지를 보면서, grid가 달린 card의 translate, rotate, scale 값을 조정하며 공간의 정면, 위, 아래, 옆면 만들어주기
5. 꺾이는 면이 있다면 꺾이는 면까지 만들어주기. 
6. Project3D 노드 생성, cam에 카메라, 나머지 인풋에 원본 이미지 넣어주기
7. 앞서 사용했던 card와 scene 노드 전부 복사 붙여넣기 후 project3D 노드의 아웃풋에 연결(project3D 노드 하나에 아웃풋 여러 개_
8. camera 노드 하나 더 만들기(렌더링용)
9. scanlinerender에 scene과 렌더링용 camera 연결 후 이 카메라에 애니메이션 넣기 
