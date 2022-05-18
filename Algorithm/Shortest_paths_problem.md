# ***Shortest-paths Problem***
## Introduction
Directed graph *G = (V,E)* 와 Weight function *w : E -> **R*** 이 주어진다.
</br>Path *p*의 weight는 *p*에 있는 edge의 weights의 합계이다.
</br>이때, Shortest-path weight from u to v는 다음과 같다.
</br>
> *&delta;(u, v) =* 
>> *min{w(p) : u ~> v}, if there is a path from u to v,*
>> </br>*Infinite, otherwise.*

*w(p) = &delta;(u, v)* 를 만족하는 path p는 u에서 v까지의 shortest-path이다.
## Variants
1. Single-source shortest paths problem
    * 그래프의 모든 vertex에 대해서 source vertex s에서 시작하는 shortest paths를 찾는 문제 (1 to All)
2. Single-destination shortest paths problem
    * 주어진 destination vertex로 끝나는 모든 shortest paths를 찾는 문제 (All to 1)
    * 그래프의 모든 엣지의 방향을 뒤집어서 single-source 문제로 바꾸어 풀 수 있음
3. Single-pair shortest-paths problem
    * u에서 v까지의 shortest-path를 찾는 문제 (1 to 1)
4. All-pairs shortest-paths problem
    * 모든 vertex에 대해서 시작하고 끝나는 shortest-paths를 찾는 문제 (All to All)
## 특징
* Opitmal Substructure
    * vertex v<sub>0</sub>에서 v<sub>k</sub>까지의 shortest path p가 p = <v<sub>0</sub>, v<sub>1</sub>, ..., v<sub>k</sub>>이고,  0<=i<=j<=k를 만족하는 어느 i,j에 대해서 vertex v<sub>i</sub>에서 v<sub>j</sub>까지의 p의 subpath가 p<sub>ij</sub> = <v<sub>i</sub>, v<sub>i+1</sub>, ..., v<sub>j</sub>>라고 하자.
    * 그럼, p<sub>ij</sub>는 v<sub>i</sub>에서 v<sub>j</sub>까지의 shortest path이다.
* 그래프에 Negative-Weight Cycle이 존재하면 안된다.
    * path weight가 무한정 작아지기 때문이다.
* Shortest path는 cycle을 가질 수 없다
    * Negative-weight cycle : 위에서 언급했 듯 무한정 짧아지기 때문이다
    * Positive-weight cycle : 짧은 길을 찾는 것이기 때문에 cycle을 돌 필요가 없다
    * Zero-weight cycle : 돌아도 의미가 없다
* Shortest-path의 edge 개수는 최대 |V|-1이다
## 용어 정리
For each v ∈ V:
* v.d = shortest-path estimate
    * 초기값은 무한대이고, 알고리즘 진행에 따라 감소할 수 있다. (단, 항상 v.d &ge; &delta;(s, v)를 만족한다)
* v.&pi; = s에서 출발하는 shortest-path에서 v이 바로 이전의 vertex
```
// shortest-paths를 찾는 알고리즘의 초기 설정
init_Single_Source(G, s)
    for each vertex v ∈ G.V
        v.d = INF
        v.&pi; = NIL
    s.d = 0
```
* V<sub>&pi;</sub> = {v∈V: v.&pi; != NIL} ∪ {s}, E<sub>&pi;</sub> = {(v.&pi;, v)∈E: v ∈ V.&pi - {s}}
* the predecessor subgraph G<sub>&pi;</sub> = (V<sub>&pi;</sub>, E<sub>&pi;</sub>)
* Relaxation
    * edge (u, v)에 대해서 기존의 shortest-path보다 개선할 수 있는지 판단하고 개선이 가능하다면, 그에 맞게 v.d와 v.&pi;를 업데이트 시켜주는 것
```
Relax(u, v, w)
    if v.d > u.d + w(u, v)
        v.d = u.d + w(u, v)
        v.&pi; = u
```
## 특성
* Triangle inequality
    * 모든 edge (u,v)에 대해서, &delta;(s, v) &le; &delta;(s, u) + w(u, v) 이다.
