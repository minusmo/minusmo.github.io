---
layout: posts
title: About KnapSack problem
category: algorithm
tags: greedy DynamicProgramming
---

## Why Greedy algorithm important?

1. natural, simple, fast/easy implemetation: **heuristic idea**
2. Test-bed: baseline performance 제공 <기준점>

- 우리가 새로운 문제들을 접할 때 연구자들이 가장 먼저 접근하는 설계 전략
- 정밀도/정확도 accuracy 향상, 속도 증가, model size 감소

3. maybe “optimal”: **optimal substructure**

- local optimal —> global optimal: proof required

## Constraint Optimization Problem

**Constrained Combinational Optimization Problem**

S = {item1, item2, ..., itemn} //문제 구성요소, object

w_i = {weight1, weight2, ..., weightn}

p_i = {profit1, profit2, ..., profitn}

W = sack size(limited)

⇒ Find A(a subset of S) such that

1. maximizes the **_profits_** in A
2. sum of the weights in A ≤ W

알고싶은 것은 **_maximum profit_**!!!

### 0/1 Knapsack problem

To solve the knapsack problem

1. BF: 2^n enumeration
2. D&C: optimal을 찾을 수 있는가? optimal but inefficient?
3. DP: 가장 적절!!
4. Greedy: Only **fractional knapsack problem(남은 sack에 item을 나누어서 일부만 담을 수 있는 경우)** 에서만 **optimal solution** 을 제공한다!!

### Design: recurrence equation(recursive property)

1. 1-D Array enough? X. information about **W, weight** required!
2. 2-D Array is required! then...

p[i,w] = max 1) p[i-1,w] 2) p[i-1,w] + p_i

Okay with this? ⇒ N.

**Proper and Delicate thinking is required**

p[i,w] = max 1) p[i-1,w] → item_i is not selected 2) **p[i-1,w-w_i]** + p_i → item_i is selected

\*Trick of DP: index from 0.
직전정보가 필요하기 때문!!

### Analysis

Time Complexity

T(n,W) = theta(1)_nw //TC for each subproblem _ #subproblem

→ T(n,W) = O(nW), specifically theta(nW)

→ if W is huge(real number) ⇒ terrible performance

→ polynomial time complexity: depends on input size ‘n’

→ W value: depends on numeric value of input W

→ pseudo polynomial time complexity

To improve this, came up with an idea,

do not need to compute all elements in p[i,w]

⇒ DP optimization(implementation)

Final TC: min{O(nW), O(2^n)}

### Why this problem happened?

문제의 난이도가 다르기 때문!!

knapsack problem은 매우 어려운 문제이다. >> sort, search, cmm

### So what?

We need **new approach**!!!
→ backtracking, branch and bound
