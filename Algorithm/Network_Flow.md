# ***Network Flow***
## Introduction
Edge로 흐르는 데이터에 대해 그래프로 모델링하여 한 vertex에서 다른 vertex로 얼마나 많은 데이터가 흐를 수 있는지에 대한 문제를 해결하는 알고리즘이다.
그래프의 edge는 capacity(용량)을 가지고 있다.
* Source : 데이터를 일정 비율로 내보낸다
* Sink : 데이터를 동일한 비율로 소비한다.
## 특징
Directed graph *G = (V,E)* 이 주어진다.
* 각 edge *(u, v)* 는 *capacity c(u, v) &ge; 0* 을 가진다.
    * *(u, v)* 가 그래프 *G* 의 edge가 아니면, *c(u, v) = 0* 이다.
    * *(u, v)* 가 그래프 *G* 의 edge라면, reverse edge *(v, u)* 는 *G* 의 edge가 아니다.
* 두 구별되는 vertices인 source *s*, sink *t*는 그래프 *G*의 모든 vertex에 대하여 각 vertex는 source에서 sink까지 가는 path에 사용될 수 있다.
* Flow
    * function *f* : V X V -> **R** satisfying
        * Capacity constraint: For all u, v ∈ V, 0 &le; *f(u, v)* &le; *c(u, v)* 
        * Flow conservation: For all u ∈ V - {s, t}, &Sigma;<sub>v∈V</sub>*f(v, u)* = &Sigma;<sub>v∈V</sub>*f(u, v)* <br/>source와 sink를 제외한 vertex에 대해서 들어오는 flow의 총량과 나가는 flow의 총량은 같다.("Flow in equals flow out.")
* flow *f*의 value, |*f*|
    * |*f*| = &Sigma;<sub>v∈V</sub>*f(s, v)* - &Sigma;<sub>v∈V</sub>*f(v, s)* = flow out of source - flow into source
    * source에 나가는 flow들의 합에서 source로 들어오는 flow의 합을 빼면, network에 흐르는 flow의 값을 구할 수 있다.
* Maximum flow problem
    * flow network G와, s, t, c가 주어졌을 때, G에서 최대 flow 값을 찾는 문제
