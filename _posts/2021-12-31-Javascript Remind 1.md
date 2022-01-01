---
layout: posts
title: Javascript Remind 1
category: programming language
tags: javascript
---

**Javascript The Definitive Guide - David Flanagan** 중

여기서는 위 서적에서 발견한 몇가지의  
**내가 몰랐던, 꼭 알아야할, 혹은 알면 좋을**,  
혹은 사소한 것들을 정리한다.  

## 2.5.1 Unicode Escape Sequences  
javascript의 문자열은 유니코드(UTF-16) 문자의 집합이다.  
자바스크립트 컴파일러는 유니코드 문자열을 변수이름으로 사용하는 것을 허용한다.  
같은 유니코드 문자를 2개 이상의 unicode escape sequence로 표현하는 경우도 있다.  
이 경우, 표현법만 다르고 의미하는 유니코드 문자는 같으므로 같은 변수를 가리킨다.  

### 하지만,

유니코드와 아스키코드를 섞어서 유니코드 문자를 표현하는 경우는,  
유니코드만 사용해서 변수를 선언했을 때와는 binary encoding이 다르므로 다른 변수를 가리킨다.  

## 3.1 Overview and Definitions  
자바스크립트는 원시타입과 객체타입으로 크게 나뉜다. 

## 3.2 Numbers  
javascript의 Number 자료형은 정수와 실수(근사)를 표현한다.  
자바스크립트는 64-bit 부동소수점 표현방식으로, IEEE 754 standard에 정의되어 있다.  
이는 실수 표현 범위가 최대 +-1.7976931348623157 * 10 ** 308,  
최소 +-5 * 10 ** -324  
까지 임을 의미한다.  
  
자바스크립트는 정확히 +-9,007,199,254,740,992(+-2 ** 53) 범위의 정수를 표현할 수 있다.  
표현범위를 넘어가면 오버플로우나 언더플로우가 발생한다. 

## 3.2.3 Arithmetic in Javascript  
ES6에서 추가된 유용한 Math 객체의 메소드들.
- Math.cbrt(27) => 3: cube root
- Math.hypot(3, 4) => 5: square root of sum of squares of all arguments  
- Math.log1p(x): natural log of (1+x); accurate for very small x  
- Math.sign(x): -1, 0, 1 for arguments <, ==, > 0  
- Math.imul(2, 3) => 6: optimized multiplication of 32-bit integer  
- Math.trunc(3.9) => 3: convert to an integer by truncating fractional part  
- Math.fround(x): round to nearest 32-bit float number  
  
javascript 산술 연산은 오버플로우, 언더플로우, 0으로 나누는 연산에서 에러를 일으키기 않는다.  
대신, 
```javascript
Infinity, -Infinity in case of overflow  
0, -0 in case of underflow  
NaN in case of 0/0  
```
와 같은 특별한 값들이 존재한다.  

ES6에서 추가된 유용한 Number 객체의 메소드 및 프로퍼티들.  
- Number.parseInt()
- Number.parseFloat()  
- Number.isNaN()  
- Number.isInteger()  
- Number.isSafeInteger()
- Number.EPSILON: javascript 실수간의 가장작은 차이  

0과 -0은 **분모로 사용되었을 때**를 제외하고는 차이가 없다.  
