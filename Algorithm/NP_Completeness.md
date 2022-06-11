# ***NP-Completeness***
## Classifying Problem Complexity
문제가 tractable(다루기 쉬운)한 가? 즉, 문제를 풀 수 있는 polynomial-time algorithm이 존재하는 가?
* Tractable problems : 문제를 해결할 polynomial time algorithm이 존재한다.
* Intractable problems : 효율적으로 해결할 알고리즘이 없다. 완전 polynomial time이 걸리거나 그 이상의 시간이 필요하다.
* Undecidable problems : 해결할 수 있는 알고리즘이 전혀 없다. (Unsolvable)
## P, NP, NPC
* P = {problems solvable in polynomial time}
    * *n* : problem size
    * polynomial time : *n*<sup>*O(1)*</sup>
* NP = {decision problems solvable in nondeterministic polynomial time}
    * decison problems : answer is YES or NO
    * non-deterministic : can guess one of out polynomially many options in O(1) time
* X is NP-Complete if X &isin; NP & X &isin; NP-hard
* X is NP-hard if every problem Y &isin; NP reduces to X
### the class P
Polynomial time 내에 풀 수 있는(solvable) 문제들이다. 
</br>좀 더 구체적으로 말하자면, 주어진 input의 size가 n일 때, 해당 문제는 어떤 상수 k에 대해서 *O(n<sup>k</sup>)* 의 시간 복잡도 내에 풀 수 있다.

### the class NP
NP는 non-polynomial로 오해할 수 있는 데, 사실은 non-deterministic algorithm의 약자이다. Polynomial time 내에 증명할 수 있는(verifiable) 문제들이다. 
</br>증명될 수 있는 문제(a problem being verifiable)에 대해서 구체적으로 말하자면, 문제의 해답에 대한 증거(certificate)가 주어졌을 때, 이 증거가 올바르다는 것을 *O(n<sup>k</sup>)* 내에 증명(verify)할 수 있는 문제를 말한다. (쉽게, 주어진 답이 진짜 맞는 건지 확인하는 게 polynomial time이 걸리는 것) 다음은 NP의 예시이다.

* the hamiltonian cycle problem : directed graph G = (V, E)가 주어졌을 때, 모든 vertices를 한 번씩 지나는 경로를 찾는 문제
    * sequence <*v<sub>1</sub>, v<sub>2</sub>, v<sub>3</sub>, ... ,v<sub>|V|</sub>*> 가 certificate로 주어질 수 있다.
    * 이 경우, (*v<sub>i</sub>, v<sub>i+1</sub>*) &isin; *E* for *i = 1, 2, 3, ... , |V|-1* 그리고 (*v<sub>|V|</sub>, v<sub>1</sub>*) &isin; *E*임을 polynomial time 내에 쉽게 확인할 수 있다.
* 3-CNF satisfiability
    * 3개의 변수가 OR로 묶여있는 clause 여러개가 AND로 연결되어있는 boolean formula를 1로 만들 수 있는 경우가 존재한다면 해당 boolean formula는 satisfiable 하다.
    * 변수들의 대한 할당값들이 certificate로 주어졌을 때, 이 할당값들이 boolean formula를 satisfy하는 지 polynomial time 내에 확인할 수 있다.

### P와 NP
P에 속한 문제는 특정 certificate가 주어지지 않더라도, 언제든지 문제를 polynomial time 내에 해결할 수 있다. 따라서 P에 속한 모든 문제는 NP에 속한다. (P &sube; NP) 
</br> 문제는 P = NP의 관계가 성립하는 가에 있다. 아직 해결되지 않은 문제이다.

### NPC
NP-Completeness(NPC)는 NP문제에 속하고, NP에 있는 어느 문제만큼 난해한 문제(NP-Hard)이다. 
</br>
NP-Complete 문제가 하나만 해결되더라도, 모든 NP-complete 문제가 해결될 것이다.

### Decision problems vs. optimization problems
NP-completeness는 optimization problem이 아니라 decision problems에 직접 적용한다. 
* Decision problems는 optimization problems보다 더 쉽다(easier), 혹은 적어도 더 어렵진 않다(at least no harder).
    * Decision problems &le; Optimization problems
* 만약 한 optimization problem이 쉽다면, 이와 관련된 decision problem은 쉽다.
    * Decision problems &le; Optimization problems = 쉬움
* 만약 한 decision problem이 어렵다는 증거가 있다면, 이와 관련된 optimization problem은 어렵다는 증거가 된다.
    * Decision problems = 어려움 &le; Optimization problems
