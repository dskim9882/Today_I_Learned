# ***Heap***
## 정의
왼쪽과 오른쪽의 subtrees가 그들의 parents보다 작은(Max Heap)/큰(Min Heap) 값을 가지는 binary tree이다. 최댓/최솟값을 빠르게 찾아내기 위해 고안된 완전 이진트리 자료구조이다. Binary heap이라고도 한다.
## 종류
### Max Heap
* 부모의 key 값이 자식의 key 보다 큰 heap을 말한다
* Heap에서 가장 큰 값은 Root node에 있다.
### Min Heap
* 부모의 key 값이 자식의 key 보다 작은 heap을 말한다
* Heap에서 가장 작은 값은 Root node에 있다.
## Operation
* Reheap Up
* Reheap Down
* Build a Heap
* Insert a node into a heap
* Delete a node from a heap
* NOTE
    * Heap은 보통 array로 표현된다.
    * Heap이 zero-based array로 표현되어 있고 한 노드의 array index가 n일 때, 자식 노드의 index는 2n+1, 2n+2이다
### Reheap Up
현재 Heap에 있는 마지막 node에 대해 Heap의 속성에 맞는 위치에 놓일 때까지 부모와 비교하여 위치를 바꾸는 연산
* max heap의 수도 코드
```
reheapUp(heap, newNode)
    if (newNode not the root)
        set parent to parent of newNode
        if newNode key > parent key
            exchange newNode and parent
            reheapUp(heap, parent)
```
### Reheap Down
현재 Heap의 Root에 대해 Heap에 속성에 맞는 위치에 놓일 때까지 자식 노드와 비교하여 위치를 바꾸는 연산
* max heap의 수도 코드
```
reheapDown(heap, root, last)
    if there is a left subtree
        set leftKey to left subtree key
        if there is a right subtree
            set rightKey to right subtree key
        else
            set rightKey to null key
        if leftKey > rightKey
            set largeSubtree to left subtree
        else
            set largeSubtree to right subtree
        if root key < largeSubtree key
             exchange root and largeSubtree
             reheapDown (heap, largeSubtree, last)
```
### Build a Heap
주어진 array를 heap의 형태로 만든다
```
buildHeap(heap, size)
    set walker to 1
    loop (walker < size)
        reheapUp(heap, walker)
        increment walker
```
### Insert a node into a heap
Heap의 마지막 부분에 새로운 node를 추가하고 reheap Up을 통해 해당 노드를 알맞은 위치에 배치한다.
```
insertHeap(heap, last, data)
    if (heap full)
        return false
    increment last
    move data to last
    reheapUp(heap, last)
    return true
```
### Delete a node from a heap
Heap의 root node를 추출한다. 그리고 Heap의 마지막 node를 root node로 설정하고 reheap down을 통해 heap을 재정렬한다.
```
deleteHeap(heap, last, dataOut)
    if (heap empty)
        return false
    set dataOut to root
    move last data to root
    decrement last
    reheapDown(heap, 0, last)
    return true
```
## Applications
* Priority Queue : FIFO Queue와 달리, queue에 들어간 순서와 상관없이 key값의 우선 순위대로 나오는 자료구조이다. Heap으로 구현 가능하다.
* Selection Algorithm : 리스트에서 k번째 크거나 작은 data를 찾는 알고리즘에 사용될 수 있다.