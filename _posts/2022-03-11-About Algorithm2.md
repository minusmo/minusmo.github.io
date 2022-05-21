---
layout: posts
title: About Algorithm2
category: algorithm
tags: problemSolving algorithm Divide&Conquer
---

# 알고리즘 02 Divide and Conquer

# Divide and Conquer - Design

D.C는 굉장히 자연스러운 **Top-Down** approach 이다.

### Steps of D.C.

1. Divide into ≥ 2 smaller problems(instances): 2개 이상의 하위 문제로 나눈다.
2. Solve each instance: 각각의 하위 문제를 푼다.
3. Combine the subsolutions(optional): 하위 해답들을 합친다.(선택적. 필요할 수도, 안할 수도)

- Q: 하위 문제들을 어떻게 푸는가?
- Q: 하위 해답들에 대한 구체적인 디자인은 어디에 있는가?

**_이러한 질문들에 대한 해답은 이미 Steps of D.C.에 포함되어 있는 것!!
따라서 위의 스텝을 따라가기만 한다면 이러한 질문에 대한 답을 궁금해할 필요가 없다!
굉장히 기계적인 방식!_**

sorted S = [10 12 13 14 18 20 25 27 30 35 40]

problem: find x, locate x in S.

## DC_Search(binary search)

if x == S[mid], return mid

1. Divide S into 2 sub arrays
   if x < S[mid], return left array, otherwise right array
2. Conquer(solve) the chosen array
3. Combine(obtain) the solution

### How to solve step 2?

1. recursively: divide and conquer. consice, natural, clear, 기계적 해법
2. iteratively, sequentially(if the subproblem is small): faster, save memory space.(system stack)
   → recursion depth, stack depth: log(n)+1

**_Computing source를 감안해야 한다!!_**

## Detailed ver.

DC_Search(S, x, low, high): S[low] ~ S[high]

if low > high, then return nil.(boundary condition)

else

mid = (low+high)/2

if x == S[mid], then return mid

else if x < S[mid] then return DC_Search(..., low, mid-1)

else return DC_Search(..., mid+1, high)

## Time complexity

1. Best Case: O(1)
2. Worst Case: 1/2 size decreasing → O(logn)

Time Complexity: number of basic operations(컴퓨팅 소스에 상관없이 반드시 해야하는 연산!!)

T(n) = divide + conquer + combine

= 1 + T(n/2) + 0 → recurrence equation
= 1 + 1 + T(n/4)
= ... = T(n/2^k) + k (suppose n=2^k)
= T(n/n) + logn = T(1) + logn = 1 + logn → O(logn)

## k-way merge sort

### 2-way merge sort

**<Design>**

DC_Sort(original array)

1. divide into 2 ≥ subarrrays
2. solve(conquer) each subarray - sort left, right
3. combine the subsolutions - merge left, right

DC_Sort(S[1...n] array)

if n > 1 —> termination condition(depending on your coding style)

DC_Sort(left)

DC_Sort(right)

Combile(left, right)

### D.C: natural, top-down- systematic + termination condition(criteria)

## Time complexity

T(n) = divide + conquer + combine

= 0 + 2 \* T(n/2) + n/2 + n/2 - 1

= 2T(n/2) + n - 1 → recurrence

≤ 2T(n/2) + n = ... = 2^k _ T(n/2^k) + k _ n (suppose n = 2^k: very large number)

= n _ T(n/n) + logn _ n = n _ T(1) + n _ logn

= n \* 0 + nlogn = nlogn

## Divide and Conquer - Recurrence

recursive한 solution의 경우 적절히 iterative한 solution을 섞어 최적화할 필요가 있다.
