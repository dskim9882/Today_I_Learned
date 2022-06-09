# ***Topological Sort***
## 정의
해석 하면 위상 정렬이다. Directed acyclic graph(DAG)에 대해서 vertices들을 선형 정렬하는 것이다. Edge (u, v)가 있으면, 위상 정렬 이후엔 vertex u가 vertex v 전에 위치하여야 한다. 보통 수평선을 따라 나타내며, 모든 directed edges(arcs)가 왼쪽에서 오른쪽으로 향하도록 정렬한다.
## 알고리즘
### [DFS](https://github.com/dskim9882/Today_I_Learned/blob/master/Algorithm/DFS.md)
```
TOPOLOGICAL-SORT(G)
    call DFS(G) to compute finishing times v.f for each vertex v
    as each vertex is finished, insert it onto the front of a linked list
    return the linked list of vertices
```
### Kahn's algorithm
DAG에는 적어도 하나의 vertex는 들어오는 edge를 갖지 않는다. 즉, indegree가 0인 vertex가 적어도 하나는 있다. 
1. indegree가 0인 vertex 하나를 찾아 queue에 넣고 graph에서 제거한다.
2. graph에 남는 vertex가 없을 때까지 1번을 반복한다.
<center><img src="https://user-images.githubusercontent.com/78060320/172825394-6a8aa606-34b5-447f-9849-77127bce0c10.png" width="100%" height="100%"></center>

## Applications
* [Single-Source Shortest paths in a DAG](https://github.com/dskim9882/Today_I_Learned/blob/master/Algorithm/Shortest_paths_problem.md)