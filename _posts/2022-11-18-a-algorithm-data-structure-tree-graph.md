---
layout: post
title: "Algorithm data structure tree & graph"
date: 2022-11-18
categories:
  - Algorithm
tags:
  - Javascript
  - Algorithm
  - data structure
  - tree
  - graph
  - root
  - sibling
  - parent node
  - child node
  - leaf node
  - edge
  - connedcted graph
  - depth
  - level
  - height
  - sub tree
  - 자가 균형 이진 탐색 트리
  - AVL 트리
  - 레드-블랙 트리
  - 스플레이 트리
  - 시장 트리
  - 최소 비용 신장 트리
  - B-트리
  - 2-3 트리
  - B+ 트리
  - B\*-트리
  - DSW 알고리즘
  - R-트리
  - 기수 트리
  - 스팁 리스트
  - Binary tree
  - Full binary tree
  - Complete binary tree
  - Perfect binary tree
  - Binary search tree
  - tree traversal
  - preorder traverse
  - inorder traverse
  - postorder traverse
  - levelorder traverse
  - graph
  - vertex
  - adjacent vertex
  - weighted graph
  - unweighted graph
  - undirected graph
  - directed graph
  - in-dgree/ou-degree
  - adjacency
  - self leaf
  - cycle
  - 인접행렬
  - 인접리스트
  - Breadth first search
  - Depth first search
---

언제나 그렇지만 수도코드를 짜는것이 힘든 이유는 한글을 해독하지 못하는것이 크다.

한가지 언어만 잘해도 밥은 먹고산다는데 내가 힘든건 한글을 못해서구나?

다시한번 집중해서 읽은 다음 논리적 접근을 해야된다는 생각이 든 하루

---

## 1. data structure

자료구조는 데이터를 다루는 구조 자체를 뜻한다. 구현에는 제약이 없다.

```
        ㅏ단순구조ㅏbinary
        ㅣ        ㅏinteger/float
        ㅣ        ㅏchar/string
        ㅣ
        ㅏ선형구조ㅏarrayList
        ㅣ        ㅏlinkTheListㅡㅏ단순연결리스트
        ㅣ        ㅏdeck         ㅏ이중연결리스트
자료구조ㅣ         ㅏstack        ㅏ원형연결리스트
        ㅣ        ㅏqueue
        ㅣ                    ㅏ일반트리
        ㅏ비선형구조ㅏtreeㅡㅡㅏ이진트리
        ㅣ          ㅏgraphㅡㅡㅡㅡㅡㅡㅡㅏ방향그래프
        ㅣ                               ㅏ무방향그래프
        ㅏ파일구조ㅏ순차파일
                  ㅏ색인파일
                  ㅏ직접파일
```

## 2. Tree & Graph

### 2.1. Tree

나무를 뒤집었을때 다단계 피라미드처름 생긴 모형을 이룬다.

```
     1          level 1  ㅏsub treeㅓ
     /\                  ㅣ   3    ㅣ
    2  3        level 2  ㅣ   /\   ㅣ
   /\  /\                ㅣ  6  7  ㅣ
  4 5  6 7      level 3  ㅣ  \     ㅣ
 /\     \                ㅏ  10    ㅓ
8 9     10      level 4  ㅏㅡㅡㅡㅡㅓ

- 1: root -> 뿌리
- 2 - 3: sibling -> 형제관계
- 1 - 2: parent node - child node -> 부모 - 자식
   - 1 - 3, 2 - 4...
- 8, 9, 10: leaf node -> 자식이 없는 node
- /, \: edge -> 간선(연결선)
- 1,2,3,4,5,...: node -> 각 데이터
- leaf node -> 자식이 없는 node
```

- node: 트리구조를 이루는 모든 개별 데이터
- root: 트리의 시작이되는 노드
- parent node: 두노드의 상하관계 시 상대적으로 루트에서 가까운 노드
- child node: 두노드의 상하관계 연결 시 루트에서 먼노드
- leaf: 트리의 끝 지점, 자식노드가 없어야함.

