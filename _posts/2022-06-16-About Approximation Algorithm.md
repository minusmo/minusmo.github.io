---
layout: posts
title: About Approximation Algorithm
category: algorithm
tags: ProblemClassification computation NP Approximation
---

updated at 2022-06-17

Approximation Algorithm은 이론적 증거를 바탕으로 NP-C, NP-H 문제에 대해서 적용할 수 있다.

# Approximation Algorithm의 특성

근사치를 계산하는 알고리즘의 개발은 쉽다.(suboptimal solution)

## 그렇다면 얼마나 optimal solution에 가까운가? 를 제시.

1. mathematically: bound theorem
2. empirically: accuracy, relavancy

## 또한 얼마나 빠른가(효율적인가)? 를 제시.

1. mathematically: Time Complexity. T(n) = polynomial
2. emprically: execution time, running time(in seconds)

### Approximation algorithm의 개발 접근법

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

# Approximation의 예시들

TSP, Bin Packing problem

## TSP

MST를 이용하여 TSP를 해결.

MST의 특성

- short edge를 연결
- no cycle

MST로 연결된 구조는 round-trip route/path를 구성하는데 용이.

**Approximation Design**

1. determine a MST(Using Prim’s Algorithm): ranking func.
2. create a path around the MST(Using preorder visit)

**Approximation Analysis**

1. Time Complexity: O(n^2)
2. Boundness(theorem, proof): approx sol < optimal sol(관계성)

cost(mst.path) < cost(opt.path)

cost(full walk on MST) = 2 \* cost(mst.path)

cost(full walk on MST) < 2 \* cost(mst.path)

→ cost(opt.path) < cost(full walk on MST)(by triangular inequality)

⇒ cost(opt.path) < 2 \* cost(opt) proof!

## Bin Packing problem

- Bin Packing problem: NP-Hard
- unit-size의 가방을 최소한으로 하여 주어진 아이템들을 모두 가방에 담는 문제!

Applications: 이삿짐, 여행가방, 인테리어 레이아웃(방에 가구 배치), 게임서버 load balance issue

if “Bin packing problem을 해결하라"는 문제가 주어진다면?

1. 문제의 problem-level(class) classification → 난이도 파악
2. NP-C ⇒p Bin packing ?

**Approximation Design(Non-increasing, First-fit: NFF)**

1. sort the items in non-increasing order(greedy, ranking)
2. pack into as close bin as possible

**Approximation Analysis**

1. Time Complexity: T(n) = O(nlogn)
2. bound Theorem(Quality)
   → “approximate bin < optimal bin \* 1.5”(theorem)
   → “any items placed by NFF in an extra bin has size ≤ 1/3”(lemma)
