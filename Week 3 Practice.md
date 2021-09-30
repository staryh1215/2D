**Rotoscoping/Chroma Keying**   
: 알파 채널을 만드는 과정. 

**Tracking and Match-move**   
: 매트 패인팅 등으로 만들어 놓은 2D/3D 공간을 2D 이미지로 만들어 놓고, 로토나 크로마키로 만든 알파 채널에 적용시켜놓고 카메라랑 똑같이 움직이게 만든다 / 어떤 특정 지점에 들어가게 만든다. 

Merge: B에 밑에 들어갈 대상(배경)이 오도록    
Merge over: A+B*(1`a)     
A: input A's RGB / B: input B's RGB / a: input A's alpha / b: input B's alpha     
**Merge(over)을 할 때는 꼭 위에 올라가는 대상에 Roto(alpha)[o], Transform[T]가 들어가야 함**

