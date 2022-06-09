***DFS***
===
Depth-First Search / 깊이 우선 탐색
---
* 그래프에서 어디든지 가능한 더 깊은 노드부터 탐색함
* 모든 노드를 탐색하고자 할 때 사용
* * *
특징
---
* 재귀적 호출을 통해서 구현할 수 있음
* 아직 탐색하지 않은 edge를 가진 가장 최근에 탐색한 노드의 엣지를 탐색함
* 노드의 모든 엣지가 탐색되면 해당 노드가 발견된 경로로 백트래킹함
* 탐색한 노드에 대해 방문 처리를 해주어야 무한 루프에 빠지지 않음
* Stack, 재귀호출을 통해 구현
* * * 
알고리즘
---
1. Input으로 주어진 노드에 인접한 노드 중 방문하지 않은 노드를 찾음
2. 해당 노드를 방문 처리를 하고 해당 노드를 Input으로 주며 DFS 알고리즘을 재귀 호출함
3. 재귀 호출을 통해 방문하지 않은 인접 노드가 없는 노드에 다다르면, 해당 노드의 탐색을 진행함
4. 탐색이 끝나면, 이전 경로의 노드로 백트래킹함

```c++
void DFS(GRAPH graph){
    for(/*graph의 모든 노드 중 하나를 고름*/){
        if(graph.v.visit == false){// v : 고른 노드 중 하나
            graph.v.visit = true;
            DFS_visit(graph, v);// v에서 시작해서 방문할 수 있는 노드들을 모두 탐색
        }
        //아직 방문 하지 못한 다음 노드를 찾아서 다시 DFS
    }
}

void DFS_visit(GRAPH graph, NODE node){
    for(/*방문 노드와 인접한 노드들*/){
        if(graph.adj(node).v == false){// 방문하지 않은 인접 노드
            graph.adj(node).v = true;// 방문 처리
            DFS_visit(graph,graph.adj(node).v); // 재귀 호출을 통해 더 깊은 노드 방문
        }// 해당 분기(branch)의 방문이 모두 끝나면 다음 인접 노드에 대해 DFS 
    }// 모든 인접노드 방문이 끝나면 함수를 종료하여 백트래킹
}
```
아래의 수도 코드에서는 vertex v 별로 방문 시작(v.d)/종료(v.f) time을 기록한다. 이 시간 정보는 [topological sort](https://github.com/dskim9882/Today_I_Learned/blob/master/Algorithm/Topological_Sort.md)에 활용될 수 있다.
</br> 또한 WHITE = undiscover, GRAY = discover, but not finished, BLACK = finished를 의미한다.

```
DFS(G)
    for each vertex u ∈ G.V
        u.color = WHITE
        u.pi = NIL
    time = 0
    for each vertex u ∈ G.V
        if u.color == WHITE
            DFS-VISIT(G, u)

DFS-VISIT(G, u)
    time = time + 1
    u.d = time
    u.color = GRAY
    for each v ∈ G.Adj[u]
        if v.color == WHITE
            v.pi = u
            DFS-VISIT(G, v)
    u.color = BLACK
    time = time + 1
    u.f = time
```