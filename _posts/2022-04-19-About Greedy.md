---
title: About Greedy
category: algorithm
tags: graph algorithm greedy
toc: true
toc_label: "Contents"
---

**_DP gives optimal solution but not practical in fields_**

## Sprit of Greedy Algorithm

알고리즘을 디자인 하는 사람마다 그리디 설계는 달라질 수 있다.

실생활의 문제들은 대부분 최적화 문제들이다.

만약 우리가 **”local optimal”** —> **”global optimal” 이라고 가정한다면
그리디 알고리즘을 적용해 볼 수 있다.**

---

## Greedy Algorithm

Grabs data items in sequence, each time with **BEST choice  
thinking future.**

→ Best choice: local optimal choice(O), global choice(X)

→ in terms of my viewpoint(intuition, heuristics 경험)

### Good example of Greedy alg

→ MST(Minimum Spanning Tree)

### Applications of MST

smartphone(IC chip), KTX railway, Network 망사업자,

→ 많은 문제들의 모델링을 할 수 있다.

## Design steps of Greedy Algorithm

### Ranking function

### <Design>

```cpp
while NOT solved yet {
step1. Selection(local optimal choice, by ranking)
step2. Feasibility check(constraint, optimal)
step3. Solution check(termination)
}
```

### Example with MST

Greedy_MST(input: graph G=(V,E))

```cpp
F = empty set
while NOT solved yet {
select an edge e(local optima choice) -> ranking(scoring) function
if e creates No cycle then add e to F
if T=(V,E) is a Spanning Tree, then stop/exit
}
```

→ output: MST T=(V,E), F is subset of E

→ how to select e? makes difference in Prim’s and Kruskal’s Algorithm.

---

## Prim’s Algorithm: node(vertex)-based approach

```cpp
F = empty set
Y = {v1}
while NOT solved yet {
	select v in V - Y nearest to Y // selection
	feasibility test(cycle?) // Prim's alg에서는 불필요. 알고리즘 원리상 cycle이 생길 수 없음.
	add v to Y
if V === Y, then stop/exit
}
```

### <Analysis>

1. Time Complexity T(n) → T(#vertex) = T(|V|) = T(n) ⇒ O(n(n-1)) = O(n^2)
2. Proof required.(반드시 증명되어야 하는 것은 아니다.)

## Proof of Greedy Algorithms

- **Induction: 과정 유도**
- **Proof by Contradiction: 주장을 부정하고 이것이 틀림을 증명하는 것!**

---

## Kruskal’s Algorithm: edge-based approach

```cpp
Given a graph G=(V,E)

sort Edge set 'E': my ranking/scoring function
while NOT solved yet {
	select next edge 'e' from sorted list
	if cycle check: YES -> remove/pass else add 'e'
	if stop condition: YES -> stop else repeat
}
```

### How to check ‘cycle’ in Kruskal’s ?

- set of trees: **Forest** data structure
- two key operations in **Forest**: find and union
- **find**: root finding in a tree
- **union**: connect two roots

—> find each root of i and j

—> see/check if the two roots are the same

—> if YES, cycle O, else cycle X and add ‘e’ then repeat.

```cpp
Cycle check
e = next edge(u,v)
p = find(u)
q = find(v)
if p != q --> connect/merge -> connect/merge(add e to F)
```

### Pseudo code of Kruskal’s

```cpp
Given a graph G=(V,E)

F = empty set
create 'n' disjoint sets: {v1}, {v2}... {vn}
sort Edge set 'E'
while NOT solved yet {
	select next edge 'e' from sorted list
	if cycle check: YES -> remove/pass
	else connects two subsets, then merge them merge them and e to F
	if stop condition: YES -> stop else repeat
}
```

### <Analysis>

|V| = n, |E| = m

1. init: theta(n)
2. sort: depending on the specific alg: O(mlogm)
3. while loop: O(m\*alpha(n,m)) → O(mlogn)
   : find-union operations → 연구를 거쳐 **”알파 타임"이라 부른다.**
4. remaining operations

After all, O(mlogm) dominates all.

T(n,m) = O(mlogm)

number of edges: n-1≤m≤n(n-1)/2

### Proof of Kruskal’s

similar to Prim’s.

---

## Prim’s vs Kruskal’s

기본 골자는 **O(n^2) vs O(mlogm)이지만,**

적절한 자료구조와 적절한 정렬 알고리즘을 통해

프림 알고리즘의 시간 복잡도를 충분히 개선할 수 있다.

이는 **_CS의 주요 연구 골자_** 이다!
