---
layout: post
title: "HTML??"
date: 2022-08-26T00:00:00-00:00
categories:
- WebFront
tags:
- HTML
- markuplanguage
---
 말하는것도 좋아하니 글쓰는것도 좋아했던 학생시절이 기억난다. `HTML`에 대한 포스팅을 하려고 어제 `소수` 문제를 풀지 못한 것에 대한 이야기를 하고싶었다. 하지만 어느 순간 `알고리즘`에 대한 포스팅을 해야될거 같은 글을 쓰고 있더라. ~~시간은 유한하고 나는 또 딴짓을 했다~~. **가자!!!**

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
> - [`나무위키:HTML/태그`](https://namu.wiki/w/HTML/%ED%83%9C%EA%B7%B8#%EC%8B%9C%EB%A7%A8%ED%8B%B1%20%ED%83%9C%EA%B7%B8)
> - [`MDN:Sementics`](https://developer.mozilla.org/ko/docs/Glossary/Semantics#html_%EC%8B%9C%EB%A7%A8%ED%8B%B1)
> - [`w3school:HTML Semantic Elements`](https://www.w3schools.com/html/html5_semantic_elements.asp)
> - [`MDN:HTML Element Reference`](https://developer.mozilla.org/ko/docs/Web/HTML/Element)
> - [``](https://developer.mozilla.org/ko/docs/Web/HTML/Element)