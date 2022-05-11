***Divide and Conquer***
==
정의
---
Original problem을 여러 subproblems으로 나누고 그 subproblem을 재귀적으로 Solve한다. 그리고 subproblem들의 solutions을 병합하여 original problem에 대한 하나의 solution을 도출한다.

> 쉽게 정리하자면, 재귀적인 호출을 통해서 문제를 나눌 수 있을 만큼 나누어서 각각을 해결하고, 각각의 solution을 합쳐나가는 과정을 거쳐 결국 본 문제의 답안을 도출해내는 알고리즘이다.
---
각 재귀 호출에서 실행하는 3가지 단계
---
1. Divide : 문제가 분할이 가능한 경우, 같은 방식의 재귀 호출을 통해 해결할 수 있는 여러 subproblems으로 분할
2. Conquer : Subproblem들의 solution들을 획득
3. Combine : subproblem들의 solution들을 종합하여 해당 재귀 호출에 대한 Solution을 도출
---
*Application*
--
***Merge Sort***
</br>Input으로 길이가 n인 array가 입력
1. Divide : 길이 n인 array를 n/2인 subarray 두 개로 분할
2. Conquer : 두 개의 subarray를 각각 merge sort로 정렬
3. Combine : 정렬된 두 개의 subarray를 하나의 정렬된 array로 병합

```c++
void Merge(vector<int> &Arr,int p, int q, int r){
    int n1 = q - p + 1;
    int n2 = r - q;
    
    vector<int> L(n1 + 1);
    vector<int> R(n2 + 1);
    for(int i = 0; i < n1; i++){
        L[i] = Arr[p + i];
    }
    for(int i = 0; i < n2; i++){
        R[i] = Arr[q + 1 + i];
    }
    L[n1] = INF;
    R[n2] = INF;
    
    int i = 0;
    int j = 0;
    for(int k = p; k <= r; k++){
        if(L[i] <= R[j]){
            Arr[k] = L[i];
            i++;
        } else {
            Arr[k] = R[j];
            j++;
        }
    }
}

void Merge_Sort(vector<int> &Arr, int p, int r){
    if(p < r){
        q = (p + r) / 2;
        Merge_Sort(Arr, p, q);
        Merge_Sort(Arr, q + 1, r);
        Merge(Arr, p, q, r);
    }
}
```
Recurrence(점화식)
 * The worst-case running time T(n)
>$T(n) = \begin{cases} \theta(1), \;if\;n=1\\ 2T(n/2)+\theta(n), \;if\;n>1\end{cases}$ 

$\\ T(n) = \theta(nlgn)$

</br>***Maximum-Subarray Problem***
</br>Subproblem : A[low ~ high]의 maximum-subarray 찾기

1. Divide : 가능한 같은 사이즈의 두 개의 subarray로 분할
2. Conquer : 각각의 subarray에 대한 maximum-subarray 찾기
3. Combine : subarray에 대한 두 가지 maximum-subarray와 두 subarray의 각각의 일부를 포함하는 maximum-subarray 중 Best solution 하나 선별

```c++
typedef struct maximum_array_info{
    int max_left;
    int max_right;
    int sum;
} MAXIMUM_ARRAY;

MAXIMUM_ARRAY Find_Max_Crossing_Subarray(vector<int> A, int low, int mid, int high){
    MAXIMUM_ARRAY maxArr;
    int left_sum = -INF;
    int sum = 0;
    for(int i = mid; i >= low; i--){
        sum += A[i];
        if(sum > left_sum){
            left_sum = sum;
            maxArr.max_left = i;
        }
    }
    
    int right_sum = -INF;
    sum = 0;
    for(int j = mid + 1; j <= high; j++){
        sum += A[j];
        if(sum > right_sum){
            right_sum = sum;
            maxArr.max_right = j;
        }
    }
    maxArr.sum = left_sum + right_sum;
    return maxArr;
}

MAXIMUM_ARRAY Find_Maximum_Subarray(vector<int> A, int low, int high){
    MAXIMUM_ARRAY maxArr;
    if(low == high){
        maxArr.max_left = low;
        maxArr.max_right = high;
        maxArr.sum = A[low];
    } else {
        MAXIMUM_ARRAY leftMaxArr;
        MAXIMUM_ARRAY rightMaxArr;
        MAXIMUM_ARRAY crossMaxArr;
        int mid = (low + high) / 2;
        leftMaxArr = Find_Maximum_Subarray(A, low, mid);
        rightMaxArr = Find_Maximum_Subarray(A, mid + 1, high);
        crossMaxArr = Find_Max_Crossing_Subarray(A, low, mid, high);
        if(leftMaxArr.sum >= rightMaxArr.sum && leftMaxArr.sum >= crossMaxArr.sum)
            maxArr = leftMaxArr;
        else if(rightMaxArr.sum >= leftMaxArr.sum && rightMaxArr.sum >= crossMaxArr.sum)
            maxArr = rightMaxArr;
        else
            maxarr = crossMaxArr;
    }

    return maxArr;
}
```
Recurrence(점화식)
 * The worst-case running time T(n)
>$T(n) = \begin{cases} \theta(1), \;if\;n=1\\ 2T(n/2)+\theta(n), \;if\;n>1\end{cases}$ 

$\\ T(n) = \theta(nlgn)$