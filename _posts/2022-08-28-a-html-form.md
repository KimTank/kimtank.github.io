---
layout: post
title: "HTML form과 내부 태그와 속성 "
date: 2022-08-28T00:00:00-00:00
categories:
- HTML
tags:
- HTML
- form
- input
- type
- checkbox
- radio
- select
- button
- range
- textarea
---

이전에도 Android만 하지말고 Web Front로 방향을 잡아라는 친한 동생의 이야기에 웃어 넘긴적이 있다. 근래에는 JavaScript와 HTML만 보고있는데도 느끼는건 ~~시간이 많이 부족하다.~~ 볼 양이 많아서 너무 행복하다 ^^*

## HTML `<form>`

- user에게는 보이지 않는 container
- inputs, checkboxes, buttons, etc로 구성
- 그룹화된 전송하는 데이터의 모든 입력을 담는 상자
- `form`을 제출하면 HTTP요청이 전송된다.
- `action` attribute를 사용하여 제어한다.

> HTTP method `get` & `set`이 있다.

## `<form>`의 내부 태그들

## `<input>`

- `type` attribute로 input태그의 형식을 정한다.
- closing tag 없다.

## `<input>`'s attribute

- `type`
  
  ```javascript
  <input type="type's value">
  ```

  - `text`
  - `password`
  - `color`: 브라우저에따라 color picker가 다를 수 있다.
  - `number`: `text`와 비슷하나 숫자만 입력되고 방향키 가능
  - `name`
  - 서버와 통신하는 `key`값으로 서버가 찾으려는 간단한 값이다.

  > https://www.anymous-website-example.com/login_action?user=유저명&pwd=비밀번호&birth=생일...
  > > 각 input 태그에 저장된 정보가 form의 action 속성인 login_action을 통해 input의 name에 지정된 이름(user, pwd, birth)와 같은 키값으로 입력된 value(유저명, 비밀번호, 생일)를 전송한다.   
  > > 해당 /접속주소?key=value&key2=value2 의 형태로 GUI를 이용하지 않고, google검색이나 해당 동작을 주소창에서 할 수도 있다.

  - `checkbox`
    - `checkbox`는 꼭 `<label>`처리 한다.

```html
<div>
  <input type="checkbox" id="giant" name="giant" checked>
  <label for="giant">Giant</label>
</div>
<div>
  <input type="checkbox" id="merida" name="merida">
  <label for="merida">Merida</label>
</div>

<form>
  <input type="checkbox" id="checked" name="checked">
  <label for="checked"></label>
  <button>전송</button>
  <!-- 체크 후 전송 시 https://주소.도메인/action?checked=on  체크하지 않았을 도 보내지 않는다.-->
</form>
```

- `radio`
  - `checkbox`와 비슷하지만 중복선택이 가능한 `checkbox`와는 다르게 단일값만 선택 가능하다.

```html
<form>
  <p>choose your bike size</p>
  <label for="s">S(47)</label>
  <input type="radio" name="size" id="s" value="s">
  <label for="m">M(50)</label>
  <input type="radio" name="size" id="m" value="m">
  <label for="l">L(53)</label>
  <input type="radio" name="size" id="l" value="l">
  <button>전송</button>
  <!-- value를 지정해줘야 선택한 값이 전송된다. 라디오버튼을 묶기 위해서는 name 한 값으로 줘야한다.-->
</form>
```

- `range`
  - 범위를 만들어서 그 값을 선택하게한다.
  - 최소값, 최대값을 제어가능하다.

```html
<div>
  <label for="quantity">수량</label>
  <input type="range" id="quantity" min="0" max="65535" step="100" value="32267" name="quantity">
</div>
<!-- 
  수평으로된 범위(andrid progressbar)선택 gui가 출력된다.
  step: 한눈금단 단위
  value: 초기값
  submit 시 정해진 범위로 /주소?key=value
  type="number"일 때도 min, max값을 지정하면 지정한 범위만큼 입력가능하다.
-->
```

- `placeholder`

```html
<input type="..." placeholder="(ex: username, enter password, etc)" >
```

> 모든 `<input>`에서 적용되지는 않는다.

## `<select>`

```html
<label for="color">choose your bike color</label>
<select name="color" id="color-selected">
  <option value="choose color">select color</option>
  <option value="black">Metal Black</option>
  <option value="silver">Shiny Silver</option>
  <option value="blue">Ocean Blue</option>
  <option value="red">Fire Red</option>
</select>
<!-- value값이 키값인 color로 전송된다. 단순 문자열은 UI일뿐 -->
```

## `<label>`

- 접근성이 좋고 form을 편하게 해준다.

```html
<form>
  <div>
  <!-- 표준 -->
    <label for="specialized">like Specialized</label>
    <input type="checkbox" name="specialized" id="specialized">
  </div>
  <!-- 비표준 -->
  <div>
    <label>
      like Trek
      <input type="checkbox" name="trek" id="trek">
    </label>
  </div>
</form>
```

  > `<label>`의 `for` attribute와 `<input>`의 `id` attribute로 연결점생김.<br/>
  > `id`는 identify, 유일한 값을 가져야한다.
  
## `<button>`

```html
<div>
  <button>그냥버튼</button>
  <form>
    <button type="button">그냥 버튼</button>
    <button>form action으로 전송</button>
    <input type="submit" value="button전송과 같은 동작">
  </form>
</div>
```

- `<form>`안에 위치할 경우 기본값이 `submit`, `<form>`의 `action` attribute와 연동되어 따로 명시하지 않으면 전송한다.


## `<textarea>`

- 복수의 줄을 입력하는 입력창이 출력된다.
- Android:View/TextView/maxLine: 지정과 같은 모양(모양만 같다 동작은 다르다.)

```html
<div>
  <label for="review">상품 리뷰</label>
     
  <textarea id="review" row="5" cols="50" name="review" placeholder="input your review">
</div>
```

> ## 참조
> [MDN:HTML/Element/form](https://developer.mozilla.org/ko/docs/Web/HTML/Element/form)   
> [MDN:HTML/Element/input](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input)   
> [MDN:HTML/Element/select](https://developer.mozilla.org/ko/docs/Web/HTML/Element/select)   
> [MDN:HTML/Element/button](https://developer.mozilla.org/ko/docs/Web/HTML/Element/button)   
> [MDN:HTML/Element/Input/radio](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/radio)   
> [MDN:HTML/Element/Input/checkbox](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)   
> [MDN:HTML/Element/Input/range](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range)   
> [MDN:HTML/Element/textarea](https://developer.mozilla.org/docs/Web/HTML/Element/textarea)