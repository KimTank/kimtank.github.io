---
layout: post
title: "Algorithm data structure stack & queue"
date: 2022-11-17
categories:
  - Algorithm
tags:
  - Javascript
  - Algorithm
  - data structure
  - stack
  - queue
  - First In Last Out
  - Last In First Out
  - Fist In Fist Out
  - Last In Last Out
  - Circular Queue
---

기피해오던 알고리즘의 이론.

뭐든 알면 쉽고 모르면 알고싶지않다. 일단 알아보자

---

## 1. data structure

여러 데이터의 bundle을 저장하고, 사용하는 방법을 정의한 것이다. data는 실생활을 구성하고 있는 모든 정보값이다. 데이터는 분석하고 정리하여 활용해야만 의미를 가진다. 필요에 따라 데이터의 특징을 분석하여 정리하고 활용할 필요가 있다. 데이터는 하나의 구조로만 정리하고 활용하는 것이 아닌, 체계적으로 관리하여 저장하는 과거 현인들의 방식을 알아야한다.

> 자료구조는 데이터를 다루는 구조 자체를 뜻한다. 구현에는 제약이 없다.

```
        ㅏ단순구조ㅏbinary
        ㅣ        ㅏinteger/float
        ㅣ        ㅏchar/string
        ㅣ
        ㅏ선형구조ㅏarrayList
        ㅣ        ㅏlinkTheListㅡㅏ단순연결리스트
        ㅣ        ㅏdeck         ㅏ이중연결리스트
자료구조ㅣ         ㅏstack        ㅏ원형연결리스트
        ㅣ        ㅏque
        ㅣ                    ㅏ일반트리
        ㅏ비선형구조ㅏtreeㅡㅡㅏ이진트리
        ㅣ          ㅏgraphㅡㅡㅡㅡㅡㅡㅡㅏ방향그래프
        ㅣ                               ㅏ무방향그래프
        ㅏ파일구조ㅏ순차파일
                  ㅏ색인파일
                  ㅏ직접파일
```

## 2. Stack & Que

### 2.1. Stack

선입후출 Last In First Out 으로 외웠던 순서대로 쌓이고, 쌓인 가장 마지막 스택이 먼저 나가는 구조. FILO

- push(넣고): a b c d
- pop(빼고): d c b a

조회가 필요없고 저장 검색의 과정이 매우 빠르다. 최상위 공간에 데이터를 저장하고 검색하면 된다.

#### 2.1.1. 특징

1. 데이터는 하나만: 여러개는 안된다.
2. 입출력방향: one way, 여러개면 안된다.
3. 데이터는 유한하고 정적: 콜스택 함수 실행데이터 스택의 프레임으로 저장된다. 함수가 새 변수를 선언시마다 스택 최상위로 push된다. 다음 함수가 종료될 시 최상위는 지워진다. 이에 해당 함수로 스택에 들어간 모든 변수는 삭제된다. 정적 특성을 가져야만 컴파일 시간을 결정할 수 있다.
   - local variable: value type, primitive, primitive constant
   - pointer
   - function frame
4. 스택크기 제한: heap에 비해서는 스택의 크기가 제한되어있다. stack overflow조심

### 2.2. Queue

선입선출 First In First Out, 먼저 들어간것이 먼저 나간다. 줄을 서서 기다리는 대기행렬이다. LILO. 입출력의 방향이 고정되어있다. 두곳에서 접근 가능하다.

- enqueue(넣고): a b c d
- dequeue(빼고): a b c d

각 장치사이 존재하는 속도의 차이, 시간 차이를 해결하기 위해 임시 기억 장치의 자료구조는 Queue로 되어있다. buffer라고하며, 컴퓨터장치에서 발생하는 이벤트가 불규칙하다. 연산장치인 cpu가 일정한 속도로 처리하기 위해, 발생한 불규칙한 이벤트를 buffer를 통해 처리한다.

컴퓨터와 일반 장치의 데이터 통신

- 장치는 속도가 느리다.
- cpu는 장치에 비해서 빠르다(항상그렇지않을 수 있음)
- cpu는 data를 만들어 queue에 저장하고 다른 작업 수행, 장치는 queue에서 data받아서 동작

#### 2.2.1. 특징

1. 하나씩 가능: 여러개 안된다.
2. 입출력방향 두개: 입출력 방향은 다르다. 하지만 만약에 입출력방향이 같으면 Queue가 아니다.

#### 2.2.2. 추가 확장 Circular Queue data structure

- [Circular Queue Data Structure](https://www.programiz.com/dsa/circular-queue)
- [Circular Queue](https://jetalog.net/119)

---

## 참조

> [알고리즘 시각화 사이트(cs)](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)  
> [알고리즘 시각화 사이트(visualgo)](https://visualgo.net/en/list?slide=2-8)  
> [programiz: circular queue](https://www.programiz.com/dsa/circular-queue)  
> [jetalog: circular queue](https://jetalog.net/119)
