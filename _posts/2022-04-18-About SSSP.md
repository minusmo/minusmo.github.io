---
title: About SSSP
category: algorithm
tags: graph algorithm DynamicProgramming greedy
toc: true
toc_label: "Contents"
---

# Single Source Shortest Path Problem(SSSP)

given a Graph G=(V,E) and Starting vertex S,

find Shortest Path from S to v in V(set of vertices)

1. Problem: find a SP from A to B
2. MODEL: a weighted graph G=(V,E)
   function f: E(sequence of edges) → R
   find the minimum R(total cost = min weight)
3. Solution Algs:
   Dijkstra alg(non-negative edge weight)
   Bellman-Ford alg(negative edges)

---

### Negative edge가 있는 경우,

negative edge cycle이 있을 수 있다. 이런 경우는 최단 경로를 찾지 못한다.

그래서 만약 negative edge가 있다면 , 알고리즘이 negative weight cycle을 찾아서

detect/report 해야한다.

---

## Dijkstra Alg.

No negative weight edge SSSP.

From a starting vertex S → find SSSP.

**Idea**:
repeatedly select u in v-s(vertices set) with minimum SP, add u to S, **relax** all edges out of u.

**Extract min** —> design DP(X), Greedy(O)

Time complexity: O(n^2), |V|=n → O(v^2)
—> could be better using Heap(beyond scope)

---

## Bellman-Ford Alg.

Negative cycle problem → detect and report\*\*\*
SP is indeterminant!!

---

## Dijktra and Bellman-Ford

### idea:

- Dijkstra: find the closest v from S → relax → ...
- B-F: simple relax all edges for |V|-1 time
  Adj matrix updated repeatedly

### 구현 난이도:

B-F(easy) >> Dijkstra

### Time complexity:

B-F O(VE) < Dijkstra O(n^2=V^2)

|E| = n(n-1)/2 → O(VE) = O(n^3)

### Negative weight cycle:

B-F(O), Dijkstra(X)

### Design perspective:

- Djikstra: **Greedy** design
- Bellman-Ford: **DP** design
  subproblem: SP v→t, update edge 1개, 2개, 3개...

---

## MIT Lec 15 lecture note

G(V,E,W) W,E → R

V: vertices

E: edges

W: weights

![SSSP0](/assets/images/sssp0.png)

![SSSP1](/assets/images/sssp1.png)

![SSSP2](/assets/images/sssp2.png)

![SSSP3](/assets/images/sssp3.png)
