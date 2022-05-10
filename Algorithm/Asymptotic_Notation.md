***Asymptotic Notation***
===
Asymptotic (점근적) 
---
*  주어진 값이 커질 수록 어떤 함수나 표현에 가까워지는 것을 말함
> y=(1/x)+x 는 x가 커질 수록 점근선 y=x에 가까워 짐
---
점근적 표기법
---
* 알고리즘의 효율성을 간단히 나타내는 지표
* 다른 알고리즘과 수행능력을 비교하는 데 사용 가능
* Input의 사이즈가 한계치에 있을 때, 알고리즘의 Running time or 메모리 공간 사용량이 얼마나 증가하는 지 나타냄
---
순서
---
점근적 표기법으로 나타낸 time complexity를 비교할 때, n은 충분히 큰 값이어야 함

>*lg n* < *n* < *n lg n* < *n<sup>2* < *n<sup>3* < *2<sup>n* < *n!*
---
O-notation (Upper bounds)
---
*f(n) = O(g(n))*
* Definition of O-notation

*O(g(n)) = {f(n) : there exist positive constants c and n<sub>0</sub> such that 0<=f(n)<=cg(n) for all n >= n<sub>0</sub>}*
> *n<sup>2</sup> + 10n ∈ O(n<sup>2</sup>)*
>> *c =  2, n<sub>0</sub> = 10* or *c =  11, n<sub>0</sub> = 1* or ...
---
&#8486;-notation (Lower bounds)
---
*f(n) = &#8486;(g(n))* 
* Definition of &#8486;-notation

*&#8486;(g(n)) ={f(n) : there exist positive constants c and n<sub>0</sub> such that 0<=cg(n)<=f(n) for all n >= n<sub>0</sub>}*
> *n<sup>2</sup> + 10n ∈ &#8486;(n<sup>2</sup>)*
>> *c =  1, n<sub>0</sub> = 0* or ...
---
&#952;-notation (Tight bounds)
---
*f(n) = &#952;(g(n))* 
* Definition of &#952;-notation

*&#952;(g(n)) ={f(n) : there exist positive constants c<sub>1</sub>, c<sub>2</sub> and n<sub>0</sub> such that 0<=c<sub>1</sub>g(n)<=f(n)<=c<sub>2</sub>g(n) for all n >= n<sub>0</sub>}*

---
[Big-O cheat sheet](https://www.bigocheatsheet.com/)