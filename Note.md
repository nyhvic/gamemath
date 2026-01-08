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