단방향 그래프의 하나로, 뿌리하나에서부터 가지가 사방으로 뻗는다.

데이터가 순차적으로 나열된 선형적 구조가 아닌 하나의 데이터에 여러개의 데이터가 존재하므로 비선형적 구조이다.

계층적 구조이기에 cycle은 없다. -> 연결 그래프(Connected Graph)

- 깊이(depth): root부터 하위 계층의 특정 node까지의 depth표현 가능하다. root의 node는 0
- 레벨(level): 같은 depth를 가지고 있는 node를 묶어 level로 표현 가능하다. root level 1, 같은 node 내 depth의 node들의 관계는 sibling(형제)
- 높이(height): leaf node 기준으로 root까지의 높이를 표현 가능하다. 부모노드는 자식노드의 가장 높은 height값에 1을 더한 높이를 가진다. `[8,9,5,10,7] = 0`, `[4,6] = 1`, `[2,3] = 2`, `[1] = 3` 상위 코드블럭 참조
- 서브 트리(sub tree): 큰트리 내부에 트리구조를 갖춘 작은 트리

> 자료의 집합을 구조화, 구조화된걸 표현하는 것이다. 인간이 사용하기에 편리하고 사용하기 좋은것이 자료구조이다.

- 유명한 트리 자료 구조
  - [자가 균형 이진 탐색 트리](https://ko.wikipedia.org/wiki/%EC%9E%90%EA%B0%80_%EA%B7%A0%ED%98%95_%EC%9D%B4%EC%A7%84_%ED%83%90%EC%83%89_%ED%8A%B8%EB%A6%AC)
  - [AVL 트리](https://ko.wikipedia.org/wiki/AVL_%ED%8A%B8%EB%A6%AC)
  - [레드-블랙 트리](https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC)
  - [스플레이 트리](https://box0830.tistory.com/147)
- 기타
  - [신장 트리](https://ko.wikipedia.org/wiki/%EC%8B%A0%EC%9E%A5_%ED%8A%B8%EB%A6%AC), [최소 비용 신장 트리](https://ko.wikipedia.org/wiki/%EC%B5%9C%EC%86%8C_%EB%B9%84%EC%9A%A9_%EC%8B%A0%EC%9E%A5_%ED%8A%B8%EB%A6%AC)
  - [B-트리](https://ko.wikipedia.org/wiki/B-%ED%8A%B8%EB%A6%AC), [2-3 트리](https://en.wikipedia.org/wiki/2%E2%80%933_tree), [B+ 트리](https://ko.wikipedia.org/wiki/B%2B_%ED%8A%B8%EB%A6%AC), [B\*-트리](https://fomaios.tistory.com/entry/Data-Structure-B-Tree%EB%9E%80)
  - [DSW 알고리즘](https://en.wikipedia.org/wiki/Day%E2%80%93Stout%E2%80%93Warren_algorithm)
  - [R-트리](https://ko.wikipedia.org/wiki/R-%ED%8A%B8%EB%A6%AC)
  - [기수 트리](https://en.wikipedia.org/wiki/Radix_tree)
  - [스킵 리스트](https://en.wikipedia.org/wiki/Skip_list)

#### 2.1.1. Binary Tree

이진트리는 자식 노드가 최대 두개인 노드들로 구성된 트리이다. 자료의 삽입, 삭제 방법에 따라 Full binary tree, Complete binary tree, Perfect binary tree로 나뉜다.

```
//정 이진트리
  //각 노드는 0개 혹은 2개의 자식노드를 가짐.
        1
        /\
       2  3
      /\
     4  5

//포화 이진트리
  //정 이진트리인데 완전 이진트리인 경우.
  //모든 리프 노드의 레벨이 동일, 모든 레벨이 채워져있음.
        1
       /\
      2  3
     /\  /\
    4  56  7


//완전 이진트리
  //마지막 레벨을 제외한 모든 노드가 가득 차 있어야함.
  //마지막 레벨의 노드는 전부 차있지 않지만, 왼쪽은 채워져있다.
        1
       /\
      2  3
     /\  /
    4  56
```

##### 2.1.1.1. Binary Search Tree

이진탐색의 효율적인 탐색능력을 유지하면서 빈번한 자료입력과 삭제를 가능하게 만들어진, 이진탐색과 연결리스트가 결합된 이진트리이다.

- 각노드에 중복되지 않는 키가 있다.
- 루트노드의 왼쪽 서브 트리는 해당 노드의 키보다 작은 키를 갖는 노드들로 구성된다.
- 루트노드의 오른쪽 서브트리는 해당 노드의 키보다 큰 키를 갖는 노드들로 구성된다.
- 좌우 서브트리도 모두 이진 탐색 트리이다.

-> 모든 왼쪽 자식의 값이 루트나 부모보다 작고, 모든 오른쪽 자식의 값이 루트나 부모보다 큰 값을 가진다.

```
D(lv 3) < G(lv2) < I(lv3)
        < J(root)
< L(lv3) < O(lv2) < R(lv3)

        J
       /\
      G  O
     /\  /\
    D  IL  R

- 균형잡힌 트리가 이닐 때, 입력되는 값의 순서에 따라
  한쪽으로 노드가 몰리게 될 수 있다. 균형이 잡히지않은 트리는
  탐색 시간이 더 걸리므로 해결해야된다. 이를 위해 삽입과 삭제시
  트리구조를 재조정하는 알고리즘이 추가된다.

- 일반 이진트리보다 탐색이 빠르다.
- 이진탐색트리의 연산은 트리의 높이h, o(h)의 복잡도를 가진다.
        1. 루트노드의 키와 찾고자 하는 값을 비교한다. 찾으면 탐색 종료
        2. 찾는 값이 루트 노드의 키보다 작다면 왼쪽 서브트리 탐색
        3. 찾는 값이 루트 노드보다 크다면 오른쪽 서브트리 탐색
        4. 반복진행, 못찾으면 종료, 최대 트리의 높이(h)만큼 탐색 진행

찾는 값을 제일 먼저 루트의 노드와 비교, 작으면 왼쪽, 크면 오른쪽, 찾으면
종료, 트리안의 값은 높이(h)이하 탐색 이뤄짐

트리안에 찾고자 하는 값이 없어도 최대 h번의 연산 탐색이 진행
```

#### 2.1.2. Tree Traversal

특정 목적을 위해 트리의 모든 노드 한번씩 방문하는것을 트리순회라고 한다.

노드를 순차적으로 조회할때 순서는 왼쪽에서 오른쪽이다.

```
        F
       /\
      B  G
     /\   \
    A  D   I
       /\  /
      C  EH

```

##### 2.1.2.1. preorder traverse

출처: [김로그.github.io](https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/)
![https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/](/assets/img/221118-preorder-traversal.png)

- 노드 방문
- 왼 서브트리 전위 순회
- 오른 서브트리 전위 순회

`F > B > A > D > C > E > G > I > H`

루트에서 시작, 왼쪽 노드들 순차적 순회 후 왼쪽 노드 탐색이 끝나면 오른쪽 탐색한다. 부모노드 먼저 순회하고, 부모 노드가 먼저 생성되야하는 트리를 복사할때 사용한다.

##### 2.1.2.2. inorder traverse

출처: [김로그.github.io](https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/)
![https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/](/assets/img/221118-inorder-traversal.png)

- 왼 서브트리 중위순회
- 노드 방문
- 오른 서브트리 중위순회

`A > B > C > D > E > F > G > H > I`

전위순회가 root가 시작점이라면 중위는 어휘그대로 시작점이 제일 왼쪽 끝에 있는 노드부터 순회한다. root를 기준으로 왼쪽에 있는 노드의 순회가 끝나면, root를 거쳐 오른쪽에 있는 노드로 이도아여 탐색한다. 부모가 서브 트리의 방문 중 방문하는 순회로 이진탐색트리의 오름차순 값을 가져올때 사용한다.

##### 2.1.2.3. postorder traverse

출처: [김로그.github.io](https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/)
![https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/](/assets/img/221118-postorder-traversal.png)

- 왼 서브트리 후위 순회
- 오른 서브트리 후위 순회
- 노드 방문

`A > C > E > D > B > H > I > G > F`

```javascript
// 전위(prefix), 중위(infix), 후위(postfix)에 대응된다.
const traversal = (node) => {
  /* 흐름을보세요
  if(node){
    //visit(node); preorder
    traversal(node->left);
    //visit(node); inorder
    traversal(node->right);
    //visit(node); postorder
  } */
};
```

루트를 가장 마지막에 순회한다. 제일 왼쪽 끝 노드부터 시작으로 루트를 거치지 않고 오른쪽으로 이동해 순회하고, 제일 마지막에 루트를 방문한다. 후위 순회는 트리삭제 시 사용한다. 자식이 먼저 삭제되어야 상위노드를 삭제할 수 있다.

##### 2.1.2.4. levelorder traverse

출처: [김로그.github.io](https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/)
![https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/](/assets/img/221118-levelorder-traversal.png)

root부터 한단계 level 아래로 이동하는모형으로 queue를 이용해 구현할 수 있다.

`F > B > G > A > D > I > C > E > H`

```javascript
const levelorder = (root) => {
  /* 수도코드   
  q <- empty queue
  q.enqueue(root)
  while(not q.isEmpty()){
    node <- q.dequeue()
    visit(node)
    if(node.left !== null)
      q.enqueue(node.left)
    if(node.right !== null)
      q.enqueue(node.right
  } */
};
```

### 2-2. Graph

여러개의 점들이 서로 복잡하게 연결되어 있는 관계를 표현한 자료구조이다.

수학에서 xy축을 중심으로 그리던 그래프가아닌, 컴퓨터사이언스에서 그래프란 웹처럼 여러개의 점들이 선으로 이어져있다.

- 직접적 관계: 두점 사이를 이어주는 선이 있다.
- 간접적 관계: 몇 개의 점과 선에 걸쳐 이어진다.
- 하나의 점
  - vertex(정점)
  - edge(간선)

```
    ㅏ `A`<ㅓ
`B`<ㅓ     ㅣ
    ㅏ>`C`<ㅓ

- 정점 A, B, C
- 1개의 단방향 간선
- 2개의 양방향 간선
```

#### 2-2-1. 용어

- vertex: 정점, node, 데이터가 저장되는 기본 원소
- edge: 간선, 정점간의 관계
- adjacent vertex: 인접 정점: 하나의 정점에서 간선에 의해 직접 연결되어 있는 정점
- weighted graph: 가중치 그래프, 연결강도(추가정보 등)가 얼마나 되는지 적혀져 있는 그래프
- unweighted graph: 비가중치 그래프, 연결의 강도가 적혀져 있지 않은 그래프
- undirected graph: 무방향 그래프, 양방향으로 갈 수 있다.
- directed graph: 유방향 그래프, 단방향으로만 간다.
- in-degree/out-degree: 진입차수/진출차수, 한 정점에 진입하고 진출하는 간선이 몇개인가
- adjacency: 인접, 두 정점간 간선이 직접 이어져 있다면 인접한 정점이다.
- self loop: 자기 루프, 정점에서 진출하는 간선 곧바로 자기 자신에게 진입하는 경우, 다른정점은 거치지 않는다.
- cycle: 한 정점에서 출발하여 다시 돌아온다면 사이클이 있다. 

#### 2.2.2. 인접행렬

정점 두개가 바로 이어져있으면 인접하다 이야기한다. 서로 다른 정점들이 인접한 상태인지를 표시한 행렬로 2차원 배열의 형태로 나타낸다. true(1) 이어졌다, false(0) 이어져있지 않다. 

```
                0  1  2
    ㅏ `0`<ㅓ 0[0, 1, 1]
`1`<ㅓ     ㅣ 1[0, 0, 1]
    ㅏ>`2`<ㅓ 2[1, 1, 0]
```

- 0진출차수 2개
  - 0 -> 1: [0, 1] 
  - 0 -> 2: [0, 2]
- 1진출차수 1개
  - 1 -> 2: [1, 2]
- 2진출차수 2개
  - 2 -> 0: [2, 0]
  - 2 -> 1: [2, 1]

##### 2.2.2.1. usage

- 한개의 큰표와 같은 모습을한 인접행렬은 두 정점 사이에 관계가 있는지, 없는지 확인하기에 용이하다.
- 가장 빠른 경로(shortest path)를 찾고자 할때 주로 이용한다.

- 0 1 2 0 ...
- 0 2 1 0 ...
- 1 2 0 1 ...
- 0 2 1 null
- 2 1 null

#### 2.2.3. 인접 리스트

각 정점이 어떤 정점과 인접하는지를 리스트의 형태로 표현한다. 각 정점마다 하나의 리스트를 가지고 있으며, 이 리스트는 자신과 인접한 다른 정점을 담고 있다.

## 3. BFS & DFS

하나의 정점을 시작하여 모든 정점들을 한번씩 탐색하는 것을 목적으로 한다. 그래프의 데이터는 배열처럼 정렬되어 있지 않아, 원하는 자료를 찾기 위해서는 모두 방문해야 한다.

### 3.1. Breadth-First-Search

너비를 우선적으로 탐색하는 방법이다., 너비우선탐색이라고 하고, 주로 두 정점사이의 최단 경로를 찾을 때 사용한다. 경로를 하나씩 전부 방문한다면, 최악의 경우에는 모든 경로를 다 살펴봐야한다.

- [Tree BFS](https://kimtank.github.io/algorithm/2022/11/10/a-algorithm-bfs-tree.html)

### 3.2. Depth-First Search

하나의 경로를 끝까지 탐색한 후, 다음경로로 넘어가 탐색한다. 하나의 노선을 끝까지 들어가 확인하고 다음으로 넘어가기 때문에 경로를 빨리 찾을 수 있다. 원하는 목적지가 아닌 것을 미리 체크(조건)할 수 있다면, 바로 그 순간 다음 탐색으로 넘어갈 수 있다.

깊이우선탐색은 한 정점에서 시작해 다음 경로로 넘어가기 전 해당 경로를 완벽하게 탐색할 때 사용한다. BFS보다 탐색 시간은 조금 걸릴지라도 모든 노드를 완전히 탐색할 수 있다.

- [Tree DFS](https://kimtank.github.io/algorithm/2022/11/03/b-algorithm-dfs-tree.html)

---

## 참조

> [wiki: tree structure](https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%A6%AC_%EA%B5%AC%EC%A1%B0)  
> [wiki: heap](https://ko.wikipedia.org/wiki/%ED%9E%99)  
> [wiki: linkTheList](https://ko.wikipedia.org/wiki/%EC%97%B0%EA%B2%B0_%EB%A6%AC%EC%8A%A4%ED%8A%B8)  
> [wiki: graph theory](https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%9E%98%ED%94%84_%EC%9D%B4%EB%A1%A0)  
> [이야기박스: splay tree](https://box0830.tistory.com/147)  
> [fomagran: b-tree](https://fomaios.tistory.com/entry/Data-Structure-B-Tree%EB%9E%80)  
> [김로그: bynary tree traveral](https://gnujoow.github.io/ds/2016/09/01/DS4-TreeTraversal/)