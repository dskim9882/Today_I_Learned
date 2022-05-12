***Dynamic Programming***
==
정의
--
특정 알고리즘이라기보단, programming technique이다.

일반적으로, 분할 정복 문제는 같은 subproblem이 재귀적으로 호출되는 상황에서 매번 다시 subproblem을 풀어야한다는 단점이 있다. 

DP(Dynamic Programming)에서는 한 번 해결한 문제에 대해서 solution을 table에 저장한다.(Memoization) 이 방법으로 하나의 문제에 대해서 한 번만 풀도록 할 수 있다.

---
특징
--
* 최적화 문제에 사용됨
    * Maximization / Minimization
* 4가지 단계
    1. Characterzie the structure of an optimal solution
    2. Recursively define the value of an optimal solution
    3. Compute the value of an optimal solution
    4. Construct an optimal solution from computed information
* Optimal Substructure(최적 부분 구조)
    * 원래 문제에 대한 최적의 솔루션은 하위 문제에 대한 최적의 솔루션을 통합하여 결정된다.
* Top-down, Bottom-up 두 가지 방법으로 구현할 수 있다.
---
Application
--
***Rod Cutting Problem (막대 자르기 문제)***

막대 조각의 길이에 따라 취할 수 있는 수입이 주어졌을 때, 최대 이익을 얻을 수 있는 막대 자르는 방법을 구한다.
</br>단, 막대 자르는 비용은 무료이고 막대 조각의 길이는 항상 정수이다.

* Brute force - 완전 탐색
</br>주어진 막대의 길이가 n이라고 하자. 막대는 한쪽 끝으로부터 1에서 n-1까지 떨어진 부분 마다 자를 수 있다. 따라서 막대를 자를 수 있는 총 경우의 수는 *2<sup>n-1</sup>* 이다.
```c++
/* 
p는 막대 조각의 길이에 따라 얻을 수 있는 수입
n은 막대의 총 길이
*/
// Top-down
int Cut_Rod(vector<int> &p, int n){
    if(n == 0)
        return 0;
    int q = -INF;
    for(int i = 1; i <= n; i++){
        q = max(q, p[i] + Cut_Rod(p, n - i));
    }
    return q;
}
```
* DP
</br>완전 탐색 방법에서는 동일한 subproblem에 대해서 매번 다시 재귀 호출을 해야하기 때문에 비효율적이다. 이를 DP를 통해 해결한다.
```c++
// Top-down with memoization
int Memoized_Cut_Rod(vector<int> &p, int n){
    vector<int> r(n + 1, -INF);
    return Memoized_Cut_Rod_Aux(p, n, r);
}
int Memoized_Cut_Rod_Aux(vector<int> &p, int n, vector<int> &r){
    if(r[n] >= 0)
        return r[n];
    int q = -INF;
    if(n == 0)
        q = 0;
    else{
        for(int i = 1; i <= n; i++){
            q = max(q, p[i] + Memoized_Cut_Rod_Aux(p, n - i, r);
        }
    }
    r[n] = q;
    return q;
}
```
```c++
// Bottom-up
int Bottom_Up_Cut_Rod(vector<int> &p, int n){
    vector<int> r(n + 1);
    for(int j = 1; j <= n; j++){
        int q = -INF;
        for(int i = 1; i <= j; i++){
            q = max(q, p[i] + r[j - i]);
        }
        r[j] = q;
    }
    return r[n];
}
```