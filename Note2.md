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



