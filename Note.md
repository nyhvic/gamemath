# 2
수, 집합, 함수, 체, 등등
# 3
Cartesian, Vector


## 3-1
FORCELINE - 컴파일러에서 함수 호출 대신 코드 복사해서 붙여넣어 사용  
explicit - 암묵적 형변환 차단  
constexpr - 컴파일 타임에 초기화 보장  
union -  메모리공간 같이 사용하는 데이터타입  


# 4
삼각함수, radian  
회전 - 기저 변환 (1,0), (0,1) to (cos,sin), (-sin,cos)  
(x,y) -> (xcos - ysin, xsin + ycos)  
역삼각함수  
arctan - x,y인자로 받음 -> 벡터 각 계산 arctan2(y,x)사용(-pi,pi)  
극좌표계 - x = r*cos, y = r*sin 회전 효과에 이용  

## 4-1~4
HSV - 색조(Hue), 채도(Saturation), 명도(Value)의 3요소로 색 표현  
4-3에서 크기 조절 추가구현  
Scale, Rotate, Translation 순으로 적용후 렌더링(World Coordinate 기준 렌더링)  

## 4-5
polar coordinate에서 각도 변환 후 cartesian coordinate로 변환해서 렌더링, 기능 변형해서 구현  

# 5
행렬  
공간변환 행렬곱 고속처리  
선형성 - addictivity + homogeneity  
선형변환, 결합법칙 성립 이용  
공간(기저)변환  
Scale, Rotate, Sheer  
Identity, Inverse, Determinent  
행렬식 0 - 차원 축소됨, 음수 - 기저 평면 뒤집힘  
역행렬 - 역변환  

## 5-1
T R S  

## 5-2
역변환 순서 반대로  

# 6
affine space - sheer transfom 이용해 차원 하나 확장하며 translation 행렬로 계산. 마지막 차원 값 1인 공간  
affine transform  
point(z=1), displacement vector(z=0) (z - 마지막 차원)  
affine combination - affine space point를 결합해 새로운 point 생성 - aP1+bP2 (a+b=1)  
a,b값 범위 설정으로 직선(Line), 반직선(Ray), 선분, 평면 등등 표현 가능  
screen coordinate - 이산적 좌표 사용, +y방향 밑  
Rasterization - 벡터좌표 screen coordinate로 변환 후 픽셀에 대응, 색 부여하는 과정  
브레젠험 알고리즘 - 정수로 화면에 선분 그리는 알고리즘, 스크린 8등분, 최초 판별식 구하기 -> 점 찍기 -> 판별식 값으로 다음 판별식 구하고 해당하는 점 찍기 반복  
선의 높이와 너비 판별식에 사용, 팔분면마다 다른 판별식  
라인 클리핑 알고리즘 - 선분을 화면 영역에 유효한 선분으로 자르는 알고리즘  
코헨-서덜랜드 라인 클리핑 - 화면을 9개로 나누고 4자리 이진 값 부여(0000 출력되는 화면), 선분 시작점과 끝 점에 각각 0000구역과 좌표 비교 후 이진 값 할당  
시작점과 끝점이 0000이면 바로 출력  bitwise and연산후 0000이 아니면 버림, 0000이면 각 점 클리핑  

## 6-1
변환 후 다시 원래 차원으로  

# 7
Dot product  
|u||v|cos(\theta), ac+bd  
직각이면 0  
행렬 내적표현, 직교행렬  
강체변환 - 물체 형태가 유지되는 변환 기저 크기1, 기저들 직교, det = 1  
벡터 방향 확인 - 같은방향 내적시 + 다른방향 -, 코사인값 이용해서 시야각 판별  
렘버트 반사 모델 - 표면 법선벡터와 광원방향 단위벡터 내적으로 cos값 구해 사용(3차원)  
투영, 집합, 함수, 체, 등등
# 3
Cartesian, Vector


