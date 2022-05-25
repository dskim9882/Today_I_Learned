# ***Binary Search Tree***
## 정의
Binary search tree (BST)는 다음과 같은 성질을 가진다.
* 모든 left subtree의 값들은 root의 값보다 작다.
* 모든 right subtree의 값들은 root의 값 이상이다.
* 각각의 subtree는 그 자체로 BST이다.
<center><img src="https://user-images.githubusercontent.com/78060320/170202913-774af3a6-1320-4016-b623-1410f531d99f.png" width="50%" height="50%"></center>

## Operations
* Travesal
* Search
* Insert
* Delete
### Traversal
[Tree](https://github.com/dskim9882/Today_I_Learned/blob/master/Data%20Structure/Tree.md)의 binary tree traversal과 같은 동작이다. 여기서 주목해야 할 점은 **BST를 Inorder travesal**하게 되면 **오름차순 수열**을 얻을 수 있다.
### Searches
다음 3 개의 search algorithm을 알아본다.
* 가장 작은 node 찾기
* 가장 큰 node 찾기
* 원하는 node 찾기 (BST search)
#### 가장 작은 node 찾기
트리에서 가장 왼쪽에 위치한 node가 가장 작은 node이다.
```
findSmallestBST(root)
    if left subtree empty
        return root
    return findSmallestBST(left subtree)
```
#### 가장 큰 node 찾기
트리에서 가장 오른쪽에 위치한 node가 가장 큰 node이다.
```
findLargestBST(root)
    if right subtree empty
        return root
    return findLargestBST(right subtree)
```
#### 원하는 node 찾기 (BST search)
```
searchBST(root, targetKey)
    if empty tree
        return null
    if targetKey < root
        return searchBST(left subtree, targetKey)
    else if targetKey > root
        return searchBST(right subtree, targetKey)
    else
        return root
```
### Insert
새로운 노드는 항상 새로운 leaf node에 저장된다
```
addBST(root, newNode)
    if empty tree
        set root to newNode
        return newNode
    if newNode < root
        return addBST(left subtree, newNode)
    else
        return addBST(right subtree, newNode)
```
### Delete
```
deleteBST(root, dltKey)
    if empty tree
        return false
    if dltKey < root
        return deleteBST(left subtree, dltNode)
    else if dltKey > root
        return deleteBST(right subtree, dltNode)
    else
        if no left subtree
            make right subtree the root
            return true
        else if no right subtree
            make left subtree the root
            return true
        else
            save root in deleteNode
            set largest to largestBST(left subtree)
            move data in largest to deleteNode
            return deleteBST(left subtree of deleteNode, key of largest)
```