* Antiparallel edges
    * flow network에서 edge (u, v)와 (v, u)는 동시에 존재할 수 없다. 
    * 한쪽 edge에 vertex v'를 추가하여 (u, v'), (v', v)로 나눈다.
    * *c(u, v') = c(v', v) = c(u, v)*
    * 이런 방식으로 antiparallel(역평행) edge가 없는 equivalent flow network 로 대치한다.
* Networks with multiple sources and sinks
    * 평범한 maximum flow problem으로 만들 수 있다.
        * supersource s와 directed edge (s, s<sub>i</sub>)를 추가 한다. *c(s, s<sub>i</sub>) = &infin; for each i = 1,2, ... ,m*
        * supersink t와 directed edge (t<sub>i</sub>, t)를 추가 한다. *c(t<sub>i</sub>, t) = &infin; for each i = 1,2, ... ,m*

## The Ford-Fulkerson method
반복적으로 the value of the flow(유량) |*f*|을 증가시키는 방법이다.
 * Flow network *G*의 모든 vertex에 대하여 *f(u, v) = 0*에 시작한다. 
 * 각 반복마다, "residual network" *G<sub>f</sub>* 에서 "augmenting path"를 찾음으로써 *G*에서의 flow를 증가시킨다.
 * 반복 과정에서 |*f*|를 증가시킬 수 있지만 *G*의 특정 edge의 flow는 증가할 수도, 감소할 수도 있다.
 * Residual network에서 더이상 augmenting paths가 없을 때까지 flow를 반복적으로 증가시킨다.
 ```
 Ford-Fulkerson-Method(G, s, t)
    initialize flow f to 0
    while there exists an augmenting path p in the residual network G_f
        augment flow f along p
    return f
 ```
### Residual Network
Residual capacity *c<sub>f</sub>(u, v)*
>*c<sub>f</sub>(u, v) =* 
>>*c(u, v) - f(u, v) if (u, v) ∈ E,*
>>*<br/>f(v, u) if (v, u) ∈ E,*
>>*<br/>0 otherwise.*

현재 network의 edge에 흐르는 flow를 고려하여 각 edge마다의 여분의 capacity를 파악하고, 이 관계를 그래프로 나타낸다. (***Residual Network***) 이러한 여분 capacity를 통해서 source에서 sink로 flow가 더 흐를 수 있는 경로(***augmenting path***)를 파악하고 network의 edge마다 flow를 업데이트(***cancellation***)하여 전체 flow 값을 개선한다.(***Augmentation***)

<center><img src="https://user-images.githubusercontent.com/78060320/171802175-2b93af96-1247-4ac6-81e5-f489d5a90c69.png" width="40%" height="40%"></center>

* Residual network is *G<sub>f</sub> = (V, E<sub>f</sub>), where E<sub>f</sub> = {(u, v) ∈ V X V: c<sub>f</sub>(u, v) > 0}*
* Given flows *f* in *G* and *f'* in *G<sub>f</sub>*, define (*f &uarr; f'*)
* Augmentation of *f* by *f'*, as a function V X V &rarr; **R**
* *(f &uarr; f')(u, v) =* 
    * *f(u, v) + f'(u, v) - f'(v, u) if (u, v)* ∈ *E*,
    * 0 otherwise.
* Residual network를 통해서 edge에서 더 흐를 수 있는 flow가 있으면 더하고, 불필요한 flow가 있다면 빼어 전체 flow 값을 증가시킨다. => 이 과정을 Cancellation이라고 한다.
### Augmenting paths
augmenting path *p* 는 residual network *G<sub>f</sub>* 에서의 s에서 t까지의 simple path이다. 
* the residual capacity of *p*
    * *c<sub>f</sub>(p) = min{c<sub>f</sub>(u, v) : (u, v) is on p}*
*  *p*의 flow 값인 |*f<sub>p</sub>*|는 *c<sub>f</sub>(p)* 의 값만큼 흐를 수 있다. (|*f<sub>p</sub>*| = *c<sub>f</sub>(p)* > 0)
    * *f<sub>p</sub>* =
        * *c<sub>f</sub>(p)*, if (*u, v*) is on *p*,
        * 0, otherwise.
### Cuts
cut (S, T) of flow network G = (V, E)는 V를 S와 T = V - S로 나누는 것이다. 즉, 그래프의 vertices들의 집합을 두 동강 내는 것이다.
* flow *f*에 대해서, cut (S, T)를 가로지르는 net flow
    *  *f(S,T) = &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(u, v) - &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(v, u)*
    * |*f*| = *f(S,T)* for any cut(*S, T*)

<center><img src="https://user-images.githubusercontent.com/78060320/173008899-031b9c56-1505-4077-b186-98b85ce89c5f.png" width="80%" height="80%"></center>

* Capacity of cut (S, T)
    * *c(S, T) =  &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub>c(u, v)*
    * |*f*| &le; *c(S,T)* for any cut(*S, T*)
* Minimum cut of *G*
    * capacity가 가장 작은 cut

### Max-flow min-cut theorem
만약 *f* 가 source s와 sink t를 가진 flow network *G = (V, E)*의 flow라면, 다음 조건들은 동치이다.
1. *f*는 *G*의 maximum flow이다.
2. The residual network *G<sub>f</sub>* 는 augmenting path가 없다.
3. *G*의 몇몇 cut (S, T)에 대해서 *|f| = c(S, T)* 이다.

### The basic Ford-Fulkerson algorithm
 ```
 Ford-Fulkerson(G, s, t)
    for each edge (u, v) ∈ G.E
        (u, v).f = 0
    while there exists a path p from s to t in the residual network G_f
        c_f(p) = min{c_f(u,v) : (u,v) is in p}
        for each edge (u,v) in p
            if (u,v) ∈ E
                (u,v).f = (u,v).f + c_f(p)
            else
                (v,u).f = (v,u).f - c_f(p)
 ```
 <center><img src="https://user-images.githubusercontent.com/78060320/171854406-df78cad0-11d5-4fa7-a770-3481b409ca38.png" width="100%" height="100%"></center>

 ### Analysis of Ford-Fulkerson
 Ford-Fulkerson 알고리즘의 시간 복잡도는 augmenting path p를 찾는 것에 달려있다. the flow network *G = (V, E)* 가 적절한 자료 구조를 사용하고 있고, augmenting path를 찾는데 선형 시간이 걸리는 알고리즘을 사용한다고 생각한다. *f** 은 maximum flow이다. 
 * while 문이 한번 반복될 때마다 flow value가 최소 1 단위 오른다고 생각하면, while문은 최대 |*f**| 반복된다. 
 * residual network에서 path를 찾는 데에 *O(E)* 만큼 걸린다.
 * total running time은 *O*(*E* |*f**|)이다.

 ## Edmonds-Karp Algorithm
 Ford-Fulkerson method의 구현 중 하나이다. Ford-Fulkerson method의 일반적인 구현의 경우, augmenting path p를 찾는 조건은 G<sub>f</sub>에서 s에서 t까지의 simple path라는 것 뿐이다. 이 경우 매우 비효율적인 선택을 할 수도 있다.
 </br>Edmonds-Karp Alogrithm에서는 augmenting path p를 찾는 조건으로 edges의 개수가 가장 적은, 즉, BFS를 통해 찾을 수 있는 shortest path를 추가했다. 이 알고리즘의 시간 복잡도는 *O(VE<sup>2</sup>)* 이다.

 <center><img src="https://user-images.githubusercontent.com/78060320/171989997-79cfec8d-5861-4e6f-a55b-2ffaf45c1de2.png" width="100%" height="100%"></center>

 ## Maximum bipartite matching
 Ford-Fulkerson method로 풀이 가능한 문제이다.
 ### The maximum-bipartite-matching problem
 undirected graph *G* = (*V, E*) 가 주어진다.
* matching M
    * M &sube; E
    * 모든 vertices v &isin; V에 대해서, M의 최대 하나의 edge가 is incident on v 이다.
* 만약 matching M의 몇몇 edge가 is incident on v &isin; V라면, v는 matched라고 한다. 아니라면, free 혹은 unmatched라고 한다.
* maximum matching
    * 어떤 다른 matching M'보다도 matching M이 원소가 많을 때, 즉, |M| &ge; |M'|일 때, matching M은 maximum matching이다.
* bipartite graph
    * V = L &cup; R
    * L &cap; R = &empty;
    * 모든 edge가 L과 R 사이에 있다.
    * 그래프가 bipartite이다. *if and only if* 그래프에 홀수 length의 cycle이 없다.
### Finding a maximum bipartite matching
* the corresponding flow network *G'* = (*V', E'*)
    * *V' = V &cup; {s, t}*
    * *E' = {(s,u) : u &isin; L} &cup; {(u,v) : (u,v) &isin; E} &cup; {(v,t) : v &isin; R}* 
* edge 마다 capacity를 1로 설정하고 Ford-Fulkerson 적용하여 문제 해결 
### Algorithm
* matching M에 대해서, M의 어떤 edge의 endpoint에 속하지 않는 vertex를 free 혹은 unmatched라고 한다.
* 모든 vertex가 matched이면, M은 Maximum matching이다.
* input은 a bipartite graph G = <V,U,E> 이다.

```
Maximum-Bipartite-Matching(G)
    initialize set M of edges with some valid matching (e.g., the empty set)
    initialize queue Q with all the free vertices in V (in any order)
    while not Empty(Q) do
        w <- Front(Q); Dequeue(Q)
        if w ∈ V
            for every vertex u adjacent to w do
                if u is free
                    M <- M U (w, u)
                    v <- w
                    while v is labeled do
                        u <- vertex indicated by v's label; M <- M - (v,u)
                        v <- vertex indicated by u's label; M <- M U (v, u)
                    remove all vertex labels
                    reinitialize Q with all free vertices in V
                    break
                else
                    if (w, u) ∉ M and u is unlabeled
                        label u with w
                        Enqueue(Q,u)
        else
            label the mate v of w with w
            Enqueue(Q,v)
    return M
```