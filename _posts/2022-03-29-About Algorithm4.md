---
layout: posts
title: About Algorithm4
category: algorithm
tags: ps algorithm DP
---

# 알고리즘 04 Dynamic Programming

# Dynamic Programming

## Design

### Step1:

- establish a recursive property from the problem
- identify(find out, derive) a **recurrence equation** from the problem
- 큰 문제 = 작은 문제 + /\* 작은 문제 + ... + 작은 문제

### Step2:

- solve in a **bottom-up** fashion programming
- **solve smaller problems first**(easy problem first)
- **save** them(smaller problems) in arrays(tables, dict...)
- use them later(from look-up tables)

Also called **_Save and Reuse_** Strategy!!!

## Basic Steps

1. **make examples**(guessing)
2. recursive property = recurrence(**in mathematical expression**)
3. **Save / Reuse**

## Good Examples

- binomial coefficients
- chained matrix multiplication