## 3-1
FORCELINE - 컴파일러에서 함수 호출 대신 코드 복사해서 붙여넣어 사용  
explicit - 암묵적 형변환 차단  
constexpr - 컴파일 타임에 초기화 보장  
union -  메모리공간 같이 사용하는 데이터타입  


# 4
삼각함수, radian  
회전 - 기저 변환 (1,0), (0,1) to (cos,sin), (-sin,cos)  
(x,y) -> (xcos - ysin, xsin + ycos)  
역삼각함수  
arctan - x,y인자로 받음 -> 벡터 각 계산 arctan2(y,x)사용(-pi,pi)  
극좌표계 - x = r*cos, y = r*sin 회전 효과에 이용  

## 4-1~4
HSV - 색조(Hue), 채도(Saturation), 명도(Value)의 3요소로 색 표현  
4-3에서 크기 조절 추가구현  
Scale, Rotate, Translation 순으로 적용후 렌더링(World Coordinate 기준 렌더링)  

## 4-5
polar coordinate에서 각도 변환 후 cartesian coordinate로 변환해서 렌더링, 기능 변형해서 구현  

# 5
행렬  
공간변환 행렬곱 고속처리  
선형성 - addictivity + homogeneity  
선형변환, 결합법칙 성립 이용  
공간(기저)변환  
Scale, Rotate, Sheer  
Identity, Inverse, Determinent  
행렬식 0 - 차원 축소됨, 음수 - 기저 평면 뒤집힘  
역행렬 - 역변환  

## 5-1
T R S  

## 5-2
역변환 순서 반대로  

# 6
affine space - sheer transfom 이용해 차원 하나 확장하며 translation 행렬로 계산. 마지막 차원 값 1인 공간  
affine transform  
point(z=1), displacement vector(z=0) (z - 마지막 차원)  
affine combination - affine space point를 결합해 새로운 point 생성 - aP1+bP2 (a+b=1)  
a,b값 범위 설정으로 직선(Line), 반직선(Ray), 선분, 평면 등등 표현 가능  
screen coordinate - 이산적 좌표 사용, +y방향 밑  
Rasterization - 벡터좌표 screen coordinate로 변환 후 픽셀에 대응, 색 부여하는 과정  
브레젠험 알고리즘 - 정수로 화면에 선분 그리는 알고리즘, 스크린 8등분, 최초 판별식 구하기 -> 점 찍기 -> 판별식 값으로 다음 판별식 구하고 해당하는 점 찍기 반복  
선의 높이와 너비 판별식에 사용, 팔분면마다 다른 판별식  
라인 클리핑 알고리즘 - 선분을 화면 영역에 유효한 선분으로 자르는 알고리즘  
코헨-서덜랜드 라인 클리핑 - 화면을 9개로 나누고 4자리 이진 값 부여(0000 출력되는 화면), 선분 시작점과 끝 점에 각각 0000구역과 좌표 비교 후 이진 값 할당  
시작점과 끝점이 0000이면 바로 출력  bitwise and연산후 0000이 아니면 버림, 0000이면 각 점 클리핑  

## 6-1
변환 후 다시 원래 차원으로  

