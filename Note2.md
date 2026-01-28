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

# 12
투시 원근법 원리 적용  
perspective projection transformation(원근 투영 변환) - 공간 모든 점이 한 점을 향하는 형태로 변환, 원근법 적용  
field of view(FOV, 화각) - 카메라에 보이는 범위, 좌우 위아래 균등한 사각뻘 영역 만들어짐  
x,y,z축 직교 뷰 공간 -> 카메라 한 점으로 모이는 사각뿔 형태 공간  
projection plane(투영 평면) - 모든 물체 상이 맺히는 가상 평면, 위 아래 크기가 1이 되는지점으로 설정    
focal length(초점 거리) - 카메라부터 투영 평면까지 거리, 화각에 따라 투영 평면이 변하며 바뀜, tan(Θ/2) = 1/d    
NDC(normalized device coordinate) - 투영 평면에 대응하는 좌표계  
유클리드 공간 - 축이 모두 직교하는 공간  
사영 공간(projective space) - 사각뿔 형태 공간, z축에 영향받는 직교하는 x,y축  
종횡비(aspect ratio) - 화면 가로 세로 비, 원근 투영시 고려  
P(ndc) = -d/vz(vx/a,vy), (a=종횡비), z값은 d 고정  
행렬에는 좌표마다 달라지는 vz값 사용하지 않아야 함  
clip coordinate - 보편적 원근 투영 행렬(vz값 사용하지 않은 3x3 행렬)로 변환한 좌표계, P(clip) = (d*vx/a,d*vy,-vz)  
-vz로 나눠 NDC 좌표로 변환  
동차 좌표계(homogenous coordinate) - 좌표 1차원 증가시켜 표현한 좌표계, 미지수 차수 동일한 성질 이용해 클립 좌표 이용 가능  
depth - 카메라로부터 물체가 떨어진 정도의 값, 깊이 값 반영해 순서대로 렌더링    
절두체(frustum) - 사용 공간을 근평면(near plane), 원평면(far)으로 자른 형태, 3차원 NDC영역(깊이 값 포함), 왼손 좌표계  
카메라부터 근평면까지 거리 n, 원평면까지 거리 f 이용해 원근 투영 행렬, 클립된 좌표 (x,y,depth,-vz), -vz로 나눠 ndc 좌표 (x(ndc),y(ndc),depth(ndc))  
투영 보정 보간(perspective correction interpolation) - 투영 전 무게중심좌표 값 계산해 텍스처 매핑  
사영공간 NDC 무게중심좌표 달라지는 현상(뷰공간 -z값=사영공간 w값 으로 나눔) 해결  
원근 보정 매핑(perspective correction mapping) - 투영 보정 보간 이용해 무게중심좌표 구해 텍스처 매핑  
tn = z'/zn *qn (tn=사영공간 무게중심좌표, qn NDC 무게중심좌표, zn=정점vz값, z' = 1/(qn*1/zn+...)픽셀 vz값)  
깊이 버퍼(depth buffer) - 픽셀 단위로 깊이값 보관하는 버퍼  
깊이 테스팅(depth testing) - 현재 깊이값과 깊이 버퍼에 저장된 값을 비교하며 픽셀을 찍는 방식, 그리기 순서, 가려지는 픽셀 확인, 깊이 비슷한 오브젝트 렌더링  

## 12-1
원근 투영 행렬 적용 후 -z값으로 나눠 NCD로 변환, 백페이스 컬링, 화면에 맞춰 확대  

## 12-2
원근 투영 행렬, 뷰 행렬 한번에 곱해서 사용, 클립된 좌표 (x,y,depth,-vz) 형태  

## 12-3
아핀 텍스처 매핑(affine texture mapping)  
뷰 공간 -z값(클립공간 W좌표) 사용, z' 구하고 UV값 계산식에서 각각 invzn으로 나눈뒤 z`곱해 한번에 계산  

## 12-4
무게중심좌표와 정점 깊이(NDC z값) 이용해 픽셀 깊이값 구하기  
fragment(pixel)에 해당하는 depth buffer값 깊이값과 비교해 더 작으면 그리고 버퍼 갱신 아니면 넘기기  
픽셀 1개마다 데이터 저장 -> 1920*1080 = ?  
n평면 작지않게 조정 필요, z-fighting - 깊이값 정밀도 문제로 픽셀 깜빡거리는 현상  

