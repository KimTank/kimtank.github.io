---
layout: post
title: "CSS 구문과 color"
date: 2022-08-28T00:00:00-00:00
categories:
- WebFront
tags:
- CSS
- syntax
- link
- color
- rgb
- hex
- ;
---
Andoid는 xml명세로 이루어진 GUI로 대부분의 뷰를 제어한다. 그래서 CSS와 비슷하면서도 다르지만 더 작은그룹의 정적인 부분이 있어, 대부분 `customView`라든지 `style.xml`을 따로 정의해 구조화하는데 그 방법은 천차만별이다. ~~사실 web frontend에서 가장 무서운 부분은 CSS였다.~~ 그 CSS를 지금 보려한다.

# CSS 구문과 color

## 구문
1. 태그 내에서 사용
```html
<!-- anonymous.html -->
<h1 style="color: white">Hello Ty</h1>
```
2. `<style>`태그로 정의
```html
<!-- anonymous.html -->
<h1>Hello Ty</h1>
<style>
  h1 {
    color: white;
  }
</style>
```

3. `<link>`와 css파일
```html
<!-- anonymous.html -->
<head>
  <title>Document</title>
  <link rel="stylesheet" href="anonymous.css">
</head>
```
> `<link>`의 경우 meta이므로 `<head>`에 위치한다.
```css
/* anonymous.css */
h2 {
  color: green;
}
```

## color 정의법
- color: rebeccapurple;
- color: #00ff00;
- color: rgb(214, 122, 127);
- color: hsl(30, 100%, 50%);
- color: hsla(30, 100%, 50%, .3);
- color: hwb(1.5708rad 20% 10% / 0.7);

## RGB
Red, Green, Blue로 0없다. 255최대

## HEX
- 16진법 0~9 a~f(a==10, f==15), #(해쉬, 옥토토르프, 파운드기호 등)
- #FFFFFF, #000000, #0F55A6
- RGB값이 동일할때 축약가능, #000, #FFF, #A5E
> Decimal: 십진법. 0~9

## ;
CSS에서는 ;은 필수이다. 빠질경우 정상작동안하니 주의(Error 출력안함.)

> ## 참고
> [MDN:CSS/Syntax](https://developer.mozilla.org/ko/docs/Web/CSS/Syntax)  
> [MDN:CSS/Color](https://developer.mozilla.org/ko/docs/Web/CSS/color)   
> [MDN:CSS/Background-color](https://developer.mozilla.org/ko/docs/Web/CSS/background-color)   
> [HTMLcolorCodes/color-names](https://htmlcolorcodes.com/color-names/)