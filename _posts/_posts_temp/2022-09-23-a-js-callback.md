---
layout: post
title: "JavaScript Callback Function"
date: 2022-09-23
categories:
- JavaScript
tags:
- JavaScript
- Higher order function
- callback function
---

괴물을 만났다. api를 어렵겠는데요 하더니 30초만에 짜버린다. 따라갈수 없으니 기초부터 잡고 코드리뷰를 해야겠다. 기초를 일단 보자.

# JavaScript Callback Function

1. 고차 함수는 전달인자(argument)로 함수를 넘겨줄 수 있다.(callback)
2. 고차 함수는 다른 함수를 리턴할 수 있다.(커링함수)
3. 함수를 리턴하거나, 함수를 전달인자로 받는 함수를 모두 고차함수라고한다.
4. 고차함수(커링, 콜백, ...)

고차함수에 callback함수 전달 -> if(조건(없을수도있음))고차함수 내 콜백함수 (여러번)(if false면 안)호출(invoke)

과거 api가 없을때 [underscore.js](https://underscorejs.org/), [lodash](https://lodash.com/)같은 라이브러리(배열이나 객체를 다루기위한 라이브러리)를 사용했다. 직접 구현해보고 비교하여 효율적인 코드를 배우자.

## 비동기란

컴퓨터는 큐라던가 스택이라던가 요청처리의 방법이 자료구조에의해 처리되는걸로 배웠었는데, 하나의 작업을 시작하면 다음작업 요청이 대기열에서 기다리고 다음 작업 중 현재 처리되는 작업에는 간섭하지 못하는 **blocking**이 이루어진다고 배운적이 있다.

0번째 작업이 끝나고 다음 1번째 작업이 시작하는 시점이 같은 상황을 **동기적(synchronous)**이라고 한다. 

하지만 현재같이 파이프라인이 하나가 아니라 여러개로 뻗을 수 있게 설계된 지금 시점에서는 작업이 끝날 때 까지 기다릴 필요가 없이 리소스가 넘쳐나니 Node.js를 설계한 선생님도 Node.js를 **non-blocking**하고

> ## 참조  
> []()
> []()
> []()