* Upper-bound property
    * 모든 vertex v에 대해서 v.d &ge; &delta;(s, v)이다.
    * v.d = &delta;(s, v)로 설정되고 나면 바뀌지 않는다.
* No-path property
    * &delta;(s, v) = INF라면, v.d는 항상 무한대이다.
* Convergence property
    * 만약 s->u->v가 shortest path이고 u.d = &delta;(s, u)일 때 Relax(u, v, w)를 호출했다면, v.d = &delta;(s, v)로 수렴한다. 
* Path relaxation property
    * p = <v<sub>0</sub>, v<sub>1</sub>, ..., v<sub>k</sub>>는 s=v<sub>0</sub>에서 v<sub>k</sub>까지의 shortest path라고 하자.
    * 만약 (v<sub>0</sub>, v<sub>1</sub>),(v<sub>1</sub>, v<sub>2</sub>), ... ,(v<sub>k-1</sub>, v<sub>k</sub>)를 순서대로 relax한다면, v<sub>k</sub> = &delta;(s, v<sub>k</sub>)이다.
* Predecessor-subgraph property
    * 모든 vertex v에 대해서 v.d = &delta;(s, v)로 초기화되고 나면, predecessor subgraph는 s가 root인 shortest-paths tree이다.
## Bellman-Ford Algorithm
모든 edge에 대해서 relax하는 동작을 반복해서 Shortest-path를 찾고 성공하면 True, 실패하면 False를 반환하는 DP algorithm이다.
* 모든 edge에 대해서 relax하는 동작을 |G.V| - 1 번 반복한다.
    * 1st iteration : (v<sub>0</sub>, v<sub>1</sub>) 을 relax할 수 있다.
    * 2nd iteration : (v<sub>1</sub>, v<sub>2</sub>) 을 relax할 수 있다.
    * kth iteration : (v<sub>k-1</sub>, v<sub>k</sub>) 을 relax할 수 있다.
    * Path-relation property에 따라서 v.d = v<sub>k</sub>.d = &delta;(s, v<sub>k</sub>) = &delta;(s, v) 이다.
* negative-weigth edges를 가지는 것은 상관없지만, negative-weight **cycles**은 포함될 수 없다.
    * 모든 edge에 대하여 relax 가능 여부를 한 번 더 확인하고 가능한 edge가 있다면 negative-weight가 있다는 의미이므로 false를 반환한다.
* 시간 복잡도 : (|V| - 1) * E -> *O(VE)*
```
Bellman-Ford(G, w, s)
    init_single_Source(G, s)
    for i = 1 to |G.V| - 1
        for each edge (u, v) ∈ G.E
            Relax(u, v, w)
    for each edge (u, v) ∈ G.E
        if v.d > u.d + w(u, v)
            return false
    return true
```
## Dijkstra's Algorithm
negative-weight edges가 없을 때 사용할 수 있는 Greedy algorithm이다.
</br>BFS의 weighted version으로, FIFO queue 대신 priority queue를 사용한다. Key 값은 shortest-path weights(v.d)이다.
```
Dijkstra(G, w, s)
    init_Single_Source(G, s)
    S = ∅
    Q = G.V //priority queue
    while Q != ∅
        u = Extract-Min(Q)
        S = S U {u}
        for each vertex v ∈ G.Adj[u]
            Relax(u, v, w)
```
* 시간 복잡도 : O(V+E)

## Single-Source Shortest-path in a Directed Acyclic Graph(DAC)
1. DAC의 모든 vertex를 위상 정렬 (topological sort) 
2. 시작 vertex부터 인접한 vertices들과 relaxation을 진행한다.
* Directed Acyclic Graph 자체가 negative-weight cycle이 없다는 것을 보장한다.
```
DAG_Shortest_Path(G, w, s)
    topological sort the vertices of G
    init_Single_Source(G, s)
    for each vertex u, taken in topologically sorted order
        for each vertex v ∈ G.Adj[u]
            Relax(u, v, w)
```