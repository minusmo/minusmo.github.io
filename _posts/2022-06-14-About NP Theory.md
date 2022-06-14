---
layout: posts
title: About NP Theory
category: algorithm
tags: ProblemClassification theory computation
---

ex) 30PB 크기의 데이터는 _Computationally Prohibited_ 된다.

문제를 푸는 과정(보통의, 고전적 문제들에 대해)

1. 효율적인 알고리즘을 디자인한다.(정확한, 최적의 솔루션을 위해)
2. 분석: 시간 복잡도, 증명, 하한.

**만약 효율적인 알고리즘을 찾지 못한다면?**

1. 최적의 솔루션을 찾기 위한 아주 느린 알고리즘을 사용한다.
2. 최적의 솔루션을 포기하고, _근사치 솔루션_ 을 채택한다.
   (sub-optimal, near-optimal solutions)
3. Massive 병렬화: super com, Gpus, 분산처리
   → NEW Design: parallel algorithms

### Problems의 범주

P < NP < EXP < Solvable < Countable < Unsolvable

⇒ Problem Classification

## Problem Classification

**문제의 난이도를 확인해야 더 적합한 디자인 및 분석을 할 수 있다!!!
→ 여러가지 과정(교수자 및 교과서)에서 다양한 이론과 이해를 제시하고 있다.**

### Easy problem vs intractable problem

1. easy problem: good algorithm exist, polynomial T.C.
2. intractable problem: difficult to treat or work
   (no-polynomial time algorithm)

### P-class Definition

1. the class of decision problems that are polynomially bounded
2. T(n) = polynomial function of ‘n’
3. problems solvable in poynomial time.

### Exp-class

problems solvable in exponential time.

## 3 categories of problem classification

**1. Problems proven to be in p-class:** sort, search, CMM, SP, Dijkstra
→ easy, efficient, fast, optimal, treatable

**2. Problems proven to be NOT in p-class:
→”a few”, “intractable”
→ solvable in time like O(n!)
→ no-polynomial amount of output**

### “halting problem”

given a computer program(algorithm), does it stop/halt? y/n

p-class의 문제가 아닌 것이 증명되었다.

it’s famous because it wat the first problem proven to be _uncomputable/undecidable_

**3. Problems proven “neither” to be in P nor “nor” to be intractable
→ neither 1 nor 2: knapsack, graph coloring, TSP, subset sum…**

### 최적화 문제와 결정 문제

최적화 문제는 주어진 문제 상황에 대한 최적의 해답을 찾는 것!

결정 문제는 주어진 해답에 대해 그 해답이 맞는지를 Y or N로 대답하는 것!

예) KS problem

최적화 문제: 주어진 set에 대하여 최대의 이익을 찾는 것
결정 문제: 주어진 set에 대하여 이익이 100보다 큰 subset이 있는가? → Y or N

예) Clique problem

Clique: complete subgraph → bioinformatics, SNS

최적화 문제: 주어진 graph에 대하여 최대의 clique를 찾는 것!
결정 문제: 주어진 graph에 대하여 적어도 ‘size k’ 보다 큰 clique가 존재하는가? → Y or N

Q: KS은 NP인가?
아니다. 최적화 문제는, polynomial time 안에 모든 조합을 비교하여 최적의 해답을 도출할 수 없으므로 NP 문제가 아니다. 2^n개의 조합 비교 필요!!(결정 문제가 아니기 때문)

**Polynomial-time verification**

결정 문제를 해결하기는 어렵지만, 주어진 해답에 대해 검증하는 것은 쉽다!
KS 결정 문제는 p-time 안에 검증할 수 있다.
→ A = {i1, i2, i3, …} > 500 ? Y or N in O(n) time.

### NP의 정의

1. “A magic algorithm”을 통해 p-time 안에 해결할 수 있는 결정 문제.
2. 해답이 주어졌을 때, p-time 안에 검증할 수 있는 결정 문제.

### determine vs stochastic(random, probabilistic)

nondeterministic: automata

### Nondeterministic Algorithm/machine

1. Nondeterminisitc guess
   given a problem instance, guess a correct solution in unit time if exists(without trying all options)
2. Deterministic verification
   verifiy the guessed solution

### NP의 정의(in nondeterministic context)

1. set of all problems solvable by Poly-time Non-deterministic Algorithm.
2. solvable in Poly-time by Non-deterministic Algorithm.

\*\*Poly.time Non-deterministic Algorithm
→ Non-deterministic Alg. such that verification in Poly.time.

P == NP ? _probably no_

P is a subset of NP ? _Yes_
