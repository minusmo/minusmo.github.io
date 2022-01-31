---
layout: posts
title: About Dijkstra
category: algorithm
tags: algorithm graph
---

## 다익스트라 알고리즘이란?  
두 노드를 잇는 가장 짧은 경로를 찾는 문제인 _최단 경로 문제_ 로, 
가중치 그래프에서 간선의 가중치의 합이 최소가 되도록 하는 경로를 찾는 것이 목적이다.  

이 __최단 경로 문제__ 중에서,  
#### 단일 출발(single-source) 최단 경로 문제  
에 해당한다.  

_단일 출발 최단 경로 문제_ 는, 그래프 내의 특정 노드에서 출발하여, 
그래프 내의 다른 모든 노드에 도착하는 가장 짧은 경로를 찾는 문제이다.  

## 다익스트라 알고리즘의 논리  
첫 정점을 기준으로, 연결되어 있는 정점들을 추가해 가며, 최단 거리를 갱신하는 기법이다. 너비 우선 탐색(BFS)와 유사한 면이 있다. 첫 정점부터 각 노드간의 거리를 저장하는 배열을 만든 후, 첫 정점의 인접 노드 간의 거리부터 먼저 계산하면서, 첫 정점부터 해당 노드간의 가장 짧은 거리를 해당 배열에 업데이트한다.  

다익스트라 알고리즘은 여러가지 방법으로 구현할 수 있지만, 가장 개선된 방법은 
우선 순위 큐를 이용한 방법이다.  

>우선 순위 큐는, _MinHeap_ 방식을 활용하여, 현재 가장 짧은 거리를 가진 노드 정보
를 먼저 꺼내게 된다.  

#### 구현 순서  
1. 첫 정점을 기준으로 배열을 선언하여 첫 정점에서 각 정점까지의 거리를 저장한다.  
- 초기에는 첫 정점의 거리는 0, 나머지는 _무한대(가능한한 큰 수)_ 로 저장함  
- 우선 순위 큐에 첫 정점(시작 점)을 먼저 넣는다.  

2. 우선 순위 큐에서 노드를 꺼낸다.  
- 처음에는 첫 정점만 저장되어 있으므로, 첫 정점이 꺼내진다.  
- 첫 정점에 인접한 노드들에 대해, 첫 정점에서 각 노드로 가는 거리와, 현재 배열에 
저장되어 있는 첫 정점에서 각 정점까지의 거리를 비교한다.  
- 배열에 저장되어 있는 거리보다, 첫 정점에서 해당 노드로 가는 거리가 더 짧을 경우, 배열에 해당 노드의 거리를 업데이트 한다.  
- 배열에 해당 노드의 거리가 업데이트 된 경우, 우선 순위 큐에 넣는다.
> 결과적으로 BFS와 유사하게, 첫 정점에 인접한 노듣들을 순차적으로 방문하게 된다.  
만약 배열에 기록된 현재까지 발견된 가장 짧은 거리보다, 더 긴거리(루트)를 가진 (노드, 거리)의 경우에는 해당 노드와 인접한 노드간의 거리 계산을 하지 않는다.  

3. 2번의 과정을 우선 순위 큐가 비어있지 않는 동안 반복한다.  

예제 코드  
```python
def Edge(distance, vertex):
    return (distance, vertex)

class Dijkstra:
    def __init__(self, start) -> None:
        self.graph = {
            'a': [Edge(8,'b'), Edge(1,'c'), Edge(2,'d')],
            'b': [],
            'c': [Edge(5,'b'), Edge(2,'d')],
            'd': [Edge(3,'e'), Edge(5,'f')],
            'e': [Edge(1,'f')],
            'f': [Edge(5,'a')]
        }
        
        self.startEdge = Edge(0, start)
        
        self.initializeDistances()
        
        self.prioriryQueue = PriorityQueue()
        self.prioriryQueue.put(self.startEdge)
    
    def initializeDistances(self):
        self.distances = {}
        for key in self.graph.keys():
            self.distances[key] = sys.maxsize
        self.distances[self.startEdge[1]] = 0
        
    def dijkstraPath(self):
        while not self.prioriryQueue.empty():
            currentDistance, edgeNode = self.prioriryQueue.get()
            currentNode = edgeNode
            
            if currentDistance > self.distances[currentNode]:
                continue
            
            nodeList = self.graph[currentNode]
            for adjacentNode in nodeList:
                adjacent = adjacentNode[1]
                weight = adjacentNode[0]
                distance = currentDistance + weight
                
                if distance < self.distances[adjacent]:
                    self.distances[adjacent] = distance
                    self.prioriryQueue.put(Edge(distance, adjacent))
        
        return self.distances
```  

## 다익스트라 알고리즘의 시간 복잡도  
#### 다익스트라 알고리즘은 두 가지 과정을 거친다.  
1. 각 노드마다 인접한 간선들을 모두 검사하는 과정  
2. 우선 순위 큐에 노드/거리 정보를 넣고 삭제(pop)하는 과정  

각 과정별 시간 복잡도는 다음과 같다.  
1. 각 노드는 최대 한 번씩 방문하므로, 그래프의 모든 간선은 최대 한번씩 검사한다.
즉, 각 노드마다 인접한 간선들을 모두 검사하는 과정은 O(E)가 된다.  
2. 우선 순위 큐에 가장 많은 노드, 거리 정보가 들어가는 경우, 우선 순위 큐에 노드/거리 정보를 넣고, 삭제하는 과정에서 최악의 시간이 걸린다.  
- 이 때, 추가는 각 간선마다 최대 한 번 일어날 수 있으므로, 최대 O(E)의 시간 복잡도를 가지고, O(E)개의 노드/거리 정보에 대해 우선순위 큐를 유지하는 작업은 O(logE)ㅇㅇ의 시간 복잡도를 가진다.  
- 따라서 과정 2의 시간 복잡도는 O(ElogE)가 된다.  

따라서 ___총 시간 복잡도___ 는,  
O(E) + O(ElogE) = O(E + ElogE) = O(ElogE)이 된다.  
