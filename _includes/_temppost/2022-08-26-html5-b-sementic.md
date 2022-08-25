---
layout: post
title: "HTML sementic"
date: 2022-08-26T00:00:00-00:00
categories:
- WebFront
tags:
- HTML
- HTML5
- sementic
---
문서화에서 가장 난감한게 분류이다. 제목을 정하고 문서를 만드는것부터 의외로 시간이 많이 들어간다. 이전 그런 이유로 전직장 **천재팀장**에게 ~~혼난적도 있다.~~ 이번에 시간이 촉박한 상황에서 진행하니 더 그런것들이 와닿는거 같다. ~~재훈아 잘사니?~~ 공부하다 보니 `codestates`의 내용에 더 추가되는 내용들이 있기에 분류를 따로했다.

# HTML sementic

## HTML5??
- HTML을 정의하는 가장 발전된 표준이다.
- HTML이 아닌 기술(3D그래픽 적용된 사이트, 브라우저에서 정보 모을때 도움)을 포함한다.
- HTML5는 새로운 HTML이다.

> - HTML이 upgrade된게 아니라 HTML5 표준에 대한 정의를 바탕으로 각 브라우저 회사들이 HTML5 표준에 맞게 브라우저를 새로 구축한다. => 브라우저가 구현하는 사양의 표준
> - 브라우저에 명시한다고 한들 무언가의 스위치를 on/off하는게 아니라 브라우저에게 알려주는 것이다.

## block vs inline element (div & span)
- `<div>`와 `<span>`은 제네릭 컨테이너이다.
- `<div>`: division, `<div>`태그 내 블록요소를 넣으면 각자가 차지할 수 있는 최소한의 공간을 차지하며 공간을 나눈다.
- `<span>`: 지금 보고 있는 문서에서 인라인에 효과가 들어간 부분들을 css로 제어한다.

## other elements(HR, BR, Sup, Sub)
- `<hr>`: `horzontal rule` 마크다운문법의 `---`처럼 가로 줄을 만들어준다.
- `<br>`: `line break`, `/n`처럼 줄을 바꿔준다.
- `<sup>`, `<sub>`: 윗첨자, 아래첨자

## entities
- `HTML`대신 쓸 수 있는 특별한 코드 또는 시퀀스
- **모든 엔티티 코드는 `&` to `;`**
- 부등호를 `HTML`에 바로 써버리면 동작은 하지만 `IDE`가 태그가 끝나지 않았다고 판단해 포멧이 틀어지는 것과 같은 문제가있다. => `entity`를 쓰면 편안

### `HTML5` in `semantic web` in `semantic element`
 - `sementic`: 의미있는, 의미론적인.
 - `sementic element`없는 과거는 `<div>`의 지옥이었다.
 - #### `sementic` 사용이유
     - 검색엔진이 시멘틱요소를 우선시(상위노출)한다.
     - 협업 시 `<div>`지옥보다 코드 블록을 찾기 용이하다.
     - 각 요소 내 데이터 유형 예측이 쉽다.(명시성?)
 - #### `sementic elements`
   - `<article>`: 독립적, 자체 포함 콘텐츠 지정
   - `<aside>`: 주요 본문 외 나머지 부분 설명(사이바, 광고창 등)
   - `<footer>`: 가장 아랫부분(라이선스, 주소, 연락처 등)
   - `<header>`: 가장 윗부분(제목, 상단바, 검색창)
   - `<nav>`: `navigation`(상단바 안내`<ul>`보통)
   - `<main>`: 주 콘텐츠

### 속성은 뭐야
 - `id`: unique한 이름
 - `class`: 구조화

|HTML|Selector|
|:---:|:---:|
|`<input id="user-name">`|input#user-name|
|`<footer class="global-main>`|footer.global-main|

> 
> ### 참고
> - [`MDN:Sementics`](https://developer.mozilla.org/ko/docs/Glossary/Semantics#html_%EC%8B%9C%EB%A7%A8%ED%8B%B1)
> - [`w3school:HTML Semantic Elements`](https://www.w3schools.com/html/html5_semantic_elements.asp)
> - [`HTML:Spec/LivingStandard`](https://html.spec.whatwg.org/)
> - [`W3:HTML5/char reference`](https://dev.w3.org/html/html-author/charref)
> - [`W3:HTML/entities`](http://www.w3big.com/ko/html/html-entities.html#gsc.tab=0)