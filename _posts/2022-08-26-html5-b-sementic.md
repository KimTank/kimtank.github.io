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
- sementic element
- emmet
- attribute
---
문서화에서 가장 난감한게 분류이다. 제목을 정하고 문서를 만드는것부터 의외로 시간이 많이 들어간다. 이전 그런 이유로 전직장 **천재팀장**에게 ~~혼난적도 있다.~~ 이번에 시간이 촉박한 상황에서 진행하니 더 그런것들이 와닿는거 같다. ~~재훈아 잘사니?~~ 공부하다 보니 `codestates`의 내용에 더 추가되는 내용들이 있기에 분류를 따로했다.

# HTML sementic

## `HTML5` `sementic`???
 - 의미있는, 의미론적인.
 - `sementic element`없는 과거는 `<div>`의 지옥이었다.
 - `sementic`이 적용된 이후로는 태그가 무엇을 의미하는지 알기 쉬워졌다.~~(없을때보다낫다)~~

## `sementic` 사용이유
- 검색엔진이 시멘틱요소를 우선시(상위노출)한다.(크롤러가 더 쉽게 코드를 알도록)
- 협업 시 `<div>`지옥보다 코드 블록을 찾기 용이하다.(접근성, 스크린리더로 더 쉽게 검색)
- 각 요소 내 데이터 유형 예측이 쉽다.(명시성?)
- 코드를 만드는 주체인 `나`님 `너`님이 더 쉽게 찾을 수 있다.

## `sementic elements`
- `<article>`: 독립적, 자체 포함 콘텐츠 지정, 내용을 그룹으로 묶을때
- `<aside>`: 주요 본문 외 나머지 부분 설명(사이바, 광고창 등)
- `<footer>`: 가장 아랫부분(라이선스, 주소, 연락처 등)
- `<header>`: 가장 윗부분(제목, 상단바, 검색창)
- `<nav>`: `navigation`(상단바 안내`<ul>`보통)
- `<main>`: 주 콘텐츠
- `<section>`: 제네릭한 웹사이트의 독립적인 부분
- `<time>`: 인라인요소로 시간을 표시한다. 기계 판독 가능한 포멧에서는 `datetime` 속성으로 표현한다.
- `<figure>`: 독립적인 부분으로 cation으로 사용한다.

> ### 주의
> `sementic element`는 각각에 의미에 맞게 사용되어야 하기에 오사용하는 유저들이 많다. 정확한 의미를 알고 사용하자.

## emmet
편리한 `도구`로 `vscode`에는 내장되어있어 따로 설치할 필요는없다.
```html
!<!--코드 스니펫 자동완성-->
main>section>h1
<!-- 
  결과물
  <main>
    <section>
      <h1>
      </h1>
    </section>
  </main>
-->
```
> ### 편리한 도구나 라이브러리 api에 관해
> `람다식`을 처음만났을 때와 `안드로이드 데이터바인딩`을 만났을때 느낀 감정(무어야이건!!!???)이겠지만, 해당 새로운 편안한 무언에는 익숙해지기위한 지식과 기초가 필요하다. 무조건 편하니까 이걸 써야되, 남들이 다쓰니까 이걸 써야되가 맞는말일지도 틀린말일지도 모르겠지만, 완전한 사용법을 모르고 사용하는 도구들의 경우에는 레거시한 방법이 더 효율적일때가 많았다. 온전히 선택은 본인이 하는것.
  
### 속성은 뭐야
 - `id`: unique한 이름
 - `class`: 구조화

|HTML|Selector|
|:---:|:---:|
|`<input id="user-name">`|input#user-name|
|`<footer class="global-main>`|footer.global-main|

> 
> ## 참고
> [MDN:Sementics](https://developer.mozilla.org/ko/docs/Glossary/Semantics#html_%EC%8B%9C%EB%A7%A8%ED%8B%B1)
> [w3school:HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)
> [HTML:Spec/LivingStandard](https://html.spec.whatwg.org/)
> [W3:HTML5/char reference](https://dev.w3.org/html/html-author/charref)
> [W3:HTML/entities](https://www.w3big.com/ko/html/html-entities.html#gsc.tab=0)
> [Emmet:doc/cheat-sheet](https://doc.emmet.io/cheat-sheet)