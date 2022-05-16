# ***Union-Find***
## 정의
Disjoint-set으로도 불리는 자료구조이다.
</br> 공통 원소가 없는 서로소 부분 집합들로 나눠진 원소들의 정보를 저장하고 관리하는 자료구조이다.
</br> MST를 구하기위한 알고리즘인 Kruskal's algorithm을 구현하는 데에 사용된다.
## 연산
1. Make-set : 특정 한 원소만 가지는 집합을 만든다.
2. Find-set : 어떤 원소가 주어졌을 때, 원소가 속한 집합의 대표 원소를 반환한다.
3. Union : 두개의 집합을 하나의 집합으로 합친다.
## 구현 (C++) 
### Array
```c++
void Make_set(int n){
    for(int i = 0; i < n; i++){
        parent[i] = i;
    }
}

int Find_set(int a){
    if(parent[a] == a)
        return a;
    else {
        parent[a] = Find_set(parent[a]);
        return parent[a];
    }
}

void Union_set(int a, int b){
    a = Find_set(a);
    b = Find_set(b);

    if(a != b){
        parent[b] = a;
    }
}
```
### Tree
```c++
struct Disjoint_set{
    struct Disjoint_set *parent;
    int value;
    int rank;
};

vector<struct Disjoint_set*> Make_set(int n, vector<int> &data){
    vector<struct Disjoint_set*> set(n);
    for(int i = 0; i < n; i++){
        set[i] = (struct Disjoint_set*)malloc(sizeof(struct Disjoint_set));
        set[i]->parent = set[i];
        set[i]->value = data[i];
        set[i]->rank = 0;
    }
    return set;
}

struct Disjoint_set* Find_set(struct Disjoint_set *a){
    if(a->parent == a)
        return a;
    else {
        a->parent = Find_set(a->parent);
        return a->parent;
    }
}

void Union_set(struct Disjoint_set *a, struct Disjoint_set *b){
    a = Find_set(a);
    b = Find_set(b);

    if(a != b){
        if(a->rank == b->rank){
            b->parent = a;
            a->rank++;
        } else if(a->rank > b->rank){
            b->parent = a;
        } else {
            a->parent = b;
        }
    }
} 
```