---
layout: post
title: "JavaScript Variable & Boolean"
date: 2022-09-05
categories:
- JavaScript
tags:
- JavaScript
- Variable
- let
- const
- Syntax
- var
- Boolean
---

JavaScript 역시 정해진 문법이 있는 언어이고, 약속과 규칙이 있다. 정해진 문법을 사용해야 원하는 결과를 얻을 수 있다. 그 문법의 기초가 되는 변수를 알아보자

# JavaScript Variable

## Basic Syntax

```javascript
let year = 1986;
// 변수 year를 선언하고 1986이라는 'number' type의 값을 할당하였다.
// ;의 경우 빠질 시 JavaScript가 자동으로 넣어주지만. 명시적으로 넣어주자.
```

## 명명규칙

```javascript
let isTrue; // 낙타법 camelCase 권장, snake_case비권장
//let hello world //띄워쓰기 안됨
//let 1element // 숫자가 맨앞 안됨
let _arg; // 밑줄가능하지만 권장하지 않음
//변수의 이름은 한눈에 알아볼 수 있도록 직관적으로 써야됨.
let isLuckyDay = true;//바로 알아볼 수 있어야 한다.
```

## Variable Update

```javascript
let number = 10;
number = number + 1; //11
nubmer += 1; //12(상기와 동일)

// -= *= /= 가능

number -= 1; //11
number-- //11 업데이트 전의 현재 값을 보여줌(##콘솔에서)
number //10

//JavaScript는 Type이 고정되어 있지 않다.(##주의)
//다른 언어에서 변수 선언 시 type을 지정하여 사용하는 것과 달리
//JavaScript는 변수의 type이 변경될 수 있다.
//이런점이 단점이 될 경우도 있어, addon인 TypeScript가 있다.
number = 'ty'; // type 'string'
number = false; // type 'boolean'
number = 123; // type 'number'
```

## Const

Constant, 상수의 약자

- let과 비슷하게 동작하지만 할당 후 값을 변경할 수 없다.
- 변하지 않는 값을 사용할때 쓰인다.
- const를 쓰면 JavaScript가 업데이트를 막는다. Uncaught TypeError: Assignment to constant variable

## Var

let, const가 나오기전 변수를 선언하는 유일한 방법이었으나, 지금은 권장하지 않는다.

## Boolean(Primitive Type)

true와 false값을 가진다.

### falsy value

- 값이 없다.
- 0
- -0
- null
- false
- NaN
- undefined
- ''(빈문자열)
- "false"(문자열)
- 외 값은 true

### Boolean 객체와 Primitive Type boolean

- (Boolean 객체의 true, false === boolean type의 true, false) => false
- object type의 value가 undefined, null이 아닌 조건문에서는 true(값이 false인 Boolean 객체 포함)

```javascript
let x = new Boolean(false);
if(x){
    //x true로 들어옴
}

let y = false;
if(y){
    //primitive type false는 안들어옴
}

//Boolean이 아닌값을 변환할때 Boolean 객체를 사용하면 안된다. Boolean 함수를 사용해야 한다.
let a = Boolean(expression);    //추천
let b = new Boolean(expression);    //비추천

//값이 false인 Boolean 객체를 포함한 어떤 객체를 Boolean객체의 초기값으로 넘겨주더라도 새로운 Boolean 객체는 true를 가진다.(말이 좀 어려우니 코드 참고)
let booleanObj = new Boolean(false);    //초기값 거짓
let c = Boolean(booleanObj);    //초기값 참
let stringObj = new String('Anything'); //문자열 객체
let d = Boolean(stringObj); //초기값 참

//Boolean primitive value에 Boolean object를 이용하면 안된다.
```

### Constructor

Boolean(): Boolean 객체를 생성한다.

### Instance Method

- Boolean.prototype.toString(): 객체의 값에 따라 문자열 'true'또는 'false'를 반환, Object.prototype.toString() 메서드를 재정의한다.
- Boolean.prototype.valueOf(): Boolean 객체의 원시값(primitive value)을 반환, Object.prototype.valueOf() 메서드 재정의

### Example

```javascript
//false값으로 초기화한 Boolean 객체 만들기
let bNoParam = new Boolean();
let bZero = new Boolean(0);
let bNull = new Boolean(null);
let bEmptyString = new Boolean('');
let bfalse = new Boolean(false);

//true값으로 초기화한 Boolean 객체 만들기
let btrue = new Boolean(true);
let btrueString = new Boolean('true');
let bfalseString = new Boolean('false');
let bSuLin = new Boolean('Su Lin');
let bArrayProto = new Boolean([]);
let bObjProto = new Boolean({});
```

> ## 참고
> [MDN:JavaScript/Grammar&Types/Declarations](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Grammar_and_types#declarations)   
> [MDN:let](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/let)   
> [MDN:const](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/const)   
> [MDN:var](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/var)   
> [MDN:Identifier](https://developer.mozilla.org/ko/docs/Glossary/Identifier)   
> [MDN:Boolean](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Boolean)