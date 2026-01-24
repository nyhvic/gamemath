# 10
right/left handed coordinate - z축 모니터 앞/뒤, x-y-z-x-y, 프로그램마다 z up/y up 등등 다르게 사용  
scale, translate transform 동일, rotation은 다름 x축/y축/z축 회전, 오일러 각  
euler angle - object 방향 3개 각으로 표시 pitch yaw roll, 프로그램마다 다르게 사용  
x축, y축, z축 회전행렬 - x축(yz 회전), y축(zx 회전), z축(xy 회전)  
pitch yaw roll 순서 프로그램마다 다름 ex) unreal - R = R(yaw) * R(pitch) * R(roll), 동일하게 로컬 축 벡터(회전행렬과 동일) 저장해 사용  
M = T*R*S로 변환행렬 곱해서 사용 or 미리 구해진 modeling matrix 식에 scale, rotation, translation 값(벡터) 대입해서 사용(gpu/cpu기준으로 다르지 않을까?)  
카메라 - view matrix - modeling matrix의 역행렬, V = M^-1 = R^-1*T^-1, (R행렬은 직교행렬. 전치), x,y축 방향 맞게 회전  
오일러 각 - 적은 용량, 직관성  
gimbal lock - 특정 상황에서 회전 움직임 제한되는 현상, 오일러 각 방식에서 회전을 3번으로 나눠 진행하기 때문, 로드리게스, 사원수 사용으로 해결  
rotation interpolation - 회전 보간, 시작 회전과 끝 회전 전환시 경과된 시간에 따른 중간 회전 값 계산, Θ` = (1-t)Θ(start) + tΘ(end)  
두 각의 회전 변환 곱한 값이 두 각의 합의 회전 변환과 같아야 함 - 회전 나누어 적용/합쳐서 적용 같아야 함 - 같은 축의 회전만 보간 가능, 다른 축은 성립하지 않음  
캐릭터 회전은 주로 y축만 하므로 보간 가능, 다른 회전은 다른 방법 필요  

## 10-1
xy축 맞추기 위해 y축 180도 회전  

# 11
cross product - 3차원, 교환법칙,결합법칙x, 평행시 0, 값 크기 사인값에 비례(이루는 평행사변형 크기), 직교하는 벡터 생성  
normal vector  
시선벡터 f, 물체방향 벡터 v fxv값과 up vector 비교(내적)으로 좌우 판별, +면 좌, -면 우  
카메라 로컬 축 구하기 - 카메라 시선벡터 v(물체-카메라) 정규화 = z, up vector(u)와 외적 = x, z와 x 외적 = y  열벡터 나열한 행렬 - 회전행렬  
카메라 위쪽방향이 +y방향인지 고려, 아니면 -y와 외적, z가 up vector와 평행할 경우 수동으로 x축 설정  
backface culling - camera에 보이지 않는 mesh 뒷면 생략  
인덱스 버퍼 정점 이용해 mesh의 face normal vector 계산 후 카메라 view vector와 내적해 같은 방향이면 생략  
axis-angle rotation - 임의의 축에 대한 회전  
로드리게스 회전 공식 - 점 P가 축 n에 대해 Θ만큼 회전(u = P - O) -  u` = cosΘ + (1-cosΘ)*(u*n)*n + sinΘ*(n x u)    
행렬 변환 어려움, 추후 사원수로 회전 구현  
triple product - 3 벡터(u,v,w)의 내적,외적 이용한 연산  
scalar triple product - u*(v x w)형태, v x w 크기 = 평행사변형, 만들어지는 법선벡터 크기, |u|cosΘ = |vxw|에 투영한 벡터 높이 -> u,v,w의 육면체 부피  
세 벡터가 선형독립인지 판별 - 0이면 종속, u*(v x w) =  v*(w x u) =  w*(v x v)  
vector triple product - u x (v x w) = (u*w)*v - (u*v)*w  (triple product expansion, 라그랑주 공식), 각 성분 전개 후 계산  
v,w의 선형결합 형태 - 삼중곱 결과가 v,w가 만드는 평면에 속함  
이차원 평변 벡터 u와 동일 평면 임의 벡터 v 이용해 (u x v) x u로 u와 직교벡터 계산 가능  
추후 사원수 연산에 활용  

## 11-1
특정 object(플레이어)추적 카메라  

## 11-2
인덱스 버퍼 정점으로 face normal vector 계산, 내적  

## 11-3
회전할 축의 n과 회전할 각 세타와 정점 이용해 로드리게스 회전 공식에 대입해서 구하기, 행렬 변환 어려워 scale, translate 추가로 해줘야함  
