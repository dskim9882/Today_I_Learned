# ***Tree***
## 정의
Non-linear list에서 각 element는 하나 이상의 successor(후임, 후계자)를 가진다. Non-linear list에는 크게 두 가지의 자료 구조가 있는데 하나는 tree, 다른 하나는 graph이다.
<br/>
Tree에서 root를 제외한 각 element는 오직 하나의 predecessor(전임자)를 가진다.
<br/>
Tree는 node라고 불리는 element와 nodes를 연결하는 branch라는 명칭의 directed lines로 구성된다.

## 용어 정리
* degree : node와 관련된 branch의 개수
    * indegree : node로 들어오는 방향의 branch 개수
    * outdegree : node에서 나가는 방향의 branch 개수
    * degree = indegree + outdegree
* leaf : outdegree가 0인 node, 즉, successor가 없는 node
* internal node : root나 leaf가 아닌 node
* parent : outdegree가 1 이상인 node, 즉, successor가 있는 node
* child : indegree가 1 인 node, 즉, predecessor가 있는 node
* siblings : 같은 parent node를 갖는 둘 이상의 nodes
* path : 각 node와 그 node에 인접한 다음 node로 이루어진 node들의 수열
* ancestor : root에서 특정 node n<sub>d</sub>까지의 path가 있을 때, n<sub>d</sub>를 제외한 path에 놓인 모든 node들은 n<sub>d</sub>의 ancestor
* descendent : 어떤 parent node에 대해서 그 아래 놓인 모든 nodes
* level : root에서 node까지 떨어진 거리
    * root의 level은 0
    * root의 children의 level은 1
    * root의 children의 children은 2 ...
    * Siblings은 항상 같은 level에 존재한다.
* height : tree에서 가장 긴 path의 level + 1
* depth : height와 같음, 보통 tree를 도식화할 때, root에서 아래로 내려가며 그리기 때문에 depth라고 표현
* subtree : tree는 subtree로 나눠질 수 있다. subtree의 첫 번째 node가 subtree의 root가 되고, subtree의 이름으로 사용된다.
subtree는 다시 subtree로 나눠질 수 있다.
    * Tree는 비어 있거나 root라고 하는 지정된 node가 있으며, 여기서부터 계층적으로 0개 이상의 subtree가 내려온다. Subtree는 tree이기도 하다.
## Binary Trees
각 node가 최대 두 개의 successors를 가질 수 있는 tree이다.
### Height of Binary trees
Tree를 구성하는 node가 N개 있다고 하자
* *Maximum Height = H<sub>max</sub> = N*
* *Minimum Height = H<sub>min</sub> =* &#8970;*log<sub>2</sub>N*&#8971; *+ 1*
### # of Nodes
Tree의 높이가 H일 때,
* *Minimum Nodes = N<sub>min</sub> = H*
* *Maximum Nodes = N<sub>max</sub> = 2<sup>H</sup> - 1*
### Balance
the balance factor : *B = H<sub>L</sub> - H<sub>R</sub>*
</br>
왼쪽 subtree와 오른쪽 subtree의 높이 차이가 1 이하이면 balanced binary tree이다.
### Binary Tree Traversals
* Depth-first Traversals
![Whiteboard](https://user-images.githubusercontent.com/78060320/169948223-7ae38bb9-2da6-4c4c-9652-a0156a29ca32.png)
    * Preorder Traversal
        ```
        preorder(root)
            if root is null
                process(root)
                preorder(leftSubtree)
                preorder(rightSubtree)
        ```
    * Inorder Traversal
        ```
        inorder(root)
            if root is null
                inorder(leftSubtree)
                process(root)
                inorder(rightSubtree)
        ```
    * Postorder Traversal
        ```
        postorder(root)
            if root is null
                postorder(leftSubtree)
                postorder(rightSubtree)
                process(root)
        ```
* Breadth-first Traversal
    ```
    breadthFirst(root)
        set currentNode to root
        createQueue(bfQueue)
        loop (currentNode not null)
            process(currentNode)
            if left subtree not null
                enqueue(bfQueue, left subtree)
            if right subtree not null
                enqueue(bfQueue, right subtree)
            if not emptyQueue(bfQueue)
                set currentNode to dequeue(bfQueue)
            else
                set currentNode to null
        destroyQueue(bfQueue)
    ```
## General Trees
General tree는 successor의 개수에 제한이 없다.