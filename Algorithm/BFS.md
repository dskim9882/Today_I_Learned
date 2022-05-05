***BFS*** 
===
Breadth-First Search / 너비 우선 탐색
--------------------
* 시작 노드에 인접한 노드들 부터 탐색함
* 시작 노드에서 거리가 k인 모든 노드를 탐색해야 k+1만큼 떨어진 노드를 탐색할 수 있음
* 최단 거리 찾기 문제에 활용됨
* * *
특징
----
* 방문한 노드들에 대한 방문 표시가 필요
* 다음 방문 예정 노드들을 Queue에 담아 진행
* * *
알고리즘
---
1. 시작 노드를 Queue에 담는다.
2. Queue에서 노드 하나를 뺀다 (Queue는 FIFO, 즉, 먼저 들어간 노드가 먼저 나온다.)
3. 해당 노드에 대해 일을 처리한다.
4. 방문하지 않은 인접 노드들을 모두 Queue에 담고 방문처리한다.
5. Queue가 비워질 때까지 2 ~ 4번 과정을 반복한다.

* C++ 예시 )
```c++
void BFS(GRAPH graph){
    queue<NODE> q;
    vector<int> check(/*그래프 크기만큼 할당*/);
    q.push(graph.start);// 그래프의 시작 노드를 q에 삽입
    check[graph.start.index] = 1;
    while(!q.empty()){// 큐가 비워질 때까지 반복
        NODE cur = q.front();
        q.pop();
        /* 
        현재 노드 (cur)에 대한 일처리
        */
        for(/* 인접 노드들 모두 둘러보기 */){
            if(check[/* 인접 노드의 index */] == 0){
                q.push(/*방문하지 않은 인접 노드*/); // 방문하지 않은 인접 노드를 Queue에 담음
                check[/* 인접 노드의 index */] = check[cur.index] + 1;// 방문 처리 : true or false로 처리할 수 있지만 지금은 깊이 정보 저장
            }
        }
    }
}
```
* * *
시간복잡도
---
* 인접 리스트로 표현된 그래프 : *O(V + E)*
* 행렬로 표현된 그래프 : *O(N^2)*