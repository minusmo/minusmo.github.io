---
layout: posts
title: About NP Complete
category: algorithm
tags: ProblemClassification theory computation NP
---

CS에서 대부분의 중요한 문제는 NP에 속해있다.

너무나 많은 문제들이 P class의 문제라고 증명될 수 없다.

이러한 문제들 중 단 하나라도 P 문제라고 증명할 수 있다면, 다른 모든 문제들도 P에 속한다고 할 수 있다.

NP 문제들 중 가장 대표적, 어려운, core, 완전한 문제는 무엇인가?
→ “NP-Complete” 클래스
→ NP-Complete 문제들 중에 단 하나라도 Polynomial time에 풀 수 있다면, 다른 모든 문제들도 그렇다.

## NP-Complete의 정의

### Problem B is NP-Complete if

1. B is NP and
2. for all A in NP, A can be transformed, reduced to B

### Problem C is NP-Complete if

1. C is NP and
2. for B which is NP-Complete, B can be transformed, reduced to C

## Cook’s theorem(1971)

“If CNF is P, then P == NP”, “CNF Problem is NP-Complete”라고 증명된 최초의 문제!

_CNF problem: Satisfactory(also called Boolean SAT) Problem_

**Conjunctive Normal Form of CNF Problem**

ex) (x or y) and (y or not z) and not y = F(boolean expression)

CNF Problem in Decision Problem version

→ is there a Truth assignment for x, y, z such that F == True ⇒ Y or N
→ Y if x = True, y = False, z = False

### Problem transformation

**_”주어진 어려운 문제를 NP-C로 증명할 수 있다.”_**

NP-C 중 하나가 해결되면, 다른 NP-C도 변환해서 해결!

### Transformation Algorithm/Technique

- want to solve a problem A
- we have an algorithm to solve a problem B

**To solve A**,

1. transform(reduce) a ⇒ b
2. apply algorithm for B

There is an algorithm to transform an instance a of A to b(an instance of B) such that a is yes if b is yes.

_A is Poly.time reducible to B_ **_if there is Poly.time algorithm from A to B_**

A ⇒ B(in P time)

### Theorem

If Decision Problem B is P-class and A ⇒ B(in P time), A is also P.

SAT is Decision Problem. So, A should be Decision Problem

Ex) Hamiltonial Circuit Decision Problem is NP-Complete if

1. HC.DP is NP and
2. SAT.DP can be transformed into HC.DP in P-time.
