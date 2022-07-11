---
title: About Graph Coloring
category: algorithm
tags: DFS Backtracking graph
toc: true
toc_label: "Contents"
---

# Problem

주어진 방향 그래프에서, 그래프가 *사이클* 을 가지고 있는지 아닌지 판단한다. 만약 그래프에 사이클이 하나라도 있으면, *True* 아니면 *False* 를 반환한다.

## Approach

DFS를 사용하여 사이클을 감지할 수 있다. *연결된* 그래프에서 DFS는 *트리* 를 생성한다. *연결되지 않은* 그래프에서 DFS는 *포레스트* 를 생성한다. 사이클을 감지하기 위해서는, 각각의 트리의 사이클을 *back edge* 가 있는지를 검사한다. 

일반적인 DFS에서는 *방문한 정점(현재 콜스택의 정점)* 을 저장하며 진행한다.

*그래프 컬리링* 에서는, 방문한 정점에 대해 *색깔* 을 부여한다. 

- 흰색: 아직 처리되지 않은 정점의 색
- 회색: 현재 처리되고 있는 정점의 색(이 정점에 대한 DFS가 진행중이며, *자손들*이 아직 모두 처리되지 않은 정점의 색)
- 검은색: 자신과 자신의 모든 자손 정점이 처리된 정점의 색.

## Procedural steps

1. *에지* 와 *색 배열* 을 파라미터로 가지는 재귀 함수를 선언한다.
2. 현재 정점의 색을 **’회색'** 으로 한다.
3. 인접한 모든 정점을 탐색한다. 그리고 인접한 정점 중 *회색* 인 정점이 있으면, *True* 를 반환한다.
4. 인접한 *흰색* 정점이 있으면 그 정점에 대해 재귀 함수를 호출한다. 만약 그 함수가 *True* 를 반환하면, 호출한 함수도 *True* 를 반환한다.
5. 만약 어떠한 인접한 정점도 *회색* 이 아니고 *True* 를 반환하지 않았으면 현재 정점을 *’검은색'* 으로 하고 *False* 를 반환한다.

### Geeks for Geeks example code

```python
class Graph():
    def __init__(self, V):
        self.V = V
        self.graph = defaultdict(list)
 
    def addEdge(self, u, v):
        self.graph[u].append(v)
 
    def DFSUtil(self, u, color):
        # GRAY :  This vertex is being processed (DFS
        #         for this vertex has started, but not
        #         ended (or this vertex is in function
        #         call stack)
        color[u] = "GRAY"
 
        for v in self.graph[u]:
 
            if color[v] == "GRAY":
                return True
 
            if color[v] == "WHITE" and self.DFSUtil(v, color) == True:
                return True
 
        color[u] = "BLACK"
        return False
 
    def isCyclic(self):
        color = ["WHITE"] * self.V
 
        for i in range(self.V):
            if color[i] == "WHITE":
                if self.DFSUtil(i, color) == True:
                    return True
        return False
```

### Time Complexity

O(V+E)

### Space Complexity

O(V)