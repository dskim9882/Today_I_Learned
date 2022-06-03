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
        * Flow conservation: For all u ∈ V - {s, t}, &Sigma;<sub>v∈V</sub>*f(v, u)* = &Sigma;<sub>v∈V</sub>*f(u, v)* <br/>("Flow in equals flow out.")
* flow *f*의 value, |*f*|
    * |*f*| = &Sigma;<sub>v∈V</sub>*f(s, v)* - &Sigma;<sub>v∈V</sub>*f(v, s)* = flow out of source - flow into source
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
<center><img src="https://user-images.githubusercontent.com/78060320/171802175-2b93af96-1247-4ac6-81e5-f489d5a90c69.png" width="40%" height="40%"></center>

* Residual network is *G<sub>f</sub> = (V, E<sub>f</sub>), where E<sub>f</sub> = {(u, v) ∈ V X V: c<sub>f</sub>(u, v) > 0}*
* Given flows *f* in *G* and *f'* in *G<sub>f</sub>*, define (*f &uarr; f'*)
* Augmentation of *f* by *f'*, as a function V X V &rarr; **R**
* *(f &uarr; f')(u, v) =* 
    * *f(u, v) + f'(u, v) - f'(v, u) if (u, v)* ∈ *E*,
    * 0 otherwise.

### Augmenting paths
augmenting path *p* 는 residual network *G<sub>f</sub>* 에서의 s에서 t까지의 simple path이다. 
* the residual capacity of *p*
    * *c<sub>f</sub>(p) = min{c<sub>f</sub>(u, v) : (u, v) is on p}*
### Cuts
cut (S, T) of flow network G = (V, E)는 V를 S와 T = V - S로 나누는 것이다. 즉, 그래프의 vertices들의 집합을 두 동강 내는 것이다.
* flow *f*에 대해서, cut (S, T)를 가로지르는 net flow
    *  *f(S,T) = &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(u, v) - &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(v, u)*
* Capacity of cut (S, T)
    * *c(S, T) =  &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub>c(u, v)*
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