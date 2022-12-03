---
layout: post
title: "Truth-y & False-y"
date: 2022-09-10
categories:
  - JavaScript
tags:
  - JavaScript
  - Truth-y
  - False-y
  - if
---

JS를 배우기 전에는 JS는 신기한 언어라고 생각했다. 뭔가 Java나 C와는 다른 부분들이 분명히 존재했고, 그건 각 type에 대해 들여다보다 falsy한 값에 대한 이야기를 들었을때 확 다가왔다. 언제나 그런거지만 내가 설계하고 만든게 아니니 만든사람들이 만든대로 배우고 쓰면서 왜 이게 있을까라고 연구해야한다.

---

## 1. Falsy values

- false
- 0
- -0
- "" (빈문자열)
- null
- undefined
- NaN (Not a Number)
- 0n (BigInt)

## 2. Truthy values

without falsy

## 3. 예제

```javascript
//첫번째 객체 falsy value라면 해당 falsy value 반환
false && "anything"; //false
0 && "anything"; //0
```

## 참조

> [MDN:Falsy](https://developer.mozilla.org/ko/docs/Glossary/Falsy)  
> [MDN:Truthy](https://developer.mozilla.org/ko/docs/Glossary/Truthy)
