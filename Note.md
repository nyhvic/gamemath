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