# 7
Dot product  
|u||v|cos(\theta), ac+bd  
직각이면 0  
행렬 내적표현, 직교행렬  
강체변환 - 물체 형태가 유지되는 변환 기저 크기1, 기저들 직교, det = 1  
벡터 방향 확인 - 같은방향 내적시 + 다른방향 -, 코사인값 이용해서 시야각 판별  
렘버트 반사 모델 - 표면 법선벡터와 광원방향 단위벡터 내적으로 cos값 구해 사용(3차원)  
Projection - v` = (uv/vv) * v, (u*v)*v (단위벡터)  

## 7-1
정면벡터 f, 물체방향 벡터 v fv내적값으로 시야 판별, 앞뒤, 시야각 내부(cos값 이용)  

## 7-2
표면 법선벡터, 광원방향 벡터 내적값([0,1]) 이용해 반사광 표현  

## 7-3
내적으로 투영벡터 구하기, 단위벡터 있으면 좋음  

# 8
convex - 영역 내 임의 두 점 연결하는 선분이 영역 내부에 속함 <-> concave    
convex combination - affine combination에서 스칼라 값 [0,1]로 제한 -> convex region  
선분, 삼각형, 삼각뿔  
mesh - 삼각형 중심 물체 관련 정보 데이터, vertex
vertex buffer - vertex 정보 배열로 저장  
index buffer - 삼각형 구성 vertex index 저장(크기 3배수)  
wireframe - 외곽선만 그려 mesh 표현  
barycentric coordinate - affine combination 스칼라 좌표각함수, radian  
회전 - 기저 변환 (1,0), (0,1) to (cos,sin), (-sin,cos)  
(x,y) -> (xcos - ysin, xsin + ycos)  
역삼각함수  
arctan - x,y인자로 받음 -> 벡터 각 계산 arctan2(y,x)사용(-pi,pi)  
극좌표계 - x = r*cos, y = r*sin 회전 효과에 이용  

## 4-1~4
HSV - 색조(Hue), 채도(Saturation), 명도(Value)의 3요소로 색 표현  
4-3에서 크기 조절 추가구현  
Scale, Rotate, Translation 순으로 적용후 렌더링(World Coordinate 기준 렌더링)  

## 4-5
polar coordinate에서 각도 변환 후 cartesian coordinate로 변환해서 렌더링, 기능 변형해서 구현  

# 5
행렬  
공간변환 행렬곱 고속처리  
선형성 - addictivity + homogeneity  
선형변환, 결합법칙 성립 이용  
공간(기저)변환  
Scale, Rotate, Sheer  
Identity, Inverse, Determinent  
행렬식 0 - 차원 축소됨, 음수 - 기저 평면 뒤집힘  
역행렬 - 역변환  

## 5-1
T R S  

## 5-2
역변환 순서 반대로  

# 6
affine space - sheer transfom 이용해 차원 하나 확장하며 translation 행렬로 계산. 마지막 차원 값 1인 공간  
affine transform  
point(z=1), displacement vector(z=0) (z - 마지막 차원)  
affine combination - affine space point를 결합해 새로운 point 생성 - aP1+bP2 (a+b=1)  
a,b값 범위 설정으로 직선(Line), 반직선(Ray), 선분, 평면 등등 표현 가능  
screen coordinate - 이산적 좌표 사용, +y방향 밑  
Rasterization - 벡터좌표 screen coordinate로 변환 후 픽셀에 대응, 색 부여하는 과정  
브레젠험 알고리즘 - 정수로 화면에 선분 그리는 알고리즘, 스크린 8등분, 최초 판별식 구하기 -> 점 찍기 -> 판별식 값으로 다음 판별식 구하고 해당하는 점 찍기 반복  
선의 높이와 너비 판별식에 사용, 팔분면마다 다른 판별식  
라인 클리핑 알고리즘 - 선분을 화면 영역에 유효한 선분으로 자르는 알고리즘  
코헨-서덜랜드 라인 클리핑 - 화면을 9개로 나누고 4자리 이진 값 부여(0000 출력되는 화면), 선분 시작점과 끝 점에 각각 0000구역과 좌표 비교 후 이진 값 할당  
시작점과 끝점이 0000이면 바로 출력  bitwise and연산후 0000이 아니면 버림, 0000이면 각 점 클리핑  

## 6-1
변환 후 다시 원래 차원으로  

# 7
Dot product  
|u||v|cos(\theta), ac+bd  
직각이면 0  
행렬 내적표현, 직교행렬  
강체변환 - 물체 형태가 유지되는 변환 기저 크기1, 기저들 직교, det = 1  
벡터 방향 확인 - 같은방향 내적시 + 다른방향 -, 코사인값 이용해서 시야각 판별  
렘버트 반사 모델 - 표면 법선벡터와 광원방향 단위벡터 내적으로 cos값 구해 사용(3차원)  
Projection - v` = (uv/vv) * v, (u*v)*v (단위벡터)  

