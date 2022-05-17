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