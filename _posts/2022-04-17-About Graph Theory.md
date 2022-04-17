---
layout: posts
title: About Graph Theory
category: algorithm
tags: graph algorithm theory
---

## 알고리즘 디자인의 과정(솔루션을 도출하는 과정)

1. 자연어로 기술된 문제를 접한다.
2. CS를 활용하여 적절하게 모델링한다.
3. CS 알고리즘 사고를 통하여 솔루션을 디자인한다.

---

### 1. Problem: described in natural language

### 2. MODEL: clear, easy to understand, communicate

→ mathematical expressions  
→ graph model  
→ probability/stat model(네트워크 전공 연구원)  
→ linear algebra model(인공지능)  
→ convex optimization model(최적화, 2차함수, 수치해석)  
→ graph model in various applications  
: shortest path, network information flow analysis,
social network services(SNSs), state diagram...  
→ step-by-step procedure(순서도, flow charts)

모든 문제를 graph로 표현/모델링하고 답을 찾는다.

**Graph Theory**!!

---

Following content is a personal lecture note taken in **Mathematics for CS in MIT**

---

## Graph Theory and Coloring

**Graph Coloring** Problem:
given a graph G and K colors, assign a color to each node so adjacent nodes get different colors.

**Def:** The minimum value of k for which such a coloring exists is the \_\_Chromatic Number(Kai) of G

### Basic Coloring Alg for G=(V,E)

1. order the nodes v1, v2, ... vn
2. order the colors c1, c2, ...
3. for i=1, 2, ... n
   Assign the lowest legal color to v

### Theorem: If every node in G has degree ≤ d, the Basic Alg uses at most d+1 colors for G.
