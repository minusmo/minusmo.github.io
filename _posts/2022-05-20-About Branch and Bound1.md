---
title: About Branch and Bround
category: algorithm
tags: BFS BranchAndBound
toc: true
toc_label: "Contents"
---

## Promising function = Bound function

## Knapsack problem

### Observation

Knapsack problem에서는, 탐색할 state가 **_promising or not_** 에 대한 기준점이 탐색을 거듭하면서 바뀐다!

**promising의 기준**: **_Best Profit_**

### Bound function = g + h

- g = **지금까지의 Profit**
- h = **남은 아이템 이익의 최대 추정치(예측치)**

**If bound function = g+ h < Best Profit**

**_Non Promising!_**

### h function

h stands for **_heuristic_**

bound function의 설계자에 따라 달라진다!

## Questions

### estimator h는 큰 값을 예측하도록 설계하는 것이 좋은가?

- pruning power가 증가되는가?
- 한편으로는, _incorrect pruning_ 이 발생하지 않는가?

→ 중요한 문제!

bound function design이 잘될 수록 **performance gain이 커진다!!**

## Design of Backtracking Algorithm

- N-Queens, subset sum problems: _Non-optimization_ problem(Y/N)
- 0/1 KS problem: _Optimization_ problem
  → compare promising fn/bounding fn/evalutaion fn = g(exact) + h(estimate)
  → non-promising if < Best evaluation

### Maximization Optimization Problem

e.g) 0/1 KS

**upper bound estimation at each node**!

### Minimization Optimization Problem

e.g) TSP

**lower bound estimation at each node**!

## Backtracking vs Brand&Bound

### Difference?

**_DFS or BFS_**!!!

in practice, B&B is far better than Backtracking!

**_Why?_**

BFS is **reliable**!

tree traverse order에 따라 Best evaluation이 업데이트되는 순서가 다르다!!

**\*\*** 미래 estimate(**’h-value’**)가 좋으면(정확한 예측이 가능하다면),
BFS로 진행하는 것이 좋다 → start root 근처 pruning이 일찍 발생할 수 있다!

**\*\*** Backtracking은 탐색을 진행할 수록, **’g-value’**가 빨리 갱신되고,
**’h-value’**에 대한 불확실성이 빠르게 줄어든다!

### Key-point

향후 h-value 설계/추정/수식유도 등에 경험을 통해 자신감이 향상되면, B&B가 우월하다.

아니라면, Backtracking이 좋을 것!

## B&B: Best-First

**Improved Standard B&B**

- idea: based on the visit order of children nodes
- BFS, DFS has fixed traverse order
- observe that the bound function updating
- _change the visit order during the algorithm run!_

Best evaluation이 계산된 state부터 탐색!
→ use appropriate data structure(e.g priority queue)

### application

- A\* algorithm in AI

### Questions

- If promising/bound value가 다른값이 배정되면?
- Best-first B&B: + greedy approach(local optima choice)
  **_”Optimal solution이 확실한가?”_** → 증명 필요.
  기존 방법들은 all enumeration이 가능.

## Advanced Topic

how to define h function?

h: mathematical expression for estimation/prediction

**Guideline for h function**

h-value의 range를 설정하며 범위를 좁혀간다.

1. 0 < h < infinity
2. h*: global optimal value → h와 h*의 관계성 유추
   h > h\* : overestimate(max opt problem)

overestimate하면 실수하지 않는다.(miss pruning)

- optimal로 진행가능한 가지를 pruning out하지 않음
- 보수적, 안정적인 pruning
- pruning되는 subtree 가지의 수는 적을 수 있음. e.g) 0/1 KS
- h는 h*보다 큰 값 중에서 가장 작은 값이 좋다. → Pruning Power matters!
  h = h* + alpha(small value)
