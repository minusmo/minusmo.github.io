---
layout: posts
title: About Algorithm3
category: algorithm
tags: ps algorithm D&C
---

# 알고리즘 03 Divide and Conquer: Quick Sort

# Divide and Conquer: Quick Sort - Design

### D and C without Step 3(Combine) → Quick Sort

Q: Combine step 없이 정렬을 하기 위해서는 어떻게 해야 하는가?

A: Divide(step 1)을 더 잘해야 한다!!

```jsx
Quick_Sort(low, high);
{
  if (hight > low) {
    //stopping(termination) condition
    Divide(low, high);
    Quick_Sort(low, pivot_index - 1); //left
    Quick_Sort(pivot_index + 1, high); //right
  }
}
```

### Quick Sort Analysis: T(n)

T(n)

= Divide + Conquer + Combine

= (n-1) + T(n/2) + T(n/2) + 0 —> Best Case —> ... —> ≤ O(nlogn)

= (n-1) + T(n-1) + T(1) + 0 —> Worst Case —> ... —> ≤ O(n^2)

## Recurrences

### Recurrence equations

1. Describe a sequence of numbers

- Early terms(numbers) are specified explicity
- Later terms are calculated(expressed) as function of their predecessors

ex) T(1) = 1, T(n) = T(n-1) + 1

1. Reduces a big problem into smaller problems until easy cases(terms) are reached(progressively)
2. Useful and Powerful to analyze the performance of recursive algorithms → Time Complexity analysis

**_D and C is not Recurrence!!!_**

## Two big classes of recurrences in CS

1. Linear recurrence
   Later terms = linear combinations of early terms
   Linear Algebra
   ex) fibonacci recurrence
2. D and C recurrence
   ex) merge sort recurrence

## 주목해야 할 점들

1. **더 작은 문제들을 만들어 내는 것**이, **재귀적 호출당 추가적인 단계를 줄이는 것**보다 알고리즘적 속도(효율성)에서 중요하다.
2. 일반적으로, 선형적 재귀(큰 하위 문제들을 가지고 있는)들은 주로 지수적 해법(극도로 비효율적)이다.
   하지만 분할 정복 재귀(작은 하위 문제들을 가지고 있는)들은 주로 다항 함수적 시간복잡도에 그친다.
3. 만약 하위 문제들이 원래 문제 크기의 일부에 그친다면, 해당 해법은 주로 다항 함수에 그치는 시간복잡도를 가진다. —> 분할 정복 디자인이 좋다.
4. 더욱 안좋은 것은, 피보나치 재귀들은 **”겹치는"** 하위 문제들을 가진다. → 같은 항에 대한 반복되는 계산이 수행된다. —> 극도로 비효율적이다!!
5. 어떻게 이런 선형 재귀를 다루어야 하는가?
   우리는 이런 재귀들이 **반복적으로 다루어 질 수 있음을 안다.
   —> 새로운 디자인의 도입을 통해 해결한다!(Dynamic Programming)**
