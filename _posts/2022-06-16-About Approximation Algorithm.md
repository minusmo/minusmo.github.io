---
layout: posts
title: About NP Complete
category: algorithm
tags: ProblemClassification computation NP Approximation
---

Approximation Algorithm은 이론적 증거를 바탕으로 NP-C, NP-H 문제에 대해서 적용할 수 있다.

## Approximation Algorithm의 특성

근사치를 계산하는 알고리즘의 개발은 쉽다.(suboptimal solution)

### 그렇다면 얼마나 optimal solution에 가까운가? 를 제시.

1. mathematically: bound theorem
2. empirically: accuracy, relavancy

### 또한 얼마나 빠른가(효율적인가)? 를 제시.

1. mathematically: Time Complexity. T(n) = polynomial
2. emprically: execution time, running time(in seconds)

## Approximation algorithm의 개발 접근법

대부분 휴리스틱(그리디) 접근을 사용한다.

기존의 그리디 알고리즘과 근사치 계산의 그리디는 다르다!

- 기존의 그리디: 로컬 옵티마가 글로벌 옵티마로 간다는 것이 증명됨!
- 근사치의 그리디: 위의 증명을 기반으로 사용하는 것이 아니라 글로벌 옵티마를 구하기 어려우므로 사용하는 것!

### Boundness

p-time안에 optimal을 계산하기 어렵다. ⇒ Approximation!

optimal solution과의 관계를 수학적으로 표현한다.
ex) approximation solution < optimal \* 2

Theorem을 통해 bound를 제시할 수 있으면 좋다.
더 좋은 bound 일 수록 더 좋다!
