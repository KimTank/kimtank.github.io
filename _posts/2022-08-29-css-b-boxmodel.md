---
layout: post
title: "CSS Box Model"
date: 2022-08-27T00:00:00-00:00
categories:
- WebFront
tags:
- CSS
- box-model
- border
- padding
- margin
- display
- relative-unit
- percentage
- em
- rem
---
오늘은 아마 재빨리 끝나면 새벽이지 싶다. CSS는 역시 양이 ~~너무많아서 행볶는다.~~

# CSS Box Model

## The Box Model
- Content Box: 기준이되는 Box
- Padding: Content Box와 Border와의 거리
- Border: Content Box에서 Padding을 띄운 거리
- Margin: Border와 다른 Content Box의 Border와의 거리
- Width: Content Box의 넓이
- Height: Content Box의 높이
> width와 height의 단위: px, em, %, auto

## Border
- Border Width: border의 굵기 제어
- Border Color: border의 색상 제어
- Border Style: border의 모양 제어
  - none
  - hidden
  - dotted
  - dashed
  - solid
  - double
  - groove
  - ridge
  - inset
  - outset
- Border Radius: 모서리의 곡률(px, %)
```css
/* width style color */
border: medium dashed red;
```
원하는 모서리만 골라서 곡률을 제어가능하다.

---
## Padding
```css
/* 속기법 */
/* all */
padding: 5px;

/* vertical horizontal */
padding: 2px 7px;

/* top horizontal bottom */
padding: 1px 2px 3px

/* top right bottom left */
padding: 10px 2px 1px 6px
```
px말고도 여러 단위 사용가능

---

## Margin
속기법은 Padding과 동일

---

## Display Property
MDN문서에 많은 속성이 있으나, 브라우저마다 동작하지 않는 것도 많다.
```html
<!-- 구조대로 출력된다. -->
<h1>나는 블록요소1</h1>
<h1>나는 블록요소2</h1>
<span>나는 인라인요소1</span><span>나는 인라인요소2</span>
```
```css
h1 {
  ...
  /* inline요소인 span같이 inline으로 변경 */
  display: inline;
  ...
}
span{
  ...
  /* block요소인 h1과 같이 block요소로 변경 */
  display: block;
  ...
}

/* Inline요소와 Block요소에서 Width, Height, Padding, Margin의 동작은 상이하다.(특히 inline) */

anytag {
  ...
  /* inline이지만 block처럼 width, height, padding, margin값이 정상작동함. */
  display: inline-block;
  ...
}

wanthide{
  ...
  /* Android View의 visible: gone과 같이 공간과함께 사라진다. */
  display: none;
  ...
}
```

---

## Relative Unit

### percentages: 항상 상대적인 값
```css
/* parnet width, height의 50% 절반 차지 */
parent {
  width: 1000px;
  height: 1000px;
}
child {
  width: 50%;
  height: 50%;
}

/* 특성에 따라 부모가 아닌 요소(ex: font)를 따라가는 것도 있다.*/
any-selector {
  ...
  font-size: 100px;
  /* 부모요소가 아닌 font-size를 기준 절반*/
  line-height: 50%;
  ...
}
```

### em
글꼴의 크기로 box를 제어한다. 대분자 M의 높이, 너비 그리고 타이포그래피와 연관이 있다.
```css
parent {
  font-size: 100px;
}
child {
  /* 부모와 같은 크기(ex: 2em 부모의 2배) */
  font-size: 1em;
}
```

### rem
em의 단점을 보완해서 나온것이다.
```html
<div>
<ul>
  <li>
  A: 나는 부모의 1.5em, 1.5배 커진다.
    <ul>
      <li>나는 부모(A: 1.5em, 1.5배 커짐)보다 또 1.5배 커진다.</li>
    </ul>
  </li>
  <li>A: 나는 부모의 1.5em, 1.5배 커진다.</li>
</ul>
</div>
```
```css
div {
  font-size: 10px
}
ul {
  /* ul의 중첩되어 1.5배 2번 커졌다. 소수점으로가면 0.5 * 0.5배 작아짐 */
  font-size: 1.5em;
}
```
그리하여 나온것이 root html 태그의 font size를 기준으로하는 rem이 나왔다. rem을 사용시 위와같은 중첩문제가 발생하지 않는다. 
> ## 참고
> [MDN:CSS/Box Model](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/The_box_model)   
> [MDN:CSS/Value & Unit](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Values_and_Units)