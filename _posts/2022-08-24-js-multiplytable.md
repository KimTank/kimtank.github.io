---
layout: post
title: "JavaScript multiplyTable"
date: 2022-08-24T00:00:00-00:00
categories:
- JavaScript
tags:
- JavaScript
- multifly table
---
`코드스테이츠`의 간단한 구구단 구현을 하다 딴길로 세어 결국 검증부터 n개의 값이 들어갔을때 작동하는 코드를 만들기위해 삽질을 했다. ~~무려 한시간동안~~ :D

# 구구단만들기!!
## 원래 원하던 결과물
```javascript
let mutiplyTable = number => {
  console.log(number * 1);
  //... 2~8중략
  console.log(number * 9);
};
```
## 템플릿 리터럴로 표현하고 싶어
```javascript
let mutiplyTable = number => {
  console.log(`${number} * 1 = ${number * 1}`);
  //... 2~8중략
  console.log(`${number} * 9 = ${number * 9}`);
};
```
## 역시 반복문을 써야 편할거야
```javascript
let mutiplyTable = number => {
  for(let i = 0; i < 10; i++)
  console.log(`${number} * ${i+1} = ${number * (i+1)}`);
};
```
## 나머지매개변수로 n개의 매개변수를 넘겨보고 싶어
이때부터 ~~삽질이 시작되었다.~~ `foreach`도 쓰고싶고 args배열의 체인으로 나오는 `for loof`도 써보고 싶었다. 욕심이 과했다.

`forEach`의 경우 `continue`를 어떻게하는지 검색한 후 `filter`를 찾았지만, `filter`내에서 검증이후 문구출력을 하는법을 몰라서 ~~시간날때 손대기로했다(과연?).~~

`for loof`는 내가 원하던 그 편안함 :D
```javascript
const mulTablePrinter = (...args) => {
    for (let arg of args) {
        let number;
        //검증
        if(!(typeof arg === 'number')){
            console.log(`${arg}는(은) 숫자가 아닙니다.`);
            console.log('-----------------------');
            continue;
        }
        if(!(arg > 0 && arg < 10)){
            console.log(`${arg}는 구구단(1~9)이 아닙니다.`);
            console.log('-----------------------');
            continue;
        }
        number = arg;
        console.log(`${number}단 구구단`);
        //실제 출력구문 
        for (let i = 0; i < 9; i++) { 
            console.log(`${number} * ${i+1} = ${number * i+1}`);
        };
        console.log('-----------------------');
    };
};
```
> **출력값**   
> mulTablePrinter(1, 'ss', 1919)   
> VM1347:16 1단 구구단   
> VM1347:19 1 * 1 = 1   
> VM1347:19 1 * 2 = 2   
> VM1347:19 1 * 3 = 3   
> VM1347:19 1 * 4 = 4   
> VM1347:19 1 * 5 = 5   
> VM1347:19 1 * 6 = 6   
> VM1347:19 1 * 7 = 7   
> VM1347:19 1 * 8 = 8   
> VM1347:19 1 * 9 = 9   
> VM1347:21 -----------------------   
> VM1347:6 ss는(은) 숫자가 아닙니다.   
> VM1347:7 -----------------------   
> VM1347:11 1919는 구구단(1~9)이 아닙니다.   
> VM1347:12 -----------------------   

사실 상위 코드가 나오기까지 쓸데없는 구문과 변수를 잘못 대입해 결과물을 원하는대로 얻지 못하는 실수가 계속 있었고, 나는 시간을 잘 조율하지 못하고 단지 디버깅하는 재미로 코드를 생각없이 막 짜고 있었다.

~~변탠가?~~

결국 실습과정에서 끝까지 읽어보지도 않고 한 결과 `템플릿 리터럴`도 마지막에 사용하라고 되어있었고, `2중 for문`도 구현해보자 라고 되어있더라...

뭐한걸까??~~(하지만 재밋었다, 좋은 구구단이었다.)~~

^^ 이제는 시킨거라도 잘해야지

> ## 참조
> [MDN:JavaScript/for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)   
> [MDN:JavaScript/forEach](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)   
> [MDN:JavaScript/rest parameters](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)   
> [MDN:JavaScript/instanceof](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/instanceof)   
> [MDN:JavaScript/addition assignment](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Addition_assignment)