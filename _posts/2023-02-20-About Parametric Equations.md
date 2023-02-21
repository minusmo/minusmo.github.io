---
title: About Parametric Equations
category: ComputerGraphics
tags: VectorGrahpics Mathematics
toc: true
toc_label: "Contents"
---

# Introduction

수학에서, 파라메트릭 방정식은 어떤 량(값, 측정치 등)들의 그룹을 "매개 변수"라고 불리는 하나 이상의 독립적인 변수의 함수로 정의합니다.
파라메트릭 방정식은 일반적으로 [곡선이나](https://en.wikipedia.org/wiki/Curve "곡선") [표면과](https://en.wikipedia.org/wiki/Surface_(mathematics) "표면 (수학)") 같은 기하학적 물체를 구성하는 점의 [좌표를](https://en.wikipedia.org/wiki/Coordinates "좌표") 표현하는 데 사용되며, 이 경우 방정식은 집합적으로 **파라메트릭 표현**, 또는 객체의 **매개 변수화**라고 불립니다.

예를 들면, x = cost, y = sint와 같은 단위원의 파라메트릭 표현이 있을 수 있습니다.
여기서 t가 매개변수 입니다.
이런 파라메트릭 표현은 일반적으로 고유하지 않습니다. 따라서 동일한 양이 여러가지 다른 표현으로 나타내어질 수 있습니다.
보통 파라메트릭 방정식은, 물체의 궤적이 매개 변수로 시간에 따라 방정식으로 표현되는 "운동학"에서 사용됩니다.

# 응용
- 물리
	- 운동학
- CAD(컴퓨터 지원 설계)
	- Implicit
	- Explicit
	- Parametric
- Integer Geometry

## Kinematics(운동학)
운동학에서, 물체의 궤적은 종종 매개변수 곡선으로 묘사됩니다. 각각의 공간 좌표는 독립변수(주로 시간)에 의존합니다.  이런 방식으로 사용되었을 때, 매개변수 방정식의 세트는 좌표에 대한 벡터 함수를 형성합니다. 이런 매개 변수 곡선은 각 항별로 미/적분 될 수 있습니다. 

에를 들면,
r(t) = (x(t), y(t), z(t)) 로 표현된 매개변수 좌표함수는,
v(t) = dr(t)/dt = (dx(t)/dt, dy(t)/dt, dz(t)/dt) 가 될 수 있습니다.

## CAD(Computer-Aided Design)
CAD에서, 매개 변수 함수는 평면 곡선을 묘사하는 데 주로 사용됩니다.

| 종류     | 형태 | 예시 | 모양 | 
| -------- | ----- | ----- | ----- |
| 명시적 | y = f(x) | y = mx + b | 선 |
| 암시적     |  f(x,y) = 0 | (x-a)^2 + (y-b)^2 = r^2 | 원 |
| 매개 변수적 | x = g(t)/w(t), y = h(t)/w(t) | x = a + rcost, y = b + rsint | 원 |

각각의 표현은 장단점이 있습니다.
명시적 표현은 매우 복잡할 수 있고, 아예 존재하지 않을 수도 있습닏. 더욱이, 기하학적 변환에서 제대로 동작하지 않을 수 있습니다(특히 회전에서)
다른 한 편으로는, 매개 변수 방정식과 암시적 방정식은 명시적 표현으로부터 쉽게 추정될 수 있고, 단순한 명시적 표현이 존재할 때는, 두 표현 모두 장점이 있습니다.

암시적 표현으로는 곡선위의 점을 생성하기는 어렵지만, 주어진 점이 곡선위에 있는지나 곡선 안,밖에 있는지 판별하는 것은 쉽습니다.

매개변수적 표현으로는 암시적 표현같은 판단은 어렵지만, 곡선위의 점을 생성하고, 곡선을 그리는 데는 가장 잘 맞습니다.
# 암시화
라는 것은, 매개변수화된 방정식의 세트를, 단일한 암시적인 방정식으로 변환하는 것을 의미합니다. 이것은 결국 매개변수를 "제거"하는 것을 의미합니다.

예를 들어,
x = acost, y = bsint 인 매개변수적 표현을,
cost^2 + sint^2 = 1 의 관계를 이용하면,
x^2 + y^2 = a^2 의 명시적 표현을 얻을 수 있습니다.


# 2차원의 예시
- 포물선
- 원
- 타원
- 리사주 곡선
	- 리사주 곡선은, 타원과 비슷하지만, x와 y의 위상이 동일하지 않습니다.
	- [![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Lissajous_curve_3by2.svg/220px-Lissajous_curve_3by2.svg.png)](https://en.wikipedia.org/wiki/File:Lissajous_curve_3by2.svg)
- 쌍곡선
- 하이포트로코이드
	- 한 원에 내접하는 원에 부착된 한 점이 내접하는 원이 다른 원 둘레를 따라 회전할 때 생기는 곡선입니다.
	- [![A hypotrochoid for which r = d](https://upload.wikimedia.org/wikipedia/commons/thumb/1/12/2-circles_hypotrochoid.gif/120px-2-circles_hypotrochoid.gif)](https://en.wikipedia.org/wiki/File:2-circles_hypotrochoid.gif "A hypotrochoid for which r = d")
- 이외의 다양하고 복잡한 함수들
- [![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f5/Param_02.jpg/180px-Param_02.jpg)](https://en.wikipedia.org/wiki/File:Param_02.jpg)
## 3차원의 예시
- 나선
	- 나선은 고차원 공간에서 곡선을 묘사하기에 편리합니다.
	  예를 들어, x = acost, y = bcost, z = bt와 같은 방법으로 3차원 곡선을 묘사할 수 있습니다.
- 파라메트릭 표면
	- 토러스와 같은 3차원 도형은 매개변수 표현을 이용해 묘사될 수 있습니다.
	  x = cost(R+rcosu), y = sint(R+rcosu),z=rsinu와 같은 표현은 다음과 같은 토러스를 표현합니다.
	  [![R = 2, r = 1/2](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Torus.png/120px-Torus.png)](https://en.wikipedia.org/wiki/File:Torus.png "R = 2, r = 1/2")


https://en.wikipedia.org/wiki/Parametric_equation