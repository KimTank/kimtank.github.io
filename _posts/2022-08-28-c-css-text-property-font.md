---
layout: post
title: "CSS text property와 font"
date: 2022-08-28T00:00:00-00:00
categories:
- WebFront
tags:
- CSS
- text-align
- font-weight
- text-decoration
- line-height
- letter-spacing
- font-size
- font-family
---
주말간 CSS를 반응형까지 보려고했었건만 잠드는바람에 늦어졌다. 내일까지 얼마남지않았지만 ~~오늘의 내가 게을러지면 내일의 나는 또 밀릴거니까~~ 얼른하자!!
# CSS text property & font

## properties

### text-align
정렬 => left, right, center, justify
```css
h1 {
  text-align: center;
  width: 50%
}
/* 적용하더라도 <h1>전체가 align으로 움직이지 않는다. */
```

### font-weight
굵기 => normal, bold, lighter, bolder, 100, 900(400 normal, 700 bold)

### text-decoration: 선
```css
tag {
  text-decoration:underline;
  /* 
  - 선종류: underline, line-through, overline
  - text-decoration-style: solid, double, dotted, dashed, wavy
  - 라인굵기도 제어가능
  ---
  text-decoration: underline dotted 4px;
  text-decoration: underline dotted red;
  text-decoration: green wavy underline;
  text-decoration: underline overline #FF28A0;
   */
}
```

### line-height
줄간격을 지정 => normal, 2.5, 3em, 150%, 43px

### letter-spacing
자간 => normal, .2rem, 1px, -1px

## font size
1.2em, x-small, smaller, 12px, 80%\
```css
/* absolute-size */
tag {
  font-size: xx-small;
  /* x-small, small, medium, large, x-large, xx-large, xxx-large */
}
/* relative-size */
tag {
  font-size: smaller;
  /* larger */
}
/* 
- length value
12px
0.8em

- percentage value
80%

- global value
inherit
inital
unset
*/
```
| Relative | Absolute | 
|---|---|
| EM | PX |
| REM | PT |
| VH | CM |
| VW | IN |
| % | MM |
| AND MORE! |  |
> 일반적으로 EM, REM, %로 제어하며, 나머지는 잘 안쓰인다.   
> 반응형웹의 경우 절대값을 안쓴다.

## Font-Family

## 구문
```css
/* font family name % a generic family name  */
font-family: "Goudy Bookletter 1991", sans-serif;

/* a generic family name only */
font-family: serif;
font-family: sans-serif;
font-family: monospace;
font-family: cursive;
font-family: fantasy;
font-family: system-ui;
font-family: ui-serif;
font-family: ui-sans-serif;
font-family: ui-rounded;
font-family: ui-monospace;
font-family: ui-rounded;
font-family: emoji;
font-family: math;
font-family: fangsong;

/* global values */
font-family: inherit;
font-family: initial;
font-family: unset;
```
> font-family stack은 앞에서부터 기기에 있는 font-family를 찾아 순차적으로 명시   
> font-family: a, b, c, d, e, f, g;

> ## 참고
> [MDN:CSS/Reference](https://developer.mozilla.org/ko/docs/Web/CSS/Reference)  
> [MDN:CSS/Font-size](https://developer.mozilla.org/ko/docs/Web/CSS/font-size)   
> [MDN:CSS/Font-family](https://developer.mozilla.org/ko/docs/Web/CSS/font-family)   
> [HTMLcolorCodes/color-names](https://htmlcolorcodes.com/color-names/)
> [CSSfontStack](https://cssfontstack.com)