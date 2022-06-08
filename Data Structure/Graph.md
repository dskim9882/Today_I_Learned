# ***Graph***
## 정의
Graph는 Vertex(or Node)와 Vertex를 잇는 edge(or arc)를 모아 놓은 자료 구조이다.
</br>
*G = (V, E), where V = V(G) = set of vertices & E = E(G) = set of edges*

## 용어 정리
* Edge *e* = (*v, w*)
    * e is incident on v and w.
    * v and w are incident on e.
    * v and w are adjacent vertices.
* Isolated vertex : incident edge가 없는 vertex
* Parallel edges : vertices 한 쌍에 연결된 둘 이상의 edges
* Loops : 시작과 끝이 같은 vertex인 edge
* Directed graph (혹은 digraph) : edge 마다 direction, 즉, 방향성을 가지고 있는 graph이다. 화살표 머리가 successor(후임)을 가리키고 있다. Directed graph의 edge를 arc라고 하기도 한다.
* Undirected graph : edge에 방향성이 없는 graph이다.
* Path : vertices의 sequence인데, path의 각 vertex는 다음 vertex에 인접(adjacent)한다.
* Cycle : 시작과 끝이 같은 vertex이고, 적어도 3 개의 vertices로 구성된 path이다.
* 두 vertices 사이에 path가 있으면, 두 vertices는 **connected** 되어있다
* Graph에서 방향성을 생각하지 않고, 각 vertex간의 path가 존재하면, connected되어 있다고 한다. 
* Strongly connected : directed graph에 모든 vertices들이 connected
    * connected undirected graph에서는 edge들이 양방향 이동이 가능하므로 항상 strongly connected라서 따로 이 개념을 적용하지 않는다.
* Weekly connected : directed graph에서 적어도 두 개의 vertices가 connected되지 않은 경우
* Disjoint graph : not connected
* degree of a vertex : # of lines(edges or arcs) incident on vertex
    * indegree : vertex에서 나가는 방향의 arcs의 개수
    * outdegree : vertex에서 들어오는 방향의 arcs의 개수
* **NOTE** : tree는 각 vertex가 오직 하나의 predecessor를 가지는 graph이다. 그러나 graph는 tree가 아니다. (*T &sub; G*)

## Operations
* Insert vertex
* Delete vertex
* Add edge
* Delete edge
* Find vertex
* Traverse graph
    * [Depth-first traversal](https://github.com/dskim9882/Today_I_Learned/blob/master/Algorithm/DFS.md)
    * [Breadth-first traversal](https://github.com/dskim9882/Today_I_Learned/blob/master/Algorithm/BFS.md)
## Graph Storage Structures
### Adjacency Matrix
Adjacency matrix는 vertices들을 저장할 1차원 배열인 vector 하나와, graph의 edge를 저장할 2차원 배열인 matrix 하나를 사용한다.
</br>
Matrix의 row와 column은 ordered vertices로 labeled된다. 만약 두 vertices 사이에 edge가 있으면 1, 없으면 0을 쓴다.

### Adjacency List
Adjacency list는 vertices들을 저장할 linked list 하나와, arcs를 저장할 2차원 linked list 하나를 사용한다.
## Graph Algorithm
### 자료 구조
Adjancency list로 구현
```
graphHead
    count
    first
end graphHead

graphVertex
    nextVertex
    data
    inDegree
    outDegree
    processed
    firstArc
end graphVertex

graphArc
    destination
    nextArc
end graphArc
```
graphVertex의 processed는 Traversal 연산에서 해당 vertex를 방문했는지는 표시한다.
### Create Graph
```
createGraph
    set count to 0
    set first to null
    return graph head
```
### Insert Vertex
```
insertVertex(graph, dataIn)
    allocate memory for new vertex
    store dataIn in new vertex
    initialize metadata elements in newNode
    if (empty graph)
        set graph first to newNode
    else
        search for insertion point
        if (inserting before first vertex)
            set graph first to new Vertex
        else
            insert new vertex in sequence
```
### Delete Vertex
```
deleteVertex(graph, key)
    if (empty graph)
        return -2
    search for vertex to be deleted
    if (not found)
        return -2
    
    if (vertex inDegree > 0 or vertex outDegree > 0)
        return -1
    delete vertex
    decrement graph count
    return 1
```
### Insert Arc
```
insertArc(graph, fromKey, toKey)
    allcate memory for new arc
    
    search and set fromVertex
    if (from vertex not found)
        return -2
    search and set toVertex
    if (to vertex not found)
        return -3
    
    increment fromVertex outDegree
    increment toVertex inDegree
    set arc destination to toVertex
    if (fromVertex arc list empty)
        set fromVertex firstArc to new arc
        set new arc nextArc to null
        return 1
    
    find insertion point in arc list
    if (insert at beginning of arc list)
        set fromVertex firstArc to new arc
    else 
        insert in arc list
    return 1
```
### Delete Arc
```
deleteArc(graph, fromKey, toKey)
    if (empty graph)
        return -2
    
    search and set fromVertex to vertex with key equal to fromKey
    if (fromVertex not found)
        return -2

    if (fromVertex arc list null)
        return -3
    
    search and find arc with key equal to toKey
    if (toKey not found)
        return -3
    
    set toVertex to arc destination
    delete arc
    decrement fromVertex outDegree
    decrement toVertex inDegree
    return 1
```
### Retrieve Vertex
```
retrieveVertex(graph, key, dataOut)
    if (empty graph)
        return -2
    
    search for vertex
    if (vertex found)
        move locnPtr data to dataOut
        return 1
    else
        return -2
```
### DFS/BFS : TIL - algorithm에 정리되어 있으므로 생략
### Destroy Graph
```
destroyGraph(graph)
    if (empty graph)
        return
    loop (more vertices)
        loop (vertex outDegree > 0)
            delete vertex firstArc
            subtract 1 from vertex outDegree
```