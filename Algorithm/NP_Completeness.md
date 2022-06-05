# ***NP-Completeness***
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
</br> 문제는 P = NP의 관계가 성립하는 가에 있다.

### NPC
NP-Completeness(NPC)는 NP문제에 속하고, NP에 있는 어느 문제만큼 난해한 문제(NP-Hard)이다. 
#### Decision problems vs. optimization problems
NP-completeness는 optimization problem이 아니라 decision problems에 직접 적용한다. 
* Decision problems는 optimization problems보다 더 쉽다(easier), 혹은 적어도 더 어렵진 않다(at least no harder).
* 만약 한 optimization problem이 쉽다면, 이와 관련된 decision problem은 쉽다.
* 만약 한 decision problem이 어렵다는 증거가 있다면, 이와 관련된 optimization problem은 어렵다는 증거가 된다.
#### Reductions
Polynomial time으로 해결하고 싶은 decision problem A가 있다. 그리고 polynomial time으로 푸는 방법을 알고 있는 decision problem B가 있다.
</br></br> 특정 문제의 input을 그 문제의 instance라고 한다. polynomial-time reduction algorithm은 A의 instance &alpha;를 B의 instance &beta;로 두 가지 특징에 따라 변형시키는 절차이다. 두 가지 특징은 다음과 같다.

* 변형 과정은 polynomial time이 걸린다. 
* 두 답은 같다. 즉, &alpha;의 답이 yes &harr; &beta;의 답이 yes
 <center><img src="https://user-images.githubusercontent.com/78060320/172054762-726f9d2e-c0f2-4fac-9aaa-c026a7f3d0f9.png" width="100%" height="100%"></center>

A 문제를 B문제로 환원(reducing)함으로써 A의 easiness를 증명하는데 B의 easiness를 사용한다.

#### A first NP-Complete problem
Reduction은 어떤 NP-Complete problem을 증명하기 위해서 이미 NP-Complete라고 알려진 문제를 갖는 것에 의존하기 때문에, "first" NP-Complete 문제가 필요하다.