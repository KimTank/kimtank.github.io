---
layout: post
title: "JavaScript Number & Chrome Console"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Number
- Math-Operation
---

Udemy강의로 Class까지 달릴예정이었으나, 뭔가 이론말고 이전에 풀었던 codestates의 문제를 한번 풀어보자 싶어서 시작한게 계획과는 달리 JavaScript의 Number객체까지 보게되었다. 하지만 언어에대한 이론적 이해도 중요하니 남는 시간에라도 공부하자아앙

# JavaScript Number

JavaScript와 HTML, CSS를 굳이 비교하자면 HTML은 명사, CSS는 형용사, JavaScript는 동사이다.(이거때문에 포스팅을 하기로했다. 너무 마음에드는 비유이다. :D)

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

> ## 참조
> [MDN:JavaScript/Number](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%98%88%EC%A0%9C)