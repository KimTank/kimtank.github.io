---
layout: post
title: "CSS Responsive Design & Media Queries"
date: 2022-08-30
categories:
- WebFront
tags:
- CSS
- Media
- Media-Queries
---
컴퓨터가 처음나왔을 때는 display라는게 없었고, 출력과 입력만 가능했다. 그러다 display가 출시되고, 컴퓨터는 화면을 가지게 되었고, 그 화면은 dos부터 윈도우3.1의 탄생으로 시작하여 macos등 발전했다. 화면은 대부분 정해져 있었고, 스마트폰이 대중화되기 전에는 여러가지 화면을 고려하지 않아도 가능했다. 하지만 생각해보라, 우리가 주변에서 차고다니는 스마트워치조차 화면을 고려해야되는 아주 고도화된 시대에 들어오게 된것이다. ~~아아아아아아악~~

# CSS Responsive Design & Media Queries

## Responsive Design
현재 2022에는 시계에도 우리가 화면을 고려하여 디자인하는 시대가 왔다. 불과 몇년전만 하더라도 웹사이트는 데스크탑용과 모바일용을 따로 구축하여 서비스하였다. 그 둘은 완전 분리된 다른 개념이였다.   
현재를 생각해보자. 우리가 일반적으로 사용하는 기기들은 화면이 다양하고, 사용하는 기기의 화면 크기에 따라 반응하는 웹사이트를 만드는것이다. 기마다 다른 레이아웃을 지원해야한다. 이런 반응형 디자인이 대중화된 것은 불과 7~8년 전이다.

## Media Queries
- 미디어 쿼리는 CSS와 스타일 시트에서 작성할 수 있다.
- 스타일을 변경하고 매개변수에 따라 새로운 스타일도 넣을 수 있다.
- 화면 넓이나 기기 종류, 기기가 움직이는 방향에 맞추어 스타일을 조정한다.


```css
/* 
width: 800px 정확하게 800px으로 설정은 잘안한다. 800px로 정확하게 맞출일이 있을까

min-width와 max-width로 viewport(모니터화면아니다.)로 제어한다.
min-width: 800px => 800px을 넘어서면 변경됨
max-width: 800px => 800px아래면 변경됨
 */

 /* 600과 800사이 적용 */
@media(min-width: 600px) and (max-width: 800px){
    h1{
        color: purple;
    }
}

/* 선택자의 순서에따라 상위 red값은 적용되지 않고 아래 orange값만 적용된다. */
@media(max-width: 500px){
    h1 {
        color: red;
    }
}
@media(max-width: 1000px){
    h1 {
        color: orange;
    }
}

/* 순서를 바꿀 시 원하는대로 적용된다. */
@media(max-width: 1500px){
    h1 {
        color: yellow;
    }
}
@media(max-width: 1000px){
    h1 {
        color: orange;
    }
}
@media(max-width: 500px){
    h1 {
        color: red;
    }
}

/* 일반적으로는 min-width를 쓰며, 이런형태도 가능하다. */
h1 {
    color: red;
}
@media(min-width: 500){
    h1 {
        color: yellow;
    }
}
@media(min-width: 1000px){
    h1 {
        color: orange;
    }
}
@media(min-width: 1500px){
    h1 {
        color: green;
    }
}

/* 화면전환능 검사탭에서 기기를 폰으로 변경후 뒤집어보자(landscape) 
*/
@media(orientation: landscape){
    body{
        background-color: magenta;
    }
}
```


> [예제코드 동작확인](https://github.com/KimTank/turbo-garbanzo/tree/main/udemy/web-developer-bootcamp-2022/sample-code/Flexbox_And_Responsive/MediaQueries%20Starter)

> ## 참고
> [MDN:CSS/Media](https://developer.mozilla.org/ko/docs/Web/CSS/@media)   
> [MDN:CSS/Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)   