## 7-1
정면벡터 f, 물체방향 벡터 v fv내적값으로 시야 판별, 앞뒤, 시야각 내부(cos값 이용)  

## 7-2
표면 법선벡터, 광원방향 벡터 내적값([0,1]) 이용해 반사광 표현  

## 7-3
내적으로 투영벡터 구하기, 단위벡터 있으면 좋음  

# 8
convex - 영역 내 임의 두 점 연결하는 선분이 영역 내부에 속함 <-> concave    
convex combination - affine combination에서 스칼라 값 [0,1]로 제한 -> convex region  
선분, 삼각형, 삼각뿔  
mesh - 삼각형 중심 물체 관련 정보 데이터, vertex  
vertex buffer - vertex 정보 배열로 저장  
index buffer - 삼각형 구성 vertex index 저장(크기 3배수)  
wireframe - 외곽선만 그려 mesh 표현  
barycentric coordinate - affine combination 스칼라 좌표 (s,t,1-s-t), 내적 이용해 공식 유도해 s,t값 구하기  
s,t,1-s-t값 계산해 [0,1]사이면 삼각형 내부, 아니면 외부, (u*v)^2-(u*u)(v*v)=0 인 경우 degenerate triangle(두 벡터 평행)  
texture - mesh에 이미지를 입히기 위해 변환된 데이터, 텍스쳐 매핑  
UV좌표계 - 텍스쳐를 위한 좌표계, [0,1]로 정규화 가로 U 세로 V  
정점에 UV좌표 할당, 각 픽셀 무게중심좌표로 정점 UV좌표와 선형보간해 픽셀의 UV값 계산후 텍스쳐 색상 할당  
정점에 다양한 부가데이터 할당후 사용  

## 8-1
vertex buffer, indexbuffer 사용, 물체 vertex와 index 이용해 표현  

## 8-2
삼각형 vertex에서 u,v뽑아 계산, 삼각형 lowerleft upperright 사각형 크기 범위 점들 barycentric coordinate 계산  
denominator = udotv * udotv - vdotv * udotu  
s = (wdotv * udotv - wdotu * vdotv) * invDenominator  
t = (wdotu * udotv - wdotv * udotu) * invDenominator  

## 8-3
정점 정보 활용하기  

## 8-4
정점에 UV좌표 할당, 각 픽셀 무게중심좌표로 정점 UV좌표와 선형보간해 픽셀의 UV값 계산후 텍스쳐 색상 할당  

# 9
Scene(level) - object(actor) 묶어서 관리, object는 transform가짐   
private 멤버에 주로 m_~~ or _~~로 명명  
rigid transform - M(Modeling matrix) = T*R*S 사용  
local space - object 정보를 담는 공간  
local axis - object 기준 방향 정보, local space 기저와 같음, transform에 포함, x(right), y(up), z(forward)  
world space - object를 모아 담는 공간  
object local space 정보에 modeling matrix 적용해 world space로 변환  
Resource repository - 리소스 보관, 리소스 유형별로 나눔, 리소스는 키와 데이터 가짐, object는 리소스의 키만 저장  
Workflow - 게임엔진 실행 흐름, 씬 완성, 씬으로 렌더링 ex) 리소스 로딩, 씬 구축, 게임 로직(Update), 렌더링 로직(Render)  
문자열 해싱 이용해서 해시값으로 에셋 ID 관리  
rendering pipeline - GPU내부에 설정, object 정보 GPU에 넘겨 렌더링, ex) 정점 변환, 정점 처리, 픽셀화, 픽셀 처리  
drawcall - 렌더링 파이프라인을 시작하는 함수 호출  
shader - 개발자가 설계한 로직으로 렌더링, vertex shader, fragment shader  
fragment - 삼각형 구성 픽셀  
viewport - 카메라가 출력할 화면 크기 정보  
view space - 카메라 기준으로 변환한 공간  
view matrix - world 좌표를 카메라 중심 좌표로 변환하는 행렬  
v(view) = V*M*v(local)  

## 9-1
v(view) = V*M*v(local) 이용, Lagging 효과    
