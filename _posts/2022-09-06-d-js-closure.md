---
layout: post
title: "JavaScript Closure"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Closure
---

클로저라는 개념을 전해들었을 때 prototype만큼 중요하단걸 듣고 문서를 들여다보면서 예제를 봤더니 입이 떡 벌어졌다. return문에 함수라니?? 아니 인자에 함수라니??? 익명함수까지는 알겠는데 모듈화가 그 모듈화가 아니었고, 객체가 그 객체와다르고, 캡슐화가 그 캡슐화가 아닌??? 읭???? 처음 Java의 상속과 interface에 대해 공부하다가 쓰레드로 넘어갈때쯤 폭발해버린거같은 느낌이다. 그러다 거의 문서를 다 읽을 즈음 문서 초반에 예제에 var타입을 잘 안쓴다더니 계속 쓴게 MDN문서에 왜 권장하지않는 방식이 나오는거지 라고 생각했던 것이. 대안으로 나오는 let을 쓴다던가. prototype을 사용한다던가? 더 나가서 자세히 설명한 문서를 찾을 수 있었다. 다 읽진못했지만 꼭 이해하고 넘어가야되는거라는건 알겠더라. 일반적으로 DTO를 짤때 나오는 형식을 JavaScript의 방식으로 변경하라면 아직은 감이 안오지만, 더 공부하고 문서를 보고 직접 만들어 구현해보면 이해가 될거라 믿는다. 안되는건 없었다. 못한다고 단정지어 계속 못하는거라 믿었을 뿐이지.

# JavaScript Closure

## MDN의 Closure 정의

함수와 **함수가 선언된 어휘적(lexical)환경**의 조합. 이환경은 클로저가 생성된 시점의 유효 점위 내에 있는 모든 지역 변수로 구성된다.

JavaScript는 함수가 호출되는 환경과 별개로 기존에 선언되어 있던 환경(어휘적 환경)을 기준으로 변수를 조회한다.

**"외부 함수의 변수에 접근할 수 있는 내부 함수"** => closure function

## Closure Function 특징

### 1. 함수를 리턴한다.

```javascript
const addition = (num1, num2) => num + num2;
let add = addition(1, 10);    // 11;

//상기와 같은 결과값 도출
//invocation(함수호출) 2회
const additionClosure = num1 => num2 => num1 - num2;
let addCls = additionClosure(1); // function
addCls(10); // -9

//축약전 모형
const additionBefore = (num) => {
    return (num2) => {
        return num - num2;
    }
}

//Arrow syntax 사용안한 모형
const function additionLegacy(num1) = {
    return function (num2) = {
        return num1 - num2;
    }
}

//closure 형태는 return 값이 함수이다.
typeof add; // 'number'
typeof addCls;  // 'function'
```

### 2. 외부 함수와 내부 함수의 변수 접근법

출처: codestates(문제시 삭제하겠음)

![출처:codestates](/assets/img/220906-closure-1.png)

```javascript
//사용문법이 재밋다.
const add = addr(1)(2); // 3 number type
const fAdd = addr(1);   // function type
```

내부함수는 외부함수에 선언된 변수에 접근 가능하다.

## Closure Function Advanced

### 1. 데이터를 보존하는 함수

일반적으로 다른 언어에서 함수는 지역내 있는 변수들이 실행만되고나면 접근할 수 없다. 관련값을 얻기위해 return한다던가, factorial 형태로 구현하여 .문법으로 재귀적 방법을 사용한다던가의 모형을 가지지 않는이상은 가능하지 않다.

JavaScript의 Closure Function은 외부함수의 실행이 끝나도, 외부 함수 내 변수가 메모리에 저장이 된다.(어휘적 환경을 메모리에 저장한다.)

```javascript
const human = function (name) {
    return function (sex) {
        return `${name}(${sex})`;
    }
}

const firePerson = human('불꽃');  //function type
//함수가 끝나도 fireBoy라는 값을 가진 name 사용가능
firePerson('여자'); // 외부함수 '불꽃의 기존값과 대입한 여자를 가지고 '불꽃여자'
firePerson('남자'); //불꽃(남자)

//tagMaker를 만들어 쓸 수 있음 :D
const tagMK = tag => content => `<${tag}>${content}</${tag}>`;
const header1MK = tagMK(h1); //h1태그 메이커
header1MK('오늘도 열공'); //<h1>오늘도 열공</h1>
```

### 2. 정보의 접근 제한(모듈화)

클로저를 이용해 객체에 담아 여러개의 내부 함수를 리턴한다.

```javascript
//Java에서 public class Human안의 private 변수들을 접근한 수 있는 getter, setter 형식과 비슷하게 구현 가능
//즉 캡슐화와 은닉이 가능하다.
const humanDTO = () => {
    //if(personDTO.getName() === undefined) 사용을위해 undefined로 init
    //올바른 사용인지는 의문..
    let name = undefined;
    let age = undefined;
    //super.name 누군지 모름.
    //this.name 누군지 모름.
    return {
        setName: (pshName) => {
            name = pshName;
        },
        setAge: (pshAge) => {
            age = pshAge;
        },
        //본구문에서 스코프 생략가능한지 모름.
        getName: () => name
        ,
        getAge: () => age
    }
}

const personDTO = humanDTO();

if(personDTO.getName !== undefined)
    personDTO.setName('ty');

if(personDTO.getAge !== undefined)
    personDTO.setAge('99');

personDTO.getName();    // ty
personDTO.getAge(); // 99
//ty(99세)옹인 personDTO만들었음.
//prototype으로 재정의하여 추가되는 객체를 만들어야 하는 것으로 알고 있으나,
//일단 수업중 내용만으로 정리한다.
```

## 이거 재밋는데?

아까 하다보니 img태그를 써보고 싶었고, function이 2번 더 들어간 3개짜리 클로저를 쓰고싶어서 만들어보았다.

```javascript
const tagMaker = tag => isImgTag => content =>
    isImgTag ? `<${tag} src="${content}>"` : `<${tag}>${content}<${tag}>`;

//3단으로 들어가고싶어 isImgTag는 억지부림
const imgMaker = tagMaker('img')(true);
imgMaker('사진주소1');
imgMaker('사진주소2');

const divMaker = tagMaker('div')(false);
divMaker(imgMaker('사진주소3'));
divMaker(tagMaker(h1)(false)('제목입니다.'));
```

> ## 참조
> [WIKI:클로저(컴퓨터 프로그래밍)](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%A1%9C%EC%A0%80_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))   
> [MDN:JS/Closures](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures)   
> [MDN:JS/Inheritance & prototype chain](https://developer.mozilla.org/ko/docs/conflicting/Web/JavaScript/Inheritance_and_the_prototype_chain)   