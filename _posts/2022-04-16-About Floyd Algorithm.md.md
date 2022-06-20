---
title: About Floyd Algorithm
category: algorithm
tags: graph algorithm DynamicProgramming
toc: true
toc_label: "Contents"
---

## All Pairs Shortest Path (APSP) Problem

## Floyd-Warshall algorithm(DP)

## APSP:

- problem: given any pair(u,v), find a SP from u to v
- model: on graph
- solution algo: Design → Analysis → Best algorithm?

1. brute-force, enumeration: O(n!)
2. divde and conquer
3. DP: O(n^3)

## Wrong Approach

ex) D1[1,5] ⇒ 1번 vertex 부터 5번 vertex까지 가는데 **”1개"** 의 vertex를 경유하는 경우를 계산

문제점: 고려해야하는 계산의 경우의 수가 너무나 많다!!!

## Right Approach

ex) D1[1,5] ⇒ 1번 vertex 부터 5번 vertex까지 가는데 **”1번"** vertex를 경유하거나 안하는 경우를 계산

**_Right Thinking and clever enumeration!!_**

### Recurrence Equation

Dk[i,j] = min(k를 경유하지 않는 경우, k를 경유하는 경우)

**Dk[i,j] = min(Dk-1[i,j], Dk-1[i,k] + Dk-1[k,j])**

### Procedure

Floyd(input: graph D)

```python
for k=1...

	for i=1...

		for j=1...

			Dk[i,j] = min(Dk-1[i,j], Dk-1[i,k] + Dk-1[k,j])
```

### Only single 2-D array needed for the entire caculation

When compute **kth** iteration, only needs **value from itself** and **kth row** and **kth column
(not interrupt other values)**

### How to find shortest paths between i → j?

**Use additional 2-D array P(for path)** and save the **”k”** vertex.

```cpp
void path(index q, r) {
if (P[q][r] != 0) {
	path(q, P[q][r]);
	print("v" + P[q][r]);
	path(P[q][r], r);
}
}
```

## Principle of Optimality

Which means the global structure has **Optimal SubStructure**

**_”All subsolutions of an optimal solution are optimal”_**

**_”Optimal subsolutions can build up a global(final) optimal solution”_**

If a problem A satisfies **”Principle of optimality(opt.sub)”**

—> them DP provides the best design(optimal results)

—> (not saying DP is the most efficient design)

**For example,**

A problem of **finding the longest simple path in a Graph**

has no optimal substructure.

### DP is also called Mathematical Modeling