### Reductions
Polynomial time으로 해결하고 싶은 decision problem A가 있다. 그리고 polynomial time으로 푸는 방법을 알고 있는 decision problem B가 있다.
</br></br> 특정 문제의 input을 그 문제의 instance라고 한다. polynomial-time reduction algorithm은 A의 instance &alpha;를 B의 instance &beta;로 두 가지 특징에 따라 변형시키는 절차이다. 두 가지 특징은 다음과 같다.

* 환원(reduction) 과정은 polynomial time이 걸린다. 
* 두 답은 같다. 즉, &alpha;의 답이 yes &harr; &beta;의 답이 yes
 <center><img src="https://user-images.githubusercontent.com/78060320/172054762-726f9d2e-c0f2-4fac-9aaa-c026a7f3d0f9.png" width="100%" height="100%"></center>

A 문제를 B문제로 환원(reducing)함으로써 A의 easiness를 증명하는데 B의 easiness를 사용한다.
* A &le;<sub>p</sub> B 라고 표기한다.
* A &le;<sub>p</sub> B = 쉬움 : B의 쉬움으로 인해서 B로 환원되는 A 또한 쉽다는 것을 증명
* A = 어려움 &le;<sub>p</sub> B : A의 어려움으로 인해서 B가 적어도 A만큼은 어려운 문제임을 증명, NP-hard를 보일 때 적용
### NP-Hard
NP에 속하는 어떤 문제든지 polynomial time안에 환원될 수 있는 문제 (problems to which anything in NP be reduced in polynomial time)

### A first NP-Complete problem
Reduction은 어떤 NP-Complete problem을 증명하기 위해서 이미 NP-Complete라고 알려진 문제를 갖는 것에 의존하기 때문에, "first" NP-Complete 문제가 필요하다. 쉽게 요약해서, reduction을 하기 위해서 NPC로 알려진 문제가 필요하다는 것이다.

## Proof of NP-completeness
* 가정 : A에 대한 poly-time solution이 없다. A에서 B로의 poly-time reduction이 있다.(A &le;<sub>p</sub> B)
* B에 대한 poly-time solution이 없다는 것을 모순 통해서 증명한다. 
<center><img src="https://user-images.githubusercontent.com/78060320/173122307-1457f81b-41a0-4d4d-9a06-91ef247922e6.png" width="50%" height="50%"></center>

## 3-CNF-SAT
### 용어
* Literal
    * a Boolean variable 혹은 its negation
    * e.g., x or &not;x
* Clause
    * a disjunction (논리합) of literals
    * e.g., C = x<sub>1</sub> &or; &not;x<sub>2</sub> &or; x<sub>3</sub>
* Conjunctive normal form (CNF) (논리곱 정규형)
    * a propositional formula &Phi; that is a conjunction of clauses
    * e.g., &Phi; = C<sub>1</sub> &and; C<sub>2</sub> &and; C<sub>3</sub> &and; C<sub>4</sub>
### 문제
* &Phi;를 satisfiable 할 수 있는, 즉, 1로 만들 수 있는 boolean variables의 값을 찾기
* Decision version : &Phi;가 satisfiable하기 위한 an assignment of literals가 있는 가?

## CLIQUE Problem
### 용어
* CLIQUE in an undirected graph G = (V,E)
    * a subset V' &sube; V of vertices
    * V'에 속하는 모든 vertices 쌍이 edge로 연결되어 있다.
* the size of a clique : clique 안에 있는 vertices의 개수
### 문제
* graph에서 maximum size의 clique를 찾기
* Decision version : graph에 size가 k인 clique가 존재하는 가?
    * CLIQUE = {(G,k) : G is an graph containing a clique of size k}
    * Brute force algorithm
        * V의 모든 k-subsets을 찾아서 각 subset이 clique인지 확인한다. 이 알고리즘은 poly-time 알고리즘이 아니다.
### CLIQUE problem이 NP-Complete?
CLIQUE 문제가 NP-Complete임을 보이려면 다음 두 가지를 보여야 한다.
1. CLIQUE &isin; NP
2. CLIQUE &isin; NP-Hard
#### 1. CLIQUE &isin; NP
certificate가 주어졌을 때, 이를 poly-time 안에 증명(verify)하면된다.
* CLIQUE 문제에 주어진 certificate는 각 vertices의 쌍에 edge가 있는 지 확인하면 된다.
* size k인 clique에 대해서 확인할 vertices 쌍의 개수는 <sub>k</sub>C<sub>2</sub> 이다.
* 따라서 poly-time 안에 증명 가능하다.
#### 2. CLIQUE &isin; NP-Hard
3-CNF-SAT가 NP-Complete에 속하는 문제이다. 3-CNF-SAT가 CLIQUE로 reduction된다는 것, 즉 3-CNF-SAT &le;<sub>p</sub> CLIQUE 을 보이면, CLIQUE가 NP-Hard에 속하는 것을 증명할 수 있다.

