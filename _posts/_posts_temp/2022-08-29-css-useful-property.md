---
layout: post
title: "CSS 유용한 속성들"
date: 2022-08-29T00:00:00-00:00
categories:
- WebFront
tags:
- CSS
---
아직 FlexBox ~~근처도 못갓단말~~이야~!~!~!

# HTML Userful Property

## Opacity & Alpha Channel
- Opacity: opacity: 0.5;
- Alpha: rgba(red, green, blue, 0~1(alpha)), Hex값으로 #redGreenBlueAlpha => #0f12a3c5

## Position
박스의 위치를 원하는로 조절할 수 있다.
- position:
  - static; => 고정값이다. 뷰가 고정된다.
  - relative; => 상대적으로 기존뷰를 기준으로 움직인다.
  - absolute; => 문서에서 뷰의 위치가 없어진다.(문서랑 동작예시로 재확인 필요함.)
  - fixed; => 문서에서 뷰의 위치가 없어지고, 부모관계도 사라진다.(브라우저 내 화면에서 offset값대로 움직임), 고정되어 스크롤하여도 화면상 offset준 위치에서 움직이지 않는다.
  - sticky => 상단에 고정되어있다가 스크롤시에 스크롤과함께 스티커처럼 붙어있다 다시 스크롤을 올렸을 때 원래 자리로 돌아간다.

## Transitions
CSS를 사용하여 애니메이션 효과를 줄 수 있다.
```css
.circle{
  width: 100px;
  height: 100px;
  background-color: black;
  /* hover 시 1초동안 변환하는 애니메이션이 나온다. */
  transition: 1s;
}
.circle:hover {
  background-color: yellow;
  border-radius: 50%
}

/* 구문 */
transition: propertyName duration timingFunction delay;

/* 응용 */
.circle{
  width: 100px;
  height: 100px;
  background-color: black;
  /* hover 시 1초동안 변환하는 애니메이션이 나온다. */
  transition: background-color 1s, border-radius 2s;
}
.circle:hover {
  background-color: yellow;
  border-radius: 50%
}

/* timing function */
section div {
  height: 50px;
  width: 50px;
  background-color: magenta;
  margin: 20px 0;
  transition: margin-left 2s;
}
section:hover div {
  margin-left: 100px;
}

  /* 문서확인필요 
  linear, ease-in, steps(number, end), cubic-bezier(.29, 1.01, 1, -0.68) 
  */
```

## Transform
```css
type {
  /* transform-origin: top right; */
  transform: rotate(90deg);
  /* 90도로 돌림 */
}
type {
  /* transform scaleY(2); */
  transform: scaleY(0.5);
}
type {
  /* transform scaleY(2); */
  /* transform translateX(100px); */
  /* 100만큼 이동 X축 음수 반대, Y축 양수 음수*/
  transform: translate(100px, 200px);
  /* xy축 */
}
type {
  /* transform skewX(60deg); */
  /* 60도 기울기 */
  transform: skew(10de, 80dg);
  /* xy축 */
}
type {
  transform: rotate(0.4turn) translateY(40px);
  /* 복합적으로 사용가능 */
}

/* 상기 timing function과 transform을 사용하여 움직이는 동작(애니메이션 가능) */
```



> ## 참조
> [MDN:HTML/table](https://developer.mozilla.org/ko/docs/Web/HTML/Element/table)   
> [MDN:CSS/Transition Timing Function](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function)   
> [Easings](http://easings.net)
> [Unsplash](http://unsplash.com)