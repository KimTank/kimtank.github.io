---
layout: post
title: "CSS Layout Reset"
date: 2022-09-15
categories:
  - CSS
tags:
  - CSS
  - Layout Reset
  - box-sizing
  - border-box
---

역시 사람은 같은 실수를 여러번 반복한다. 그래서 메모가 중요하다.

---

## 1. Layout Reset

HTML 브라우저에따라 기본 스타일이 다 상이하게 적용된다. 하여 원하는 디자인을 뽑기위해서는 레이아웃을 초기화시켜줘야한다.

## 2. 필요성

- 박스의 시작을 0,0 시작하고 싶어
- width, height 계산에 여백이 포함되어있지 않아
- 브라우저에따라 여백이나 글꼴이 다 달라

[Normalize.css](http://necolas.github.io/normalize.css/)가 존재하지만 쓰지 않아도 된다.

## 3. 예제

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
}
```

> 블로깅을 해놓은줄 알았는데 안해놓은건지? 해놨는데 못찾는건지 Jekyll 검색기능 빨리 넣어야겠다 ㄷㄷ

## 참조

> [MDN/DesignGuide/CSS](https://developer.mozilla.org/ko/docs/MDN/Writing_guidelines/Writing_style_guide/Code_style_guide/CSS)
