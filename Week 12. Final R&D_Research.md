1. 기존 기획 피드백
 - 12주차에 만든 공간의 오른쪽 부분이 너무 비어 보임
 - 전체적인 공간의 대비감과 합성한 요소들 간의 대비 맞춰주기
 - volume ray가 있는 이미지를 합성했기 때문에 누크에서 volume ray 기능을 활용해 보기

2. 수정해야 할 사항
 - 추가 합성 및 보정
 - volume ray 리서치

3. R&D
3-1. 추가 합성 및 보정
좌 - 기존 합성 공간 / 우 – 추가 합성 및 보정 후
  

3-2. 바다 공간 플레이트 트래킹 / 마야 작업
플레이트 소스 출처: https://www.pexels.com/ko-kr/video/10132840/
  
![door](https://user-images.githubusercontent.com/90232599/145673430-bd663d87-b75e-4c03-a343-25a31c4825f1.jpg)
![tracking](https://user-images.githubusercontent.com/90232599/145673442-c0a701b6-2fd2-4b42-9ec2-2de24f6ac9f4.jpg)

- 원본 영상을 거꾸로 재생되도록 편집
- 문 안쪽 로토스코핑으로 알파채널 만들어 다음 매트페인팅 공간과 연결될 수 있도록 작업
- Camera Tracker 노드 사용해 트래킹
- 카메라, 트래킹 포인트 FBX 파일 추출 후 마야에서 작업

- 원본 영상에서의 카메라 흔들림 때문에 트래킹 포인트가 제대로 잡히지 않음
- 원본 영상 중에서 초점이 흐려지고 맞춰지는 구간이 있어 로토/합성에 어려움

4. Research - [Volume Ray](https://en.wikipedia.org/wiki/Volumetric_lighting)   
Volume Rays = Volumetric lighting, God Ray, Light Shaft, Crepuscular rays, ...   
3D 그래픽에서 렌더링된 scene에 조명 효과를 더해주는 것의 일종    
공간 안에서 뚜렷하게 빛의 형태(광선)이 보이는 것이 특징이며, 3D로 이를 구현하면 현실에서 안개나 먼지, 연기, 증기와 같은 대기를 통과하는 빛의 효과를 보여줄 수 있음   

![Example](https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Environment_lighting.png/260px-Environment_lighting.png)   

- VolumeRays node: https://learn.foundry.com/nuke/content/reference_guide/filter_nodes/volumerays.html
- [How to make realistic Volume Rays in Nuke](https://youtu.be/thXx_LNlPSU)
- [Nuke: Realistic Volume Rays](https://youtu.be/xs5rJuD59vw)   

