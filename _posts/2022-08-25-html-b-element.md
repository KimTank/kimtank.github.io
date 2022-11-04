---
layout: post
title: "HTML element"
date: 2022-08-25T00:00:00-00:00
categories:
- HTML
tags:
- HTML
- HTML element
---

뭔가 한동안 약속이 몰아치더니 조용해졌다. 대신 이전보다 바쁘다. ~~잠을 평소에 2배로 줄였는데도 대체왜???~~ 뭐 일단 어른들 말씀대로라면 바쁜건 한가한거보다 좋은거니 시간배분을 잘해서 더 잘 잘 수 있도록 노력해야겠다. 포스팅 역시 한번에 내용이 몰아치니 보기도 힘들고 나도 힘든거 같아 적절하게 배분하려한다.

-  `HTML`tag 형태는 `Opening Tag`와 `Closing Tag`로 구성된다.
    ```html
    <!-- opening tag ... closing tag -->
       <p>     contents    </p>
    ```
- `<div>`: 한줄을 차지
- `<span>`: 컨텐츠 크기만큼 공간차지
- `<img src="path">`: 이미지 닫는태그가 없어도 된다.
- `<a href="path" target="_blank">`: 링크태그
- `<ul>`,`<li>`,`<ol>`: unordered list, list, ordered list(numbering)
- `<input>`: 입력 폼
- `<textarea>`: 닫기필수, 멀티라인 가능한 textView
  ```html
  <input type="text" placeholder="type">

  <input type="radio" name="choice" value="v1">홍시
  <input type="radio" name="choice" value="v2">깜시

  <input type="checkbox" checked>배고파  

  <textarea name="opinion" cols="20" rows="5"></textarea>
  ```

- `<form>`: 사용자 입력값 전송(회원가입 입력정보 전송 동작)
- `<button>`: 단추

## HTML element
- `<i>`: *italic*
- `<b>`: **bold**
- `<p>`: 단락
- `<h1> to <h6>`: 제목 (1 >to 6 크기)
  - `<h1>`: 페이지에 최상위 주제는 하나지 두개일 수 없음.
  - `<h2> to <h6>`
    ```html
    <!-- 정상적인 문서 -->
    <h1>제목</h1>
    <h2>부제목</h2>
    <h3>부부제목</h3>

    <!-- 비정상적인 문서 -->
    <h1>제목1</h1>
    <h3>부제목</h3>
    <h1>제목2</h1>
    <h2>부제목</h2>

    <!-- 나는 그것도 모르고 개판으로.. -->
    ```

> ## 참조
> [나무위키:HTML/태그](https://namu.wiki/w/HTML/%ED%83%9C%EA%B7%B8#%EC%8B%9C%EB%A7%A8%ED%8B%B1%20%ED%83%9C%EA%B7%B8)   
> [MDN:HTML Element Reference](https://developer.mozilla.org/ko/docs/Web/HTML/Element)