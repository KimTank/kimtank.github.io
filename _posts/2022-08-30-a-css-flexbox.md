---
layout: post
title: "CSS Flexbox"
date: 2022-08-30
categories:
- CSS
tags:
- CSS
- flexbox
- flex-model
- main-axis
- cross-axis
- flex-direction
- justify-content
- flex-wrap
- align-items
- align-content
- align-self
- flex-sizing
- flex-basis
- flex-grow
- flex-shrink
---

시간배분을 잘못하고, 나중에 봐도 괜찮았을 애니메이션부분을 한번 보느랴(다 이해하지도, 정리하지도 못했다.) 입안이 부르텄다. 체력적인 한계는 무한인데 내입안은 무한이 아닌가보다. 잘먹고 잘자고 잘놀고의 법칙 중 세가지 다 못지키고 있다. 시간이 날 때 다른 방안을 연구해봐야겠다. 일단은 지금은 현재 할 수 있는일에 집중하기 위해 달리자.

## Flexbox

최근에 추가된 개념으로 동적인 뷰를 구성할 수 있게한다.

## Flex Model

- main axis: 기본방향 왼쪽에서 오른쪽
- cross axis

## Flex Direction

방향

- default: row
- value
  - row: 기본값, 좌로붙어 좌에서 우로 정렬
  - row-reverse: 우로붙어 우에서 좌로 정렬
  - column: 위로붙어 상하로변경 상에서 하로 정렬
  - column-reverse: 아래로붙어 상하로변경 하에서 상으로 정렬
    > 다른 설정을 하지않은 기본값을 가정할 때, 크기의 경우 부모뷰의 크기가 자식들을 다 담고도 남으면 자식뷰들은 정해진 뷰만 출력. 부모뷰의 크기가 자식들을 다 담지 못할 때는 스크롤에 따라서 부모뷰는 줄어들게된다.

## Justify Content

**주축**을 기준으로 요소와 컨텐츠를 어떻게 배치할지 결정하는 속성

- default: flex-start
- value
  - flex-start
  - flex-end
  - center
  - space-between: 0-1-1-0 부모안에서 요소끼리 공간을 동일하게 나눠서 배치
  - space-around: 0.5-1-1-0.5 부모와의 공간에서 공백을 절반 나누어 배치
  - space-early: 1-1-1-1 부모와의 공간에서도 공백을 요소끼리와 동일하게 나누어 배치

## Flex Wrap

부모를 넘어설 때 새로운 행이나 열로 요소를 정렬함.

- default: nowrap
- value
  - nowrap: 부모를 넘어설때 정해준 규칙에 따라 공간을 나눠가짐.
  - wrap: 좌에서 우로, 상에서 하로
  - wrap-reverse: 우에서 좌로, 하에서 우로

## Align Items

**교차축**의 시작점을 기준으로 아이템을 정렬한다.

- default: flex-start
- value
  - flex-start
  - flex-end
  - center: 요소들의 크기가 제각각이라도 제각각의 센터를 부모의 센터로 맞춘다.
  - baseline: font의 기준선에 맞추서 정렬한다.

## Align Content

행이나 열이 여러개일때 **교차축**을 기준으로 정렬한다.  
flex-wrap을 적용하지 않은 채 행이나 열이 단 하나라면 적용되지 않는다.

## Align Self

Align Content와 비슷하지만 flex 컨테이너에서 두개의 요소에 개별로 사용한다. flex 컨테이너 자체가 아닌 개별 요소에 적용할 때 사용한다.   
**교차축**을 기준으로 배열된 단일 요소의 위치를 바꿀 수 있다.

## Flex Sizing Properties

### Flex Basis

요소가 배치되기 전에 요소의 최초 크기를 결정한다. 플렉스 컨테이너에 추가되기 전 시작점과 같은 것이다.

### Flex Grow

공간이 있을 때 요소가 그 공간을 얼마나 차지할지 결정한다.

```html
<!-- 각요소마다 flex-grow값이 없음(초기값 0) -->
|---|-a-|-b-|-c-|-d-|---|

<!-- a에 flex-grow: 1; -->
|----a-|-b-|-c-|-d-|---|

<!-- d에 flex-grow: 1; -->
|----a-|-b-|-c-|-d----|
```

- 남는공간을 나눠가진다.
- flex-wrap이 설정되 있을때 지정된 크기 이하로 작아지면 flex-wrap설정에 따라 행이나 열이 밀려서 바뀐다.
- min-width, max-width, min-height, max-height

### Flex Shrink

컨테이너에 충분한 공간이 없을 때, 요소들이 줄어드는 비율을 정한다.

- 몇 px까지 줄도록하는게 아니라, 다른 요소에 비해 얼마나 더 줄어들지 설정한다.

### Flex Shorthand

축약법

```css
/* Keyword values */
flex: auto;
flex: initial;
flex: none;

/* one value, unitless number: flex-grow */
flex: 2;

/* one value, width/height: flex-basis */
flex: 10em;
flex: 30%;
flex: min-content;

/* two values: flex-grow | flex-basis */
flex: 1 30px;

/* two values: flex-grow | flex-shrink */
flex: 2 2;

/* Three values: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;

/* Global values */
flex: inherit;
flex: initial;
flex: unset;
```

## 참조

> [MDN:CSS/Flexbox](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Flexbox)   
> [MDN:CSS/Value & Unit](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Values_and_Units)   
> [MDN:CSS/FlexibleBox](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)   
> [MDN:CSS/FlexibleBox Layout & Other Layout Methods](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Relationship_of_Flexbox_to_Other_Layout_Methods)   
> [MDN:CSS/grid](https://developer.mozilla.org/ko/docs/Web/CSS/grid)