## 12-5
깊이값 - -vz로 나누는 반비례 비선형 형태 - 깊이 값 급격하게 올라감  
원근보정매핑 공식 응용해 뷰공간 깊이값 계산  
z' = 1/q1/z1 + q2/z2 + q3/z3(픽셀의 vz값=뷰공간 z값, 클립 w값), 깊이가 vz값을 이용하니 미리 구한 z`값 재사용하는듯  
c(depth) = z'-n/f-n, near,far값 으로 나눠 선형화된 [0,1]범위 뷰공간 깊이  

# 13
절두체 컬링(frustum culling) - 절두체 영역 밖 오브젝트 컬링, 절두체 평면 외부 물체 무시, 뷰공간  
평면의 방정식 사용, 법선벡터로 위아래 구분, n*(P-P0)=0, ax+by+cz+d=0, d=-n*p, -원점to평면 최단거리, 평면 방향(+원점-반대)  
임의 점과 평면 법선 내적+d 부호로 임의 점이 평면 내부 외부 판별 +바깥-안, 절대값 최단거리  
절두체 - near,far 제외 모두 d=0, 법선벡터 부호변경x  
NDC좌표 (nx,ny,nz) [-1,1]범위면 frustum 내부, 클립 좌표 (x,y,z,w)에서 -w<=x,y,z<=w, 뷰공간 좌표 v=(vx,vy,vz,1)  
P(원근투영행렬)*v = (x,y,z,w), x=P(row1)*v, y=P(row2)*v, z=P(row3)*v, w=P(row4)*v  
(Prow4+Prow1)*v>=0, (Prow4-Prow1)*v>=0, (Prow4+Prow2)*v>=0  
(Prow4-Prow2)*v>=0, (Prow4+Prow3)*v>=0, (Prow4-Prow3)*v>=0  6개 부등식 만족  
Prown+-Prowk = (a,b,c,d), (a,b,c,d)*v>=0, 평면방정식 -(ax+by+cz+d)/root(a^2+b^2+c^2)>0 컬링  
카메라 원근투영행렬 이용해 코사인 사인값 쓰지않고 NDC좌표값 반영된 화면 종횡비 고려한 컬링  
Bounding volum - 원시 도형(primitive shape|sphere, box 등등)으로 설정한 공간 데이터  
구(sphere) - 중심(메시 중점)과 반지름(중점과 가장 먼 점), 거리와 반지름 비교, 평면과 중심 거리(법선벡터 내적+d), 반지름 비교로 내외부 확인  
AABB(axis aligned bounding volume) - 메시 구성 점 축별 최대 최소값 두 점  
평면 법선벡터 축 부호에 해당하는 점 ex) (+,-,+)과(min,max,min) 내적+d로 내외부 판단, 양수 밖, 음수+반대방향 점 결과 양수 교차, 음수+음수 내부   

## 13-1  
pcos,psin = cos(Θ/2),sin(Θ/2)  
Plane(Vector3(pCos,0.f,pSin),0.f), // +Y  
Plane(Vector3(-pCos,0.f,pSin),0.f), // -Y  
Plane(Vector3(0.f,pCos,pSin),0.f), // +X  
Plane(Vector3(0.f,-pCos,pSin),0.f), // -X  
Plane(Vector3(0.f,0.f,1.f),nearZ), // +Z  
Plane(Vector3(0.f,0.f,-1.f),-farZ, // -Z  
frustum 평면 계산 후 내부외부 계산해 컬링  

## 13-2
Plane(-(ptMatrix[3] - ptMatrix[1])), //+Y  
Plane(-(ptMatrix[3] + ptMatrix[1])), //-Y  
Plane(-(ptMatrix[3] - ptMatrix[0])), //+X  
Plane(-(ptMatrix[3] + ptMatrix[0])), //-X  
Plane(-(ptMatrix[3] - ptMatrix[2])), //+Z  
Plane(-(ptMatrix[3] + ptMatrix[2])) //-Z  
사인 코사인 계산없이, 종횡비 반영  

## 13-3
구 반지름에 스케일 반영, 구 중심 뷰 공간으로 변환  

## 13-4
원근투영 행렬 P 대신 뷰,모델링 행렬 곱한 PVM을 컬링 검사에 사용에 로컬 좌표로 컬링  
모델링 행렬 따로구해 바운딩 볼륨 뷰 공간 변환하지 않고 컬링  

## 13-5
sphere에 비해 정교하고 계산량 높음  
