---
layout: post
title: "보류류류JavaScript Boolean Logic"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Comparisons
---

# JavaScript Boolean Logic

## Comparisons

비교연산자로 조건문으로 제어할때 자주 사용한다.

- `>`: greater than
- `<`: less than
- `>=`: greater than or equal to
- `<=`: less than or equal to
- `==`: equality
- `!=`: not equal
- `===`: strict equality
- `!==`: strict non-equality

> 문자나 문자열을 비교할때는 조심해야한다. Unicode값에 따라 비교연산자를 썻을 때 원하지 않는 결과를 가져올 수 있다.

## `==` & `===`

이중 등호와 삼중등호, 앞을 `!=`, `!==`을 붙일 경우 Not연산으로 변경

- `==`: 값이 같은지 비교한다. type은 비교하지 않는다. 두값을 같은 타입으로 강제로 변환한 뒤 비교한다. 원하지 않는 결과를 가지고 올 수 있다.

```javascript
5 == 5; // true
'b' == 'c'; // false
7 == '7';   // true
0 == '';    // true
0 == false; // true
null == undefined   // true
```

- `===`: type도 같은지 비교한다. type이 엄격한 비교등호이다.




> ## 참조
> []()   