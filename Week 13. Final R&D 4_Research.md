### 기존 기획 피드백
3D 트래킹이 들어가야 함 - 사용할 영상 플레이트 다시 찾아서 작업해보기    
12주차에 만든 공간 뒤로 더 많은 풀 합성해보기 - 바닥의 틈 가려지면 좋음    
noise 노드를 활용해서 배경에 사용된 이미지에 애니메이션 주기    

<br/>

### 수정해야 할 사항
추가 합성 및 보정    
noise 노드 리서치    
**영상 플레이트 다시 찾기**  
 
<br/>

### R&D

**3-1. 옷장 영상 촬영**   
![closet074](https://user-images.githubusercontent.com/90232599/145719658-85f3a8ba-0caa-42e3-992a-6865692d2103.png)
![closet_chromakey](https://user-images.githubusercontent.com/90232599/145719703-2bf1d3e9-a71b-4ef3-a094-59ce2f10020a.png)   
1. 옷장 영상 촬영 후 어도비 프리미어에서 안정화 작업
2. 누크에서 로토/크로마키 활용해서 알파 추출  

**3-2. 플레이트 연결**
![closet_flower](https://user-images.githubusercontent.com/90232599/145719873-97dd866c-c0bd-4a60-98c3-408af18d067c.png)
![compositing](https://user-images.githubusercontent.com/90232599/145719900-2d722ba3-e930-4ce8-b5f8-3abee98f270c.png)  

<br/> 

- 옷장 영상 재촬영해보기.. 
- 마지막 공간 Zdepth 적용한 후로 좌측에 조금 깨지는 부분 생김 - 위치 애니메이션 조정해서 다시 렌더링 걸어보기 

<br/>

### Research
[**Idistort**](https://learn.foundry.com/nuke/content/reference_guide/transform_nodes/idistort.html)       
이미지의 UV 채널을 활용해서 이미지를 변형시키는 노드.       

[Using Idistort and noise to create natural FX](https://youtu.be/XnNPA5yCkxs)   
