---
layout: post
title: "JavaScript Scope"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Scope
---

실제로 코드를 만들다 수정을 하게 될 시 스코프를 잘못 지우거나, 추가했을 시 제대로 잡아주지 않으면 계속 에러가 발생한다. 당연히 컴퓨터 입장에서는 내가 이 코드를 어느 범위까지 끝낸 줄 알 수 없으니, 실질적으로는 약속을 위반한 것이다. 우리는 스코프의 사용을 정확하게 하여야 한다. 스코프를 잘못 삽입 및 삭제했다가 코드 자동정렬이라도 했을 때는 생각만해도 끔찍하다.

# JavaScript Scope

## 스코프의 의미와 적용 범위

```javascript
let globalVariable = 10;

{
    let localVariable = 20;
    let globalVariable = 30;
    localVariable;  //20
    globalVariable; //30
}

localVariable;  //Error
globalVariable; //10(아마 에러가나서 멈추지 싶지만)
```

## 변수 별 스코프의 주요 규칙

## 전역 스코프와 지역 스코프의 차이

## block scope와 fuction scope의 차이

## 변수 선언 키워드(let, sonst, var)와 스코프와의 관계

- var: variable에서도 다룬적이 있다. legacy한 변수 선언, 블록 스코프는 무시하고 함수 스코프를 따른다.

```javascript
//var 사용의 위험성
const function() = {
    const arr = [1, 2, 3, 4, 5];
    for (var i  = 0; i < arr.length; i++){
        console.log(`index: ${i}`); //0~5까지 출력
    }
    console.log(`i: ${i}`);// 에러를 내지않고 출력??????
};
```

> 위와 같이 block범위를 벗어나도 같은 function 내에서는 접근이되버린다.   
> 해당 내용의 경우 max는 this지옥을 해방시켜준게 let이라고 설명하였음.

- let: 현재 사용하는 재선언하지 못하는 선언명(재할당은 가능), 블록 스코프를 따르기에 구체적으로 사용가능하고 복잡도를 낮춘다. 권장
- const: 상수의 의미로 재선언 재할당 하지 못하는 선언명

```javascript
var someOne = 'Poe';
var someone = 'Bull';   // 재할당 가능??????????????????
//찾기힘든 버그를 발생시킨다.

let nickName = 'sycor';
let nickName = 'kimtank';  //Error 재선언 방지
nickname = 'kimtank';   //정상

const myName = 'yg';
const myName = 'mg';    //Error 재선언 안됨
myName = 'ty';  //Error 재할당도 안됨.
```

|/|let|const|var|
|---|---|---|---|
|유효범위|블록, 함수|블록, 함수|함수|
|값 재할당|가능|불가능|가능|
|재선언|불가능|불가능|가능|

## 전역 객체란?


> ## 참조
> [MDN:JS/Type & Data Structure](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)   