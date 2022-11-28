---
layout: post
title: "Node Same Origin Policy"
date: 2022-10-13
categories:
- NodeJS
tags:
- Node
- JavaScript
- Same Origin Policy
- SOP
- origin
---

잠들었다 쇼파에서, 전화왔다 중요한, 낭비했다 3달동안, 흠. 무엇보다 중요한건 그게 아니다. 왜 배운걸 모른다는거다. 주륵. 봐봅시다.

---

## 1. 개념

## 2. like code

```JavaScript
//하위 코드는 내맘대로 적었어요, 전혀 JS React 동작과 연관 없어요 :D
const origin = {
  protocol: 'https://',
  port: '443', // http => 80
  path: 'www.some_of_path',
  endpoint: 'verbs'
};
origin.host = origin[path] + ':' + origin[port];
origin.this = `${origin.protocol}${origin.host}/${origin.endpoint}`;

/**
 * ## 하나라도 다르면 origin(출처) X
 * 1. http(:80) === https(:443) -> false(protocol diff)
 * 2. www.naver.com === www.shopping.naver.com -> false(uri diff)
 * 3. http://path.com === http://path.com:81 -> false(port diff)
 * 4. https://path.com === https://path.com:443 -> true(SAME동일출처)
 * /
```

---

## 3. what?

SOP는 SOP에 잠재적 위험을 분리, 공격받는 경로 줄인다.

## 참조

> [velog:soshin0112/Node.js CORS, SOP](https://velog.io/@soshin0112/Node.js-CORS-SOP-%EA%B0%9C%EB%85%90)