# ***Minimum Spanning Trees***
## 정의
### *Spanning Tree*
graph *G*에 대하여 다음과 같은 조건을 만족하는 tree *T*는 *G*의 spanning tree이다.
1. *T*는 *G*의 subgraph이다.
2. *T*는 *G*의 모든 vertices를 가지고 있다.

DFS, BFS를 통해서 탐색한 edge들을 모으면 spanning tree를 찾을 수 있다.
### *Minimum spanning tree*
weighted graph *G*가 주어졌을 때, *G*의 spanning trees 중에서 total edge weight가 가장 작은 것을 minimum spanning tree(MST)라고 한다.
## 특징
* *G*의 vertices의 개수가 *V*라면 MST는 *V*-1 개의 edge를 가진다.
* Cycle이 없다
* 유일하다고 할 수 없다.

## MST를 구하는 2가지 알고리즘
### Kruskal's Algorithm
connected, undirected, weighted graph *G=(V,E)*
1. 그래프의 edge들을 가중치에 따라 오름차순으로 정렬한다.
2. 정렬된 순서에 따라 현재까지 선택된 edge들과 cycle이 만들어지지 않는 edge를 하나 찾는다.
3. 발견된 edge를 현재 MST 집합에 추가한다.
```c++
TREE Kruskal(Graph G){
    TREE A;
    for(/*그래프 G의 각 vertex v*/){
        MAKE_SET(v);//원소가 v만 있는 집합을 만든다.
    }
    sort(/*그래프의 Edge를 가중치에 따라 오름차순 정렬*/);
    for(/*정렬된 그래프의 각 edge e*/){
        if(FIND_SET(e.u) != FIND_SET(e.v)){// edge e에 연결된 두 vertices를 각각 e.u, e.v라고 지칭
            // FIND_SET은 input으로 들어온 vertex가 속한 집합을 return
            // e.u와 e.v가 속한 집합이 같은 집합이면 cycle이 발생하므로 속한 집합이 다를 때 MST에 추가하는 절차 진행
            A.insert_edge(e); //현재 MST에 edge e 추가
            UNION(u,v); // edge e를 추가함으로써 e.u와 e.v가 연결되어 각각이 속한 집합을 연결(합집합, union)
        }
    }
    return A;
}
```
### Prim's Algorithm 
connected, undirected, weighted graph *G=(V,E)*
</br>
시작 vertex로 부터 단계적으로 MST를 확장
1. MST의 초기 집합에 시작 vertex만 추가
2. MST 집합에 인접한 vertices 중에서 가중치가 가장 작은 edge로 연결된 vertex를 MST 집합에 추가
3. MST가 그래프의 모든 vertex를 가질 때까지 위의 과정을 2번 과정을 반복 
```
MST-PRIM(G,w,r)
    for each vertex u in G
        u.key = INF
        u.pi = NULL
    r.key = 0
    Q = G.V
    while Q is not empty
        u = EXTRACT-MIN(Q)
        for each v in G.Adj(u)
            if v is in Q && w(u,v) < v.key
                v.pi = u
                v.key = w(u,v)
```