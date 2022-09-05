---
layout: post
title: "JavaScript Number"
date: 2022-09-05
categories:
- javaScript
tags:
- javascript
- Primitive-Types
- Chrome
- Console
- Inspect
- Number
- Math-Operation
---

Udemy강의로 Class까지 달릴예정이었으나, 뭔가 이론말고 이전에 풀었던 codestates의 문제를 한번 풀어보자 싶어서 시작한게 계획과는 달리 JavaScript의 Number객체까지 보게되었다. 하지만 언어에대한 이론적 이해도 중요하니 남는 시간에라도 공부하자아앙

# JavaScript

JavaScript와 HTML, CSS를 굳이 비교하자면 HTML은 명사, CSS는 형용사, JavaScript는 동사이다.(이거때문에 포스팅을 하기로했다. 너무 마음에드는 비유이다. :D)

## Running Code in The Console

- Chrome 브라우저의 검사 기능의 콘솔을 이용하여 가장 간단하게 코드를 작동시킬 수 있다.
- 각 os마다 지정된 단축키가 존재하니 확인하고 이용하면 편하다.
- 계속 상주하며 돌아가며 실행되니 단편적이지 않고, 간단한 코드 테스트시 유용하다.
- 창을 분리시켜 사용할 수 있다.
- 콘솔 내용 지우기 clear();, 단축키 ctrl + L(윈도우), cmd + k(mac)

## Primitive Types

어떤 프로그래밍언어라도 일반적인 타입을 약속으로 정한다.

- Number
- String
- Boolean
- Null
- Undefined
- Symbol & BigInt

## Number

- JavaScript는 숫자의 타입이 하나다.
- 양수
- 음수
- 정수
- 소수

```javascript
//콘솔에 입력
1.999999999999999   // 그대로 출력
1.9999999999999999  // 2로 출력
```
> Number는 메모리에서 특정한 양의 공간을 갖게된다. => 무제한의 공간을 차지 할 수 없다.

### Math Operations(산술 연산자)

- 연산자 순서: PEMDAS (Parentheses 괄호) > (Exponent 지수) > (Multiplication 곱하기) > (Division 나누기) > (Addition 더하기) > (Subtraction 빼기)
- % 나머지 연산자(Modulo)
- n % 2 === 0 => 짝수
- n % 2 === 1 => 홀수
- ** 지수연산자

### NaN(Not A Number)

숫자로 간주하지만 숫자가 아닌 무언가를 나타낸다.

```javascript
0/0 //NaN

1 + NaN //NaN

typeof 4 // 'number'

typeof 0/0 // NaN

typeof NaN // 'number'
```

> JavaScript에서 NaN은 숫자지만 실제로는 숫자가 아니다.

> ## 참고
> [MDN:JavaScript/Number](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%98%88%EC%A0%9C)   
> [Chrome:Developer/Devtools/Console](https://developer.chrome.com/docs/devtools/console/)