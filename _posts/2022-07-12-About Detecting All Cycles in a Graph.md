---
title: About Detecting All Cycles in a Graph
category: algorithm
tags: DFS Backtracking graph
toc: true
toc_label: "Contents"
---

# Problem

주어진 무방향 그래프에 대하여, 그래프에 속하는 모든 *사이클* 을 출력한다.

## Approach

그래프 컬러링 방법을 이용하여, 모든 *서로 다른 사이클들* 에 고유한 숫자들을 부여한다. 

그래프 탐색이 끝나면, 모든 비슷한 숫자들을 *인접 리스트* 에 넣고 출력한다. 

## Procedural steps

1. 모든 에지들을 인접 리스트에 넣는다.
2. dfs cycle detection 함수를 호출한다.(임의의 정점으로 부터)
3. 만약 *이미 한번 방문된 정점이면,* 현재 방문한 정점의 부모 정점으로 부터, *현재 방문한 정점이 나올 때 까지 백트랙 하면서,* 백트랙하는 정점들을 *사이클 리스트* 에 넣는다.
4. **all cycle detection** 이 끝나면, 사이클들을 출력한다.

### Pseudo code

```python
allCycleDectection(u, parentVertex, parents, visits, cycles) {
	cycleNumber;
	이미 탐색이 모두 끝난 정점이라면 -> 함수 종료;
	이미 한번 방문한 정점이라면 {
		increase cycleNumber;
		while backtracking from parentVertex {
			put vertices into cycle list
			return
		}
	아니면 {
		현재 정점u의 부모 정점 = parentVertex;
		현재 정점u의 visits = 1;
		for 현재 정점의 인접한 정점 v에 대해 {
			만약 v가 u의 부모 정점이라면 -> 다음 정점으로
			아니면 u를 부모로하는 allCycleDetection();
	}
	현재 정점 u의 visits = 2;
}
```

### Geeks for Geeks example

```python
graph = [[] for i in range(N)]
cycles = [[] for i in range(N)]
 
 
# Function to mark the vertex with
# different colors for different cycles
def dfs_cycle(u, p, color: list,
              mark: list, par: list):
    global cyclenumber
 
    # already (completely) visited vertex.
    if color[u] == 2:
        return
 
    # seen vertex, but was not
    # completely visited -> cycle detected.
    # backtrack based on parents to
    # find the complete cycle.
    if color[u] == 1:
        cyclenumber += 1
        cur = p
        mark[cur] = cyclenumber
 
        # backtrack the vertex which are
        # in the current cycle thats found
        while cur != u:
            cur = par[cur]
            mark[cur] = cyclenumber
 
        return
 
    par[u] = p
 
    # partially visited.
    color[u] = 1
 
    # simple dfs on graph
    for v in graph[u]:
 
        # if it has not been visited previously
        if v == par[u]:
            continue
        dfs_cycle(v, u, color, mark, par)
 
    # completely visited.
    color[u] = 2
 
# add the edges to the graph
def addEdge(u, v):
    graph[u].append(v)
    graph[v].append(u)
 
# Function to print the cycles
def printCycles(edges, mark: list):
 
    # push the edges that into the
    # cycle adjacency list
    for i in range(1, edges + 1):
        if mark[i] != 0:
            cycles[mark[i]].append(i)
 
    # print all the vertex with same cycle
    for i in range(1, cyclenumber + 1):
 
        # Print the i-th cycle
        print("Cycle Number %d:" % i, end = " ")
        for x in cycles[i]:
            print(x, end = " ")
        print()
 
# Driver Code
if __name__ == "__main__":
 
    # add edges
    addEdge(1, 2)
    addEdge(2, 3)
    addEdge(3, 4)
    addEdge(4, 6)
    addEdge(4, 7)
    addEdge(5, 6)
    addEdge(3, 5)
    addEdge(7, 8)
    addEdge(6, 10)
    addEdge(5, 9)
    addEdge(10, 11)
    addEdge(11, 12)
    addEdge(11, 13)
    addEdge(12, 13)
 
    # arrays required to color the
    # graph, store the parent of node
    color = [0] * N
    par = [0] * N
 
    # mark with unique numbers
    mark = [0] * N
 
    # store the numbers of cycle
    cyclenumber = 0
    edges = 13
 
    # call DFS to mark the cycles
    dfs_cycle(1, 0, color, mark, par)
 
    # function to print the cycles
    printCycles(edges, mark)
```

[Print all the cycles in an undirected graph - GeeksforGeeks](https://www.geeksforgeeks.org/print-all-the-cycles-in-an-undirected-graph/?ref=gcse)

### Time Complexity

O(N+M): N = number of vertices, M = number of edges

### Space Complexity

O(N+M)