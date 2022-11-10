---
layout: post
title: "Tree BFS 순회"
date: 2022-11-10
categories:
- Algorithm
tags:
- Javascript
- Algorithm
- codestates
- Tree
- BFS
- Breadth First Search
---

고민 중간에 해결을 위한 논리까지는 접근했으나, 완성하지는 못하였다. 선입견에 갖혀 어버버했던거 같다.

---

## 0. q

임의의 tree 구성 노드 중 하나를 입력받아 Breadth First Search(BFS: 너비우선탐색)을 한다. 탐색되는 순서대로 노드의 값이 저장된 배열을 리턴한다.

## 1. i

- parameter: Node = { value: number, children: [Node1, Node2...] }

## 2. o

- array

## 3. c

Node, addChild 변경 금지

## 4. io ex

```javascript
let root = new Node(1);
let rootChild1 = root.addChild(new Node(2));
let rootChild2 = root.addChild(new Node(3));
let leaf1 = rootChild1.addChild(new Node(4));
let leaf2 = rootChild1.addChild(new Node(5));
let output = bfs(root);
console.log(output); // --> [1, 2, 3, 4, 5]

leaf1.addChild(new Node(6));
rootChild2.addChild(new Node(7));
output = bfs(root);
console.log(output); // --> [1, 2, 3, 4, 5, 7, 6]

  /**
   *        1
   *      2   3
   *     4 5   6
   *            7
   * dfs: 1,2,4,5,3,6,7
   * bfs: 1,2,3,4,5,6,7
   */

  /**
 *                1
 *          2     3     4
 *        5   6  9 10   13
 *       7   8    11 12
 * 
 *    1,2,3,4,5,6,9,10,13,7,8,11,12
 */
```

## 5. static

```javascript
/// 이 아래 코드는 변경하지 않아도 됩니다. 자유롭게 참고하세요.
let Node = function (value) {
  this.value = value;
  this.children = [];
};

// 위 Node 객체로 구성되는 트리는 매우 단순한 형태의 트리입니다.
// membership check(중복 확인)를 따로 하지 않습니다.
Node.prototype.addChild = function (child) {
  this.children.push(child);
  return child;
};
```

## 6. mine(fail)

```javascript
// # 0. 가정
  // # node를 풀어해쳐서 1차원 배열로 변경
  // # 모든 배열을 1차원 배열로 만들어서 반환

  // ---------------
  // 시도1(실패). 일반적 접근의 경우 child를 넘기면서 dfs로 검색됨
  //첫배열
  if(res === undefined){
    res = [];
    res.push(node.value);
  }
  //자식 있을 때
  if(node.children.length !== 0){
    for(let i = 0; i < node.children.length; i++){
      res.push(node.children[i].value);
    }
  }
  return res;
  // -----------------
  // # 가정2. 0과같은 상상으로 합친다.

  //더이상 반환할 값이 없을때 체크하여 배열 반환
  //if(검증구문)
  //  return arr??
  //합치기
  if(node.children.length !== 0){
  }
  console.log(res);
  for(let i = 0; i < res.length; i++){
    const el = res[i];
    console.log(typeof el);
    console.table(el);
    if(typeof el === 'object'){
      console.log(el.value);
      console.table(el.children);
      if(el.children.length !== 0){
        res = [...res, el.children]
      }
      res[i] = el.value;
    }
  }
  console.log(res);
  //시도 실패 이유는 3번에서 나옴
  //---------------
  // # 시도 3. 동일
  //처음에만 풀어서
  if(!Array.isArray(node)){
    node = [node.value, ...(node.children)];
  }

  const temps = [];
  for(let i = 0; i < node.length; i++){
    if(typeof node[i] === 'object'){
      console.table("node[i]" + node[i]);
      console.table("node[i].children" + node[i].children);
      if(node[i].children.length !== 0){
        for(childNode of node[i].children){
          temps.push(childNode);
        }
      }
      node[i] = node[i].value
    }
  }
  if(temps.length === 0)
    return node;
  node = [...node, temps];
  bfs(node, node);
  //처음 구조분해할당으로 넣어준 ...(node.children이 문제였음)
  // [node.value, [Object], [Object]]로 대입됨, 추후 children을 찾지못함.
```

## 7. reference

구조분해할당을 잘못이해한거같음. 얼른 블로그 재정리 후 이전 정리본과 문서를 보며 재이해의 시간을 가져야할거같다.

```javascript
  //que에 node를 넣음
  let queue = [node];

  //반환할 value의 모음
  const values = [];

  //큐의 길이가 1미만이면 끝
  while (queue.length > 0) {
    //헤드
    const head = queue[0];
    //큐의 앞빼고
    queue = queue.slice(1);
    //헤드의 값을 대입
    values.push(head.value);
    //forEach를 사용해서 queue 반복
    head.children.forEach((child) => queue.push(child));
  }
  //큐에서 모든 값이 다 빠져나왔을 때
  return values;
```

## 8. ref after

그대로 갖다쓴거 같은 이유는 내머리속에 있는 뭔가로 외워버리는게 더 효율적인거 같아서요 ㅜㅜ 내코드를 고집할만한 정당한 이유가 없는거 같아요 주륵..

