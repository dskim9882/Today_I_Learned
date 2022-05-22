# ***Stack***
## 정의
Top이라고 불리는 한 쪽 끝에서 데이터의 삽입 삭제가 이루어지는 자료구조이다. Last in-First out(LIFO)의 성격을 가진다.
## Operations
* Push
* Pop
* Stack Top
## 자료 구조
### Stack Head
```
stack
    count
    top
end stack
```
### Stack Node
```
node
    data
    link
end node
```
## 알고리즘
### Create Stack
빈 stack을 생성한다.
```
createStack
    allocate memory for stack head
    set count to 0
    set top to null
    return stack head
```
### Push Stack
Stack의 Top에 데이터를 삽입한다.
```
pushStack(Stack, data)
    allocate new node
    store data in new node
    make current top node the second node
    make new node the top
    increment stack count
```
### Pop Stack
Stack의 Top에 위치한 데이터를 추출한다.
```
popStack(Stack, dataOut)
    if stack empty
        set success to false
    else
        set dataOut to data in top node
        make second node the top node
        decrement stack count
        set success to true
    return success
```
### Stack Top
Stack의 top에 위치한 데이터를 읽는다.
```
popStack(Stack, dataOut)
    if stack empty
        set success to false
    else
        set dataOut to data in top node
        set success to true
    return success
```
### Empty Stack
Stack이 비어있는 지 여부를 반환한다.
```
emptyStack(Stack)
    if stack count is 0
        return true
    else
        return false
```
### Full Stack
Stack이 꽉 차있는 지 여부를 반환한다.
```
fullStack(Stack)
    if memory not available
        return true
    else
        return false
```
### Stack Count
Stack의 데이터 개수를 반환한다.
```
stackCount(Stack)
    return stack count
```
### Destroy Stack
Stack을 삭제한다.
```
destroyStack(Stack)
    if stack not empty
        loop(stack not empty)
            popStack(Stack)
    delete stack head
```
## Applications
* Reversing Data : 데이터 순서를 뒤집는 것
* Parsing
* Postponing
* Backtracking