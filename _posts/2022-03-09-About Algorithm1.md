---
layout: posts
title: About Algorithm1
category: algorithm
tags: ps algorithm
---

# 알고리즘 이란

주어진 문제에 대한 **_“Approach and Strategy”_**

# 알고리즘을 배우면서 알아야 할 것

1. Design of Algorithms: multiple
   하나의 문제를 푸는 알고리즘은 복수개가 존재한다. 그 중 가장 효율적인 것을 사용!
2. Analysis of Algorithms: 알고리즘의 분석 기준은 “효율성”
   왜 어떤 알고리즘이 더 나은가? 최고인가?

# Design and Analysis

## Problem: 정답을 찾아야 하는 질문

단순 정답이 아닌 **Solution** 을 찾는다!

### Problem → Model → Solution

### 실제 생활에서 발생하는 컴퓨터 과학의 문제에 대한 풀이 = 알고리즘

: Step by Step procedure(Procedural steps)를 통한 풀이

절차적 사고를 통한 풀이가 필요하다!

### 어떤 알고리즘이 효율적인가에 대한 답은 수학적으로 제시되어야 한다.

# Time Complexity

## 알고리즘의 기준은 무엇인가?

- 동의할 수 있는 기준이 필요
- 이론적 속도가 기준: O(n), O(n^2)
- Time Complexity Analysis

### Time Complexity Analysis

1. 입력 크기를 결정: n
2. BO(Basic Operation)s 를 선택
3. 얼마나 많은 BO가 실행되었는지를 결정

### Large scale 문제일 수록 중요!

## O notations and Upperbound

이론적으로, 큰 n값에 대해서 제곱항이 나머지를 압도한다.

### Big O 의 정의

O(Upperbound)

- g(n) ≤ O(f(n))
  if c, N ≥ 0 s.t for n ≥ N, g(n) ≤ c\*f(n)
  f-function: asymptotic upperbound

O(function) = upperbound

sw/alg → _”at least as good as”_

→ worst-case time complexity를 본다!
