---
layout: post
title: "CSS Selectors와 Specificity"
date: 2022-08-29T08:20:00
categories:
- WebFront
tags:
- CSS
- Selector
- Universal-Selector
- Type-Selector
- Selector-list
- ID-Selector
- Class-Selector
- Descendant-Selector
- Adjacent-Selector
- Direct-child
- Attribute-Selector
- Pseudo-classes
- Pseudo-Elements
- The-Cascade
- Specificity
- Inheritance
---
예습을 하고싶었건만 시간은 야속하게 흐르고, ~~내 집중력은 산으로 가고있고~~ :clap:
눈뜨니 ~~아침이고 껄껄꺾크흑ㄱㄱ~~ :clap: 정신차리니 밤이더라 껄껄껄

# CSS Selector와 Specificity

## Selectors

### Universal Selector
전체 선택자
```css
* {
    property: value;
}
```

### Type Selector
지정 선택자
```css
type {
    property: value;
}
```

### Selector list
복수 지정 선택자
```css
type1, type2 ...{
    property: value;
}
```

### #ID Selector
id 선택자, #id명, id는 페이지내 한번만, id는 최소한사용
```css
#id {
    property: value;
}
```

### Class Selector
class 선택자, .class명, 비슷한 스타일끼리 묶어서 구조화할 수 있다.
```css
.class{
    property: value;
}
```

### Descendant Selector
자손 선택자, parent-tag child-tag(anchor tag), 부모태그 내 자식태그를 선택, class 사용가능
```css
parenttype childtype{
    property: value;
}

.class childtype{
    property: value;
}

parenttype #id {
    property: value;
}
```

### Adjacent Selector
인접 선택자, `+`부호 인접 선택자, 형제의 개념
```css
type1 + type2 {
    property: value;
}
```

### Direct child
직계자손 선택자, type1 > type2, `>` type1 바로 아래 있는 type2를 지칭
```css
type1 > type2 {
    property: value;
}
```

### Attribute Selector
속성 선택자, type[attribute="value"] 등
```css
type[attribute="value"] {
    property: value;
}

type.class {
    property: value;
}

/* include가 포함된 모든 a태그 */
a[href*="include"] {
    property: value;
}
```

## Pseudo Classes
선택자 끝에 붙여 상태를 특정하는 키워드
- :active
- :checked
- :first
- :first-child
- :hover
- :not()
- :nth-child(n)
- :nth-of-type(n)
```css
type:hover {
    property: value;
}

/* 4번째 태그만 선택 */
type:nth-of-type(4){
    property: value;
}

/* 2번째 태그마다 선택 */
type:nth-of-type(2n){
    property: value;
}
```

## Pseudo Elements
- ::after
- ::before
- ::first-letter
- ::first-line
- ::selection
```css
type::first-letter {
    property: value;
}

/* 문자 긁을시 */
type::selection{
    property: value;
}
```

## The Cascade
스타일의 최상단부터 출발한 폭포(cascade)가 아래로 쭉 흘러서 스타일시트 최하단이나 다음 스타일 시트로 넘어간다.
- .css파일 내 동작

```css
type-a {
    property-a: value-a;
}
type-a {
    property-a: value-A;
}
/* 적용 시 type-a 태그는 하단의 value-A가 적용된다. */
```

- head에 명시 동작

```javascript
<head>
    <meta charset="UTF-8">
    ...
    <title>Document</title>

    <link rel="stylesheet" href="index.css">
    <link rel="stylesheet" href="general-styles.css">
    // 위 링크를 적용한 후 다음 링크로 넘어가 겹치는 부분이 있을 시 아래 general-styles.css의 명세가 적용된다.
<head>
```

## SPECIFICITY
충돌이 생길 경우 브라우저에서 규칙을 적용한다.   
하나 이상의 스타일이 도일한 요소에 적용되거나, 적용될 수 있는 경우 출돌이 발생한다.
```css
/* 예시 */
.class type:pseudo element{
    property: value;
}
type:pseudo element{
    property: value-a;
}
/*
 chrome의 경우 .class type:pseudo element의 스타일을 우선한다.
 각 브라우저가 주어진 선택자의 구체도를 측정하여 더 구체적인 선택자를 우선적용한다.

 동일한 property가 충돌이 날때 우선순위에따라 적용.
*/
```
> ### 구체적 기준의 우선도   
> ---
> |ID|>|CLASS|>|ELEMENT|
> |---|---|---|---|---|
> |ID Selectors|>|Class, Attribute, Pseudo-Class Selectors|>|Element, Pseudo-Element Selectors|
> ---
> 태그 내 inline 선택자의 경우 ID선택자보다 더 명시적이므로 우선한다.
> ### !important
>개별스타일 지정에 사용할 수 있는 선택자
>```html
><div class="ty" style="color: green;">What color am I?</div>
>```
>```css
>.ty[style*="color: green"] {
>    color: magenta !important;
>}
>```
>가장 우선순위로 사용됨.

> ## 참고
> [MDN:CSS/Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)   
> [MDN:CSS/Cascade&Inheritance](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance#%EA%B3%84%EB%8B%A8%EC%8B%9D_cascade)   
> [CoolColorSelect](https://coolors.co)   
> [Specificity:keegan](https://specificity.keegan.st)