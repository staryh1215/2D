### 피드백
공간과 공간 연결이 자연스럽게 이어지도록

<br/>

### 수정해야 할 사항
옷장 플레이트 재촬영
Forest - Grass 플레이트 자연스럽게 연결될 수 있는 방법 찾기

<br/>

### R&D
1. 옷장 플레이트 재촬영
- 재촬영 후 영상 편집    
- 누크에서 로토로 알파채널 분리
![2  original](https://user-images.githubusercontent.com/90232599/146661355-b7680330-fe95-44ef-9e86-3198c174f2f3.png)
![2  original_alpha](https://user-images.githubusercontent.com/90232599/146661358-e374a5e9-651a-4258-ac92-6042d29c27dd.png)

<br/>

2. Forest - Grass 플레이트 연결
- Grass 매트페인팅 scene에 forest 플레이트에서 트래킹한 카메라 복사 붙여넣기
- 카메라의 axis에 또 다른 카메라 연결시켜 애니메이션 주자 기존 카메라에 애니메이션 추가됨
- 이후 Z depth 애니메이션 주며 Grass 플레이트 완성

<br/>

3. 옷장에 그림 합성(2D Tracking)
- 옷장 문에서 Tracker 노드로 2D 트래킹
- CornerPin2D 노드 생성해서 이미지 합성
![original](https://user-images.githubusercontent.com/90232599/146661347-46e7a300-253a-40d8-a51b-eb4dad1e13c5.png)
![postcard](https://user-images.githubusercontent.com/90232599/146661349-159c79fc-bf73-488e-b114-267cd3818d9d.png)

<br/>

4. 플레이트 전부 연결 후 카메라 애니메이션/시간 조정하며 완성

