---
layout: post
title: "고차함수 히익"
date: 2022-09-20
categories:
- Algorithm
tags:
- Codestates
- Higher Order Function
- 고차함수
---

대단원의 막이 올랐다. 이때까지는 워밍업이라니. 히익

# 고차함수


## 일급객체(first class citizen)

특별대우를 받는 클라스가다른 객체 -> 함수

- 변수에 assignment(할당) 가능 -> Array[index]?element, Object.key?{value}
- 다른 함수의 argument(전달인자)로 전달 가능
- 다른 함수의 result로 return가능

```javascript
wow();  //할당 전 사용시 ReferError throw

const wow = arg => 'This is me';
wow();  //This is me
```

## 고차함수

함수를 인자로 전달받거나 함수를 결과로 반환하는 함수를 말한다. 다시 말해, 고차 함수는 인자로 받은 함수를 필요한 시점에 호출하거나 클로저를 생성하여 반환한다. [poemWeb]

### 용어

- caller: 다른 함수
- argument: 전달인자
- callback function: 콜러의 인자로 전달되는 함수(답신전화)
- invoke: 호출
- 커링함수: 함수리턴함수의 아버지 `Haskell Curry`, 커링함수를 따로 사용시 고차함수는 `함수를 전달인자로 받는 함수`로 한정, **`고차함수{커링함수}`이게 정확한 표현**

### flow
s2-c1-2

### 예제
s2-c1-2

1. 다른 함수 인자로 받음

2. 함수 리턴

3. 함수 인자 받고, 함수 리턴

## 내장 고차 함수

내장 고차 함수는 여럿이 있음. 그중 일부 대표적인 고차 함수가 배열 메서드들이다.

### .filter()

```javascript
//immutable
let output = arr.filter(조건 true일때 push);
```

### .map()

```javascript
//immutable
let output = arr.map(함수 () return value 지정된다고 표현);
```

### .reduce() -> 응축

```javascript
let output = arr.reduce(initialized 배열의 첫번째, 다음에오는 값);

//배열 문자열화
function connectTrain(train, nextCar) {
  train = train + train.type + '-';
  return train;
}

let cars = [
  { nbr: 10_011, type: 'head' },
  { nbr: 20_110, type: 'body' },
  { nbr: 20_112, type: 'tail' }
];

cars.reduce(connectTrain, '');  //head-body-tail

//배열 객체화
function makeAddressBook(addressBook, user) {
    //분류할 앞글자 분리
  let firstLetter = user.name[0];

    //앞글자가 있으면
  if(firstLetter in addressBook) {
    //앞글자 넣고(key), user(값) 넣고
    addressBook[firstLetter].push(user);
  } else {
    //없으면 만들어서
    addressBook[firstLetter] = [];
    //넣고
    addressBook[firstLetter].push(user);
  }

    반환
  return addressBook;
}

//원본배열
let users = [
  { name: 'Tim', age: 40 },
  { name: 'Satya', age: 30 },
  { name: 'Sundar', age: 50 }
];

users.reduce(makeAddressBook, {});

//예시
{
  T: [
    { name: 'Tim', age: 40 }
  ],
  S: [
    { name: 'Satya', age: 30 },
    { name: 'Sundar', age: 50 }
  ]
}
```


## 고차 함수의 중요성

## 주석
1. 

> ## 참조
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   