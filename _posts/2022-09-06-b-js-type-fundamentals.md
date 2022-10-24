---
layout: post
title: "JavaScript Type & Fundamentals"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Primitive-Types
- Reference-Types
- Fundamentals
- Call-Stack
- Memory-Heap
---

Udemy강의와 Codestates강의를 병행하다보니, 중간중간 정리가 필요하고, 중요하다고 생각되는 부분들의 문서화가 참 시간이 걸리는것같다. 실제로는 내가 볼 내용인데 파고들다 보면 뭔가 다른사람들에게 보여줄 문서를 만들고 있지 않나? 라는 고민을 하지만, 목적은 다시 찾아 봤을때 내가 한눈에 볼 수 있는 정리본을 만드는 거니까. 한번 할때 잘해놔야 두번세번 하지 않는다. 추후에는 최신화가 되었을 시 legacy 내용에 대한 최신화가 필요할뿐.

---

변수에는 하나의 데이터만 담는다.

원시 자료형은 값 자체에 대한 변경이 불가능(immutable)하나, 변수에 다른 데이터는 할당 할 수 있다.   
참조 자료형을 변수에 할당할 때는 변수에 **값이 아닌 주소를 저장**한다. 

```javascript
//원시자료형의 call stack에 바로 저장 call stack & memory heap 참조
let pushCallStack = 10; // call stack에 올라감

const pushMemoryHeap = ['call somewhere'
    , 1
    , {birthday: '1900-09-01'
        , name: 'memoryHeap'
        , [1
            , 3
            , 5
            , 7
        ]
    }
]; // memory heap에 올라가고, 각 값에 담긴 정보의 call stack의 주소값을 참조한다.
```

## JavaScript Memory 시각화

![출처 : MDN](/assets/img/220906-js-memory.png)

## Primitive Data Types

어떤 프로그래밍언어라도 일반적인 타입을 약속으로 정한다.

원시자료형은 고정된 저장 공간을 차지하는 데이터이다. 이와는 다른 개념으로 동적으로 크기가 변화하는 배열과 객체는 참조 자료형(reference data type)이라고 한다. 이는 데이터를 저장하는 방식에 따른 분류이다.

원지자료형에는 할당 될 때 변수의 값(value) 자체가 담기고, 참조 자료형은 할당될 때 보관함의 주소(reference)가 담긴다.

- Number
- String
- Boolean
- Null
- Undefined
- Symbol & BigInt

```javascript
let a = 2;
let b = a;
b = 3;
a;  //3
a === b;    //false
//원시형은 하나의 값만 가진다. 이에 a와 b는 연관이 없는 다른 메모리에 할당된다.
```

## Reference Data Types

Memory Heap에 올라가며, Call Stack에 올라간 변수의 주소값을 저장한다.

JavaScript에서 Primitive Data Type이 아닌 모든 것은 Reference Data Type이다.   이런 자료구조가 나오게 된 이유는 원시타입에 담을 수 있는 메모리적 한계가 있었고, 이것을 csv에서는 (10,20,30...,100)과 같은 형태의 Comma Spread Values로 구분하여 String을 split하던 형식으로 배열을 대신하던 것을 더 편하게 사용하기 위해 JavaScript의 Array와 같이 쉽게 pop(), push(), unshift(), shift()와 같이 구현하였다.

- Array: 배열
- Object: 객체
- Function: 함수

```javascript
let as = [1, 2, 3, 4];
let bs = as;
bs[0] = 10;
as[0];  //10
as === bs;  //true
//참조형의 === (strict equality)는 주소값이 같은지 확인한다.
//Java의 얕은복사와 깊은복사와 같은걸 알아봐야된다.
```

## Call Stack & Memory Heap

상당히 중요한 내용으로 알고 있으면 편리하다.

JavaScript는 고차원 언어답게 GC(Garbage Collector)가 존재한다. 

```javascript
let a = 10; // 원시 자료형은 메모리 콜스택(call stack)에 바로 올린다.

let as = [10, 20, 30]; // 참조 자료형은 메모리힙(memory heap)에 저장된 객체나 배열이 각 변수의 콜스택에 주소를 참조한다.
```

> ## 참조
> [MDN:JS/Type & Data Structure](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)   
> [MDN:JS/Primitive Value](https://developer.mozilla.org/ko/docs/Glossary/Primitive)   
> [MDN:JavaScript/Call Stack](https://developer.mozilla.org/ko/docs/Glossary/Call_stack)   
> [MDN:JavaScript/Memory Management](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_Management)   
> [MDN:JavaScript/EventLoop](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)   
> [Allansendagi:JS Fundamentals/Call Stack & Memory heap](https://medium.com/@allansendagi/javascript-fundamentals-call-stack-and-memory-heap-401eb8713204)   