***Greedy Algorithm***
==
정의
--
최적화 문제에 대한 알고리즘이다.
선택의 시점마다 가장 최적의 선택을 계속 이어가서 최종 해답을 얻고 이 답을 원래 문제의 최적해로 여기는 것이다.
</br>지역적인 최적의 선택을 계속 한다고 해서, 최종적으로 최적해를 구할 수 있다고 단정할 순 없다. 다만, 일부 최적화 문제에 있어서, greedy algorithm을 통해 최적해를 구할 수 있다.
* * *
특징
--
* Greedy Algorithm의 두 가지 중요 요소
    * Greedy-choice property (그리디 선택 특성) : 최종 최적해를 구하기 위해 하는 지역적 최적 선택을 의미
    * Optimal substructure (최적 부분 구조) : Dynamic Programming에서와 마찬가지로 적용되는 요소로써, 최종 최적해가 subproblem의 최적해로 구성되어 있음을 의미
---
Application
--
***Knapsack Problem***
</br>Greedy Algorithm과 Dynamic Programming의 차이점을 보여주기 좋은 문제
</br>
</br>*0-1 knapsack problem*
* n 개의 물건이 있고, 각 물건 i에 대한 무게 w<sub>i</sub>와 가치 v<sub>i</sub>가 주어진다.
* 배낭(knapsack)에 담을 수 있는 총 무게 W가 주어진다.
* 각 물건에 대해 배낭에 담거나 담지 않는 행위만 할 수 있다면,
배낭에 담긴 물건의 총 가치의 합이 가장 높도록 담는 방법을 찾는 문제이다.

</br>*Fractional knapsack problem*
* 0-1 knapsack problem과 같은 물건과, 배낭이 주어진다.
* 다만, 각 물건들에 대해서 일부만 담을 수도 있다.

</br>
"0-1 knapsack problem"에서는 Greedy Algorithm을 적용할 수 없다. 
</br>
</br>"Fractional knapsack problem"는 Greedy algorithm을 적용하여 풀 수 있다.
</br>먼저, 물건들을 가치/무게 비율에 따라 내림차순으로 정렬한다.
이후 greedy choice를 통해 가방에 담을 수 있을 때까지 담으면, 최종적으로 가장 가치가 높도록 담을 수 있다.
