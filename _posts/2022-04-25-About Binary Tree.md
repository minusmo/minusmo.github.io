---
layout: posts
title: About Binary Tree
category: dataStructure
tags: tree graph
---

## 이진 트리의 특징들

이진 트리의 가장 큰 특징은, **_주어진 어떠한 노드의 차수라도 2를 넘지 않는다_** 라는 것이다.

이진 트리에서 우리는 **_왼쪽 서브트리_** 와 **_오른쪽 서브트리_** 를 구분하기는 하지만, 그들의 순서는 중요하지 않다.

이진 트리는 노드를 **전혀 가지지 않을 수** 도 있다.

이진 트리는 이처럼 트리와는 확실히 구별되는 다른 특징들이 있다.

**Definition:** A _binary tree_ is a finite set of nodes that is either empty or consists of a root
and two disjoint binary trees called the left subtree and the right subtree.

### Skewed Tree

이 특이한 경우는, 트리가 왼쪽 혹은 오른쪽으로 치우쳐져 있는 경우이다.

### Complete Binary Tree

이진트리가 좌 → 우 의 순서로 채워져 있는 이진 트리이다.

### ADT of Binary Tree

BinTree Create(): create empty bt.

Boolean IsEmpty(bt): check wheter bt is empty

BinTree MakeBT(bt1, item, bt2): make bt root of which has item and left subtree is bt1, right subtree is bt2

BinTree Lchild(bt): return left subtree of bt else return error

BinTree Rchild(bt): return right subtree of bt else return error

element Data(bt): return root node of bt else return error

### Properties of Binary Trees

**Maximum number of nodes**

1. The maximum number of nodes on level i of a binary tree is 2^(i-1) i ≥ 1
2. The maximum number of nodes on level i of a binary tree is 2^k -1 k ≥ 1

**Relation between number of leaf nodes and nodes of degree 2**

For any nonempty binary tree, **_T,_** if /iq is the number of leaf nodes and ^2 the number of nodes of
degree 2, then = ^2 + 1.

**Definition: _A full binary tree_** of depth **_k_** is a binary tree of depth **_k_** having 2^ - 1 nodes,
**_k>0._**

**Definition:** A binary tree with _n_ nodes and depth _k_ is _complete iff_ nodes correspond to

the nodes numbered from 1 to _n_ in the full binary tree of depth _k._

### Binary Tree Representations

**Array Representation**

1. _parent_ is at [ *i / 2]\* if i != 1 If i == 1, i is at the root and has no parent.
2. left_child(i) is at 2i if 2i ≤ n. If 2I ≥ n, then i has no left child.
3. right_child(i) is at 2i + 1 if 2i + 1 ≤ n. If 2i + 1 > n, then i has no right child.

**Linked Representation**

```cpp
struct node* tree_pointer;
struct node {
int data;
tree_pointer left_child, right_child;
};
```
