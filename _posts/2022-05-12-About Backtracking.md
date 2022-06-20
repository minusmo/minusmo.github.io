---
title: About Backtracking
category: algorithm
tags: DFS Backtracking graph
toc: true
toc_label: "Contents"
---

## Brute-Force in Graph?

### Can be done in for loop

But not Dynamic!

### By DFS and BFS!

Can search thorough every **State-Space-Tree nodes Dynamically!**

## Backtracking: idea and definition

### Example problems

- Maze problem
- N-Queen problem

### Idea

모든 탐색 가능한 조합을 검사하고 나열할 필요가 있을까?

**No! → 이미 탐색할 필요가 없는/탐색 불가능한 조합이 있기 때문!**

### Definition

1. **DFS** of a tree **except that nodes are visited**
2. Backtrack if **Non-Promising: Pruning**

**_Formal Definition_**

Do a DFS of a state-space tree, checking whether each node is promising, and

if it is not promising, backtracking to the node’s parent.

## Key-points in Design and Analysis

### Design Key: Promising function의 설계

### Analysis Key:

- Optimality: 답이 있으면 반드시 정답을 찾는다! → trivial
- Time Complexity: exponential(NOT poly. time) → BF Complexity
- 중요성: empirical test, 실험적 성능(execution/runtime)

### Q. 자식 노드를 방문하기 전에 check/계산 가능한가?

또는 직접 방문 후 check/계산 해야 하는가?

→ **구현의 issue, 개발자의 몫!**

### Problems in Backtracking: Difficult problems in CS

### Sum of subsets problem(Subset sum problem)

: a special case of 0/1 Knapsack problem.

Given a set of items with weight and fixed total Weight,
find a subset whose sum equals total Weight.

### 응용, 적용 기술: 게임서버 load balancing task team

→ 여러개의 서버에 사용자의 사용률에 맞게 배분하는 방법!

### Backtracking for SubSet Problem

Design Steps

1. promising function 설계
2. DFS traverse/visit

### Promising function: 수학적 표현 ⇒ True or False

1. i-th level: weight + weight(i+1) > W
2. weight + 미래 총 weight 합 < W

### Analysis

1. optimal solution generated
2. execution time: timer로 측정. depending on promising function
3. 실제 생성된 node 수: **_performance gain_**
   생성된 leaf nodes 수 / 전체 leaf node 수 로 계산

## Questions

앞선 예제 에제는 items → sorted

what if,

1. items are sorted in reverse
2. items are listed random

정렬은 전처리로 처리될 수 있다.
→ 전처리가 시간이 다소 걸리더라도 진행하고 backtracking을 수행하는 것이 좋은가?

## Other Problems

### Graph Coloring problem

**applications:** 강의실 무선 마이크, 무선 네트워크(귀한 자원)

how to find minimum **’m’**? → No(efficient poly. alg X)

Given m, m-colorable? → Yes. ⇒ Backtracking

### Hamiltonian Circuits problem

AKA, 한 붓 그리기

Def: Given a connected, undirected graph, H.C. is a path that starts at a given vertex,

visits each vertex exactly once, and ends at the starting vertex.
