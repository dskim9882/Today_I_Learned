# ***General Linear List***
## 정의
General linear list(선형 리스트)는 list의 어느 곳에서든 데이터의 참조, 삽입, 삭제 등의 연산이 가능한 자료 구조이다. Linear list 내의 데이터들은 일정한 순서를 가지고 있어서 Ordered list라고 불리기도 한다.
## Operations
* Insertion
* Deletion
* Retrieval
* Traversal
## 자료 구조
### Head Node
```
list
    count
    head
end list
```
### Data Node
```
node
    data
    link
end node
```
## 알고리즘
### Create List
빈 linear list를 생성한다.
```
createList(list)
    allocate list
    set list head to null
    set list count to 0
```
### Insert List Node
list에서 pPre node의 위치 뒤에 데이터를 삽입한다
```
insertNode(list, pPre, dataIn)
    allocate pNew
    set pNew data to dataIn
    if pPre null
        set pNew link to list head
        set list head to pNew
    else
        set pNew link to pPre link
        set pPre link to pNew
    return true
```
### Deletion List Node
list에서 pLoc node를 삭제한다.
```
deleteNode(list, pPre, pLoc, dataOut)
    move pLoc data to dataOut
    if pPre null
        set list head to pLoc link
    else
        set pPre link to pLoc link
    recycle pLoc
```
### Search List
list 내에 target이 있는지 검색하고, target의 위치나 target이 list에서 위치할 수 있는 위치 정보를 pPre, pLoc를 통해 제공한다. target이 list에 존재하면 true를 반환한다.
```
searchList(list, pPre, pLoc, target)
    set pPre to null
    set pLoc to list head
    loop (pLoc not null AND target > pLoc key)
        set pPre to pLoc
        set pLoc to pLoc link
    if pLoc null
        set found to false
    else
        if target equal pLoc key
            set found to true
        else
            set found to false
    return found
```
### Retrieve List Node
list에서 key 값을 찾고, 발견하면 dataOut을 통해 key값을 내보내고 true를 반환한다.
```
retrieveNode(list, key, dataOut)
    set found to searchList(list, pPre, pLoc, key)
    if found
        move pLoc data to dataOut
    return found
```
### Empty List
list가 비어 있는지 여부를 반환한다.
```
emptyList(list)
    if list count equal to 0
        return true
    else
        return false
```
### Full List
list가 가득 차 있는지 여부를 반환한다.
```
fullList(list)
    if memory full
        return true
    else
        return false
```
### List Count
list의 원소 개수를 반환한다.
```
listCount(list)
    return list count
```
### Traverse List
list를 순회하며 원소에 대해 일을 처리한다. 다음 수도 코드에서는 fromWhere이 가리키는 노드의 다음 순번 노드에 대한 데이터를 읽는다.
```
list
    count
    pos
    head
end list

getNext(list, fromWhere, dataOut)
    if empty list
        return false
    if fromWhere is beginning
        set list pos to list head
        move current list data to dataOut
        return true
    else
        if end of list
            return false
        else
            set list pos to next node
            move current list data to dataOut
            return ture
```
### Destroy List
List를 삭제한다.
```
destroyList(list)
    loop (not at end of list)
        set list head to successor node
        release memory to heap
    set list pos to null
    set list count to 0
```