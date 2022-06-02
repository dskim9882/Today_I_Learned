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
### Cuts
cut (S, T) of flow network G = (V, E)는 V를 S와 T = V - S로 나누는 것이다. 즉, 그래프의 vertices들의 집합을 두 동강 내는 것이다.
* flow *f*에 대해서, cut (S, T)를 가로지르는 net flow
    *  *f(S,T) = &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(u, v) - &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub> f(v, u)*
* Capacity of cut (S, T)
    * *c(S, T) =  &Sigma;<sub>u ∈ S</sub>&Sigma;<sub>v ∈ T</sub>c(u, v)*
* Minimum cut of *G*
    * capacity가 가장 작은 cut
### Residual Network
>*c<sub>f</sub>(u, v) =* 
>>*c(u, v) - f(u, v) if (u, v) ∈ E,*
>>*<br/>f(v, u) if (v, u) ∈ E,*
>>*<br/>0 otherwise.*

* Residual network is *G<sub>f</sub> = (V, E<sub>f</sub>), where E<sub>f</sub> = {(u, v) ∈ V X V: c<sub>f</sub>(u, v) > 0}* 
* Augmentation of *f* by *f'*, as a function V X V &rarr; **R**
* Given flows *f* in *G* and *f'* in *G<sub>f</sub>*, define (*f &uarr; f'*)
* *(f &uarr; f')(u, v) =* 
    * *f(u, v) + f'(u, v) - f'(v, u) if (u, v)* ∈ *E*,
    * 0 otherwise.