```javascript
  // # 시도4. 어버버ㅓ법ㅂ버버버 보고도 못풀면 바보
  //parameter를 변경하는게 왠지 잘못된거같지만
  node = [node];
  const res = [];
  while(node.length > 0){
    const head = node[0];
    node = node.slice(1);
    res.push(head.value);
    for(childNode of head.children){
      node.push(childNode);
    }
  }
  return res;
```

## 9. [쉽답니다 이거 쉬운거래요](https://www.geeksforgeeks.org/level-order-tree-traversal/)

쉽대요 쉽대 쉽대요 ㅜㅜ

[wiki: Breadth-first search](https://en.wikipedia.org/wiki/Breadth-first_search)

### 9-1. 재귀 BFS

모든 노드를 순회하는 재귀 함수를 사용하여 트리의 레벨 순서 순회를 인쇄한다. 트리의 높이를 찾고, 깊이를 먼저 검색, 현재 높이를 유지하고 루트에서 1까지의 모든 높이에 대해 노드를 인쇄하고, 현재 높이가 반복의 높이와 같으면 일치시킨다음 노드의 데이터를 인쇄한다.

- counter i에 대해 for loof 실행, 1~h(트리의 높이)까지의 현재 높이
- DFS를 사용하여 트리를 순회하고 현재 노드의 높이를 유지한다.
  - node가 null이면 반환
  - 레벨이 1이면 print(tree->data);
  - 레벨이 1보다 크면
    - tree->left, level-1에 대해 재귀적으로 호출
    - tree->right, level-1에 대해 재귀적으로 호출

```javascript
// Recursive javascript program for level
// order traversal of Binary Tree
 
/* Class containing left and right child of current
   node and key value*/
 class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }
 
    // Root of the Binary Tree
    var root= null;
     
    /* function to print level order traversal of tree */
    function printLevelOrder() {
        var h = height(root);
        var i;
        for (i = 1; i <= h; i++)
            printCurrentLevel(root, i);
    }
 
    /*
     * Compute the "height" of a tree -- the number of nodes along the longest path
     * from the root node down to the farthest leaf node.
     */
    function height(root) {
        if (root == null)
            return 0;
        else {
            /* compute height of each subtree */
            var lheight = height(root.left);
            var rheight = height(root.right);
 
            /* use the larger one */
            if (lheight > rheight)
                return (lheight + 1);
            else
                return (rheight + 1);
        }
    }
 
    /* Print nodes at the current level */
    function printCurrentLevel(root , level) {
        if (root == null)
            return;
        if (level == 1)
            document.write(root.data + " ");
        else if (level > 1) {
            printCurrentLevel(root.left, level - 1);
            printCurrentLevel(root.right, level - 1);
        }
    }
 
    /* Driver program to test above functions */
     
        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
 
       document.write("Level order traversal of  binary tree is ");
       printLevelOrder();
 
// This code is contributed by umadevi9616
```

- output: 1 2 3 4 5
- bigO: O(N<sup>2</sup>), N은 치우친 트리의 노드 수, printLevelOrder()의 시간복잡도는 `O(n) + O(n-1) + ... + O(1)`이고, O(N<sup>2<sup>)이다.
- 보조공간: 최악의 경우 O(N). 비뚤어진 트리의 경우 printGivenLevel()은 호출 스택에 O(n) 공간을 사용한다. 균형 트리의 경우 호출 스택은 O(log n) 공간, 즉 균형 트리의 높이를 사용한다.

### 9-2. 큐를 사용한 BFS

각 노드를 방문한 다음 해당 자식 노드를 FIFO대기열에 넣고, 다시 첫번째 노드를 꺼내고, 자식노드가 FIFO 대기열에 배치되고 대기열이 비워질때까지 반복한다. -> 아마 이 해결법

- 빈 que만들고 q에 root를 push
- q가 빌때까지 While loof 실행
  - temp_node = q.front()를 init, temp_node->data 출력
  - temp_node의 자식인 temp_node->left, temp_node->right q로 push
  - q front node 꺼내기

```javascript
// Iterative Queue based javascript program
// to do level order traversal
// of Binary Tree
 
/* Class to represent Tree node */
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}
 
/* Class to print Level Order Traversal */
    /*
     * Given a binary tree. Print its nodes in level order using array for
     * implementing queue
     */
    function printLevelOrder() {
        var queue = [];
        queue.push(root);
        while (queue.length != 0) {
            /*
             * The shift() method removes the first element from an array and returns that removed element. This method changes the length of the array.
             * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift
             */
            var tempNode = queue.shift();
            document.write(tempNode.data + " ");
 
            /* Enqueue left child */
            if (tempNode.left != null) {
                queue.push(tempNode.left);
            }
 
            /* Enqueue right child */
            if (tempNode.right != null) {
                queue.push(tempNode.right);
            }
        }
    }
 
  /* creating a binary tree and entering the nodes */
        var root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        document.write("Level order traversal of binary tree is - ");
        printLevelOrder();
 
// This code is contributed by umadevi9616
```

- output: 1 2 3 4 5
- bigO: O(N), n은 이진 트리의 노드 수
- 보조 공간: O(N), n은 이진트리의 노드 수

---

## 참조

> [geeksforgeeks: level order tree traversal](https://www.geeksforgeeks.org/level-order-tree-traversal/)   
> [wiki: Breadth-first search](https://en.wikipedia.org/wiki/Breadth-first_search)   
> [geeksforgeeks: dfs](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)