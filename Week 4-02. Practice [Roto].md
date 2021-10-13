## Roto

[Nuke/Learn/Roto](https://learn.foundry.com/course/4689/view/8-roto)

**Rotoscoping**   
촬영한 것을 2D로 트레이싱한 프레임을 로토스코핑이라고 함. 

알파 채널을 만들어주려는 대상을 로토스코핑할 때, 형태의 큰 아웃라인으로 따는 것 보다는 구역을 나누는 것이 좋음.    
: 형태가 변하거나, perspective가 변하는 경우가 있기 때문.   

상처, 문신 등을 지우거나 혹은 그런 요소들이 들어가야 하는 경우를 위한 밑작업.

1. [O] Roto node 생성   
2. 좌측 탭 펜 모양에서 roto 선택  
3. 뷰어에서 형태 따주기
4. [Z] 곡선 넣어주기
5. [E] 페더값 넣어주기 
6. [P] RotoPaint node 생성   
7. Roto node에 Shuffle node 생성 후 연결  
8. Shuffle에서 R, G, B, A 연결 전부 풀어주고 좌측 A랑 우측 R 연결
9. write 파일 포맷은 .dpx, .exr. Roto shape만 있는 경우에는 .dpx (.dpx: vpx, 편집에서 거의 표준으로 쓰는 rgb 데이터가 포함된 포맷. 렌더링 할 때는 반드시 rgb로 해야 함.) 
9-1. **파일명 입력할 때 (파일이름).####.dpx로 해줘야 함 #### 없으면 렌더링 불가능**
10. .dpx 파일 누크로 불러오기
11. copy node 생성해서 .dpx 파일(A)랑 원본 플레이트(B)에 연결(A에서 B로 넘겨준다)
12. Copy node에서 Copy channel을 [rgb.red] to [rgb.alpha]로 바꿔주기
13. 그러면 플레이트에 원래 없었던 alpha 채널이 .dpx 파일의 r채널과 똑같은 모양으로 생성됨
14. Copy node에 premult node 생성 후 연결
15. 알파 채널 확인해보면 형태 따진 게 보임. 
16. checkerboard node 생성, merge(over) node 생성 후 merge에 premult(A)랑 checkerboard(B) 연결

Roto랑 RotoPaint는 거의 비슷함. RotoPaint에 더 많은 기능이 있음. 

레퍼런스로 삼을 프레임   
: 모션블러가 가장 적은 프레임. shape가 가장 잘 드러나는 프레임. 

Roto node에서     
premultiply - [none]에서 [rgba] 로 설정해주면 플레이트 원본+까만 배경 볼 수 있음
bazier 우클릭 후 duplicate 선택하면 복사 가능, ctrl+a로 이동   
손가락 같은 경우, 마디 별로 형태를 따준 후 roto node의 표에서 새 레이어 생성, 마디 Bezier끼리 묶어주며 전체적으로 이동시키기 