<center><img src="https://user-images.githubusercontent.com/78060320/173178842-e2d8898e-5332-41dc-a37d-b0e677b3ba2d.png" width="100%" height="100%"></center>

<center><img src="https://user-images.githubusercontent.com/78060320/173178844-66df9aa5-8dde-4ec2-adb1-16e6643c24dc.png" width="100%" height="100%"></center>

* 만약 &Phi;가 satisfiable이라면, 각 Clause 마다 적어도 하나의 literal이 1이다. 이 경우, k개의 vertices 집합이 완전히 연결되어 있는 지 확인하면 된다.
    * 3-CNF-SAT의 "NO" instances가 완전히 해결된다.
* 만약 G가 사이즈 k인 clique를 갖는다면, &Phi는 vertices에 상응하는 literals에 1을 할당함으로써 satisfied된다.
    * 3-CNF-SAT의 "YES" instances가 완전히 해결된다.

## VERTEX-COVER &isin; NPC
### 용어
* vertex cover : 모든 edge의 한 쪽 vertex를 포함하는 vertices 집합 V' &sube; V
* V'에 속한 vertices들에 의해서 그래프의 모든 edge가 커버된다.
### 문제
* minimum size의 vertex cover 찾기
* Decision version : graph에 size k 인 vertex cover가 있는가?
    * VERTEX-COVER = {\<G, k>: graph G = (V, E) has vertex cover of size k}
### CLIQUE &le;<sub>p</sub> VERTEX-COVER
1. CLIQUE를 찾을 undirected graph G가 있다.
2. reduction algorithm을 통해서 G에 없는 edge들로 구성된 <span style="text-decoration: overline">G</span>를 만든다.
3. 이때 vertex cover V-V'를 찾는다.
4. CLIQUE는 V-(vertex cover) = V'이다.

## SUBSET-SUM &isin; NPC
### 문제
* SUBSET-SUM = {\<S, t> : S &sub; **N**, t &isin; **N** and &exist; a subset S' &sube; S s.t. t = &Sigma;<sub>s &isin; S'</sub>s}
### 3-CNF-SAT &le;<sub>p</sub> SUBSET-SUM
<center><img src="https://user-images.githubusercontent.com/78060320/173182741-8be0f0e3-9409-49a8-991d-8b29c3c8b3c6.png" width="100%" height="100%"></center>


<!--
## Polynomial time
### 개념 정리
#### ***Abstract problems***
abstract problem Q : a binary relation a set *I* of ***instances*** and a set S of problem ***solutions*** 
* 예시 - SHORTEST-PATH
    * instance : 그래프와, 두 vertices
    * solution : 그래프의 vertices로 이루어진 sequence
    * 주어지는 instance는 shortest-path가 유일하지 않을 수 있으므로 하나 이상의 solution을 가질 수 있다.

abstract ***decision problem*** : instance set *I* 가 solution set {0, 1}에 매핑된다.
</br>
많은 abstract problems는 decision problems이 아니라, optimization problems이다. 하지만 optimization 문제를 decision 문제로 바꾸는 건 그렇게 어렵지 않다.

#### ***Encodings***
컴퓨터가 abstract problem을 풀기 위해서는 problem instances를 프로그램이 이해할 수 있도록 표현해야 한다.
</br>

Encoding of a set S of abstract objects : a mapping *e* from S to the set of binary strings
</br>
***concrete problem*** : instance set이 binary strings의 set인 문제
</br>
길이가 n인 instance i를 가진 concrete problem를 상수 k에 대해 *O(n<sup>k</sup>)* 의 시간 안에 풀 수 있는 알고리즘이 있다면, 해당 concrete problem은 ***polynomial-time solvable***이다.
</br>
</br>
***the complexity class P*** : the set of concrete decision problems that are polynomial-time solvable
</br>
</br>
우리는 abstract problems를 concrete problems으로 매핑하기 위해 encoding을 사용할 수 있다.
</br>
abstract decision problem Q는 instance *I*가 {0, 1}에 매핑되어 있다. Encoding e : *I* &rarr; {0, 1}<sup>*</sup> 는 related concrete problem *e(Q)* 를 만든다. 
</br>
*e<sub>1</sub>* 과 *e<sub>2</sub>* 가 polynomially related encodings on *I*일 때, *e<sub>1</sub>(Q) &isin; P &harr; e<sub>2</sub>(Q) &isin; P* 이다.
</br>
</br>
The standard encoding of an object는 \<>로 감싸서 표현한다. 예를 들어 그래프 G의 standard encoding은 \<G>이다. -->