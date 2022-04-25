---
layout: posts
title: About Tree
category: dataStructure
tags: tree graph
---

## Tree는

다음을 만족하는 한개 이상의 노드의 유한 집합이다.

1. 특수하게 고안된 노드인 **root** 가 있다.
2. 나머지 노드들은 n(0 이상)개의 **분리된(disjoint)** 집합들 T1, T2, ... Tn로 나누어져 있으며,
   각각은 **트리** 이다. 우리는 T1, ... Tn을 **root** 의 **subtree** 라고 부른다.

트리는 이처럼 **recursive definition** 을 가지고 있다는 것을 주목하라.

T1, ... Tn은 반드시 **disjoint set** 이어야 하기 때문에, 서브 트리들은 **절대로** 서로 연결되면 안된다.
이말은, 다른 노드를 통해 교차해서도 안된다는 것이다.

또한 모든 트리의 노드들은 다른 어떤 서브트리의 루트임을 시사한다.

### Degree of node

노드의 **차수**는 노드의 서브트리의 개수를 의미한다.

### Degree of tree

트리의 차수는 트리에 속한 노드의 차수 중 **최대**를 의미한다.

### parent and children

subtree들을 가지는 노드는 그 서브트리들의 루트 노드들의 **_parent_ 라고 한다.**

그리고,

그 루트 노드들을 **_parent_** 의 **_children_** 이라고 한다.

### siblings

같은 부모 노드를 가지는 자식 노드들을 **_siblings_** 라고 한다. 이 정의는 **_grandparents 와 grandchildren_**
까지 확장할 수 있다.

### ancestors

노드의 **ancestors** 은 루트 노드로 부터 해당 노드까지의 경로에 있는 모든 노드들이다.

### level

노드의 **_level_** 은 루트 노드가 level 1에 있다고 시작하여, 모든 하위 노드들에 대해, 하위 노드들의 레벨은 노드들의 부모 노드의 레벨 + 1 이 된다.
