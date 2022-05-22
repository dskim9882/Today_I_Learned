# ***Queue***
## 정의
한 쪽 끝(rear)에서 삽입, 다른 쪽 끝(front)에서 삭제가 이루어지는 First in-First out(FIFO) 성격의 자료 구조이다.
## Operations
* Enqueue
* Dequeue
* Queue Front
* Queue Rear
## 자료 구조
### Queue Head
```
queueHead
    front
    count
    rear
end queueHead
```
### Queue Node
```
node
    data
    link
end node
```
## 알고리즘
### Create Queue
빈 Queue을 생성한다.
```
createQeueu
    allocate memory for queue head
    set queue count to 0
    set queue front to null
    set queue rear to null
    return queue head
```
### Enqueue
Queue의 rear에 데이터를 삽입한다.
```
enqueue(Queue, dataIn)
    if queue full
        return false
    allocate new node
    store dataIn in new node
    set new node next to null pointer
    if queue empty
        set queue front to address of new data
    else
        set next pointer of rear node to address of new node
    set queue rear to address of new node
    increment queue count
    return true
```
### Dequeue
Queue의 front에 위치한 데이터를 추출한다.
```
dequeue(Queue, dataOut)
    if queue empty
        return false
    move front data to dataOut
    if only 1 node in queue
        set queue rear to null
    set queue front to queue front next
    decrement queue count
    return true
```
### Queue front
Queue의 front에 위치한 데이터를 읽는다.
```
queueFront(Queue, dataOut)
    if queue empty
        return false
    move data at front of queue to dataOut
    return true
```
### Queue Rear
Queue의 rear에 위치한 데이터를 읽는다. 보통의 queue에서는 데이터 접근은 front에서 이루어진다. 해당 Queue는 queueHead의 rear를 통해서 rear에 바로 접근할 수 있다.
```
queueRear(Queue, dataOut)
    if queue empty
        return false
    move data at rear of queue to dataOut
    return true
```
### Empty Queue
Queue가 비어있는 지 여부를 반환한다.
```
emptyQueue(Queue)
    if queue count is 0
        return true
    else
        return false
```
### Full Queue
Queue가 꽉 차있는 지 여부를 반환한다.
```
fullQueue(Queue)
    if memory not available
        return true
    else
        return false
```
### Queue Count
Queue의 데이터 개수를 반환한다.
```
queueCount(Queue)
    return queue count
```
### Destroy Queue
Queue을 삭제한다.
```
destroyQueue(Queue)
    if queue not empty
        loop(queue not empty)
            dequeue(Queue)
    delete queue head
```
## Applications
* categorize data
* queue simulator