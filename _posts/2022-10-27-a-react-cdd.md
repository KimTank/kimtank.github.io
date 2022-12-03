---
layout: post
title: "React Component Driven Development"
date: 2022-10-27
categories:
  - React
tags:
  - CDD
  - Component Driven Development
  - CSS Preprocessor
  - SCSS
  - BEM
  - Block
  - Element
  - Modifier
  - CSS-in-JS
  - Styled-Component
---

폰노이만이 처음 인체와 같은 생물의 구조로 컴퓨터의 구조를 설계하고, 완성하지 못하고 무지개다리를 건너신 후 컴퓨터는 폰노이만의 설계대로 완성되었고, 그가 연구하다 죽음으로 멈춘 메모리계층구조 역시 현대에서는 쓰이고 있다.

이처럼 컴퓨터는 생물이 진화하는것과 비슷하게 진화하기 시작했고, 처음에는 출력장치인 모니터부터, 입력장치인 키보드, 마우스 등으로 진화를 거듭해 불과 20년 전 까지만 하더라도 "들고다니는 손바닥만한 컴퓨터가 나올 것이다".라는 말을 들었을 때 "무슨 100년뒤 이야기를 하냐"라고 했지만, 과학의 발전은 인간의 상상을 뛰어넘어 우리는 들고다니는 컴퓨터를 하나씩 가지고 다닌다.

그 발전의 와중에 프론트엔드 개발 패러다임도 많은 변화를 겪었는데, 점점 기기가 소형화되고, 상업적인 사이트들이 늘어감에따라 경쟁에 의한 진화를 거듭하게된다.

세상에서 큰화면에서부터 세상에서 가장 작은 화면까지, 애플에서는 규격화시켜 자신들의 규격으로 통일시키려는 시도를 하였으나, Android의 등장으로 처참히 실패(가격과 소스공개정책만 비슷했어도 성공했을지도 모른다.)하였고, 우리가 만지는 이동형 컴퓨터는 규정할 수 없는 화면의 크기로 개발자들의 골머리를 썩게 한다.

그 골머리를 썩으며 천재들이 고민한 끝에 내린 현재로서는 React내에서 가장 효율적이고 생산적인 방법.

---

## 1. Component Driven Development

비슷한 기능의 비슷한 UI를 매번 새로 만들어 관리할 항목을 늘릴 필요는 없다. 그래서 재사용 가능한 Component를 미리 만들어 놓는다면, 개발비용이나 유지보수비용을 줄일 수 있다.

[BBC](https://bbc.github.io/psammead/?path=/story/components-brand--without-brand-link), [UN](https://uikit.wfp.org/docs/index.html?path=/docs/templates-browser-warning-outdated--error-dialog)같은 사이트들도 CDD를 이용하여 storybook으로 UI Component를 활용했다.

### 1-1. CSS Preprocessor

CSS Preprocessor는 CSS가 구조적으로 작성될 수 있게 도움을 주는 도구이다. CSS 전처리기는 JSX처럼 Brower가 인식을 못하기 때문에, CSS 전처리기에 맞는 Compiler를 사용하고, Comlpile되면 CSS파일로 변환된다.

SASS는 CSS를 확장해주는 스크립팅 언어이다. 변수를 선언하거나, 반복되는 코드를 한번의 선언으로 재사용할 수 있게하는 기능을 가졌다. SASS는 SCSS코드를 읽어서 전처리한 다음 컴파일하여 전역 CSS 번들 파일을 만들어 주는 전처리기의 역할을 한다.

> SCSS가 그런거였군!!

하지만 언제나 그렇듯. 구조화를 위한 구조화(????)를 위한 구조화(??????)를 하다보니 CSS의 용량은 상상을 초월하게된다.

대안으로 나온것이 BEM, OOCSS, SMACSS 3가지 CSS방법론이 등장하였다. 이 방법론들의 공통 지향점은

1. 코드의 재사용화
2. 코드의 간결화
3. 코드의 확장성
4. 코드의 예측성

그래서 모든 팀프로젝트의 근간이되는 가장 중요한 진실은. CSS도 그렇겠지만 방법들에 대한 규칙을 정하는 것이다.

### 1-2. BEM

Block, Element, Modifier로 구분하여 클래스명을 작성하는 방법이다.

- Block: 전체를 감싸고 있는 블럭 요소
- Element: 블럭이 포함하고 이있는 한 조각
- Modifier: 블럭 또는 요소의 속성
- 구분점: --, \_\_

일관성있는 네이밍으로 구조화를 시키지만 클래스 선택자가 장황해지고, 길어진 클래스명 때문에 마크업이 불필해지게 커지고, 재사용할때마다 모든 UI컴포넌트를 명시적으로 확장해야되는 문제가 발생한다.

### 1-3. CSS-in-JS

이렇게 캡슐화의 개념이 필요해지고, 컴포넌트 단위로 개발하기 위한 방법으로 CSS-inJS가 만들어지게 된다.

대표적인것으로는 Styled-Component가 있다.

### 1-4. 방법론들의 특징, 장단점

|---|---|---|---|
|CSS|기본적인 스타일링 방법|-|일관된 패턴을 갖기 어려움. !important의 남용|
|SASS(preprocessor)|프로그래밍 방법론을 도입, 컴파일된 CSS를 만들어내는 전처리기|변수/함수/상속 개념을 활용하여 재사용, CSS의 구조화|전처리 과정 필요, 디버깅 어려움, 컴파일한 CSS파일 거대|
|BEM|CSS 클래스명 작성에 일관된 패턴을 강제하는 방법론|네이밍으로 문제 해결, 전처리 과정 불필요|선택자의 이름이 장황, 클래스 목록이 많아짐.|
|Styled-Component(CSS-in-JS)|컴포넌트 기반으로 CSS를 작성할 수 있게 도와주는 라이브러리|CSS를 컴포넌트 안으로 캡슐화, 네이밍이나 최적화 신경쓸 필요없음|빠른 페이지 로드에 불리|

## 2. CDD 개발도구

### 2-1. Styled Components

css를 기피하게 되는 이유

- class, id 이름을 뭘로 지을까
- css내에 주석을 안남기면 뭐가뭔지 나도 모름
- css파일을 js파일이랑 1:1매치하면 전역은 왜필요한거야
- 내가 만들었는데 중복되서 뭐가 중복된지 몰라서 애먹음

그런 우리를 위해 Styled Components, CSS-in-JS가 나오게 되었다. React가 나오며, CSS만 홀로 외로이 있는걸 못참은 누군가가 HTML + JS + CSS를 묶어 외롭지 않게 해주었다.

### 2-2. CSS를 외롭지 않게 하는 Styled Components 설치하기

- cli

```bash
# npm
$npm install --save styled-components

# yarn
$yarn add styled-components
```

- package.json

```JSON
{
    "resolutions": {
        "styled-components": "^5"
    }
}
```

- some-of-jsfile.js

```javascript
import styled from "styled-components";
```

### 2-3. Styled Components Syntax

#### 2-3-1. 컴포넌트 만들기

```javascript
const ComponentName = styled.TagKind`
    attribute1: value;
    attribute2: value;
    ...
`;

const GreenBorderBackground = styled.div`
    border: green, 2px, solid;
    background-color: transparent;
    ...
`;
```

#### 2-3-2. 기본컴포넌트 재활용

```javascript
const ComponentName = styled(recycleComponent)`
    addedAttribute1: value;
    addedAttribute2: value;
    ...
`;

const GreenBorderRedColorBackground = styled(GreenBorderBackground)`
    color: red;
    padding: 4px;
    ...
`;
```

#### 2-3-3. Props 활용

```javascript
const ComponentName = styled.tagKind`
    attribute: ${(props)=>{function()}};
    ...
`;
```

Styled Component로 제작한 React컴포넌트처럼 props를 내려줄 수 있다. 내려준 props 값에 따라 컴포넌트를 렌더링 할 수 있다.

템플릿 리터럴을 사용하여 JavaScript코드를 사용할 수 있다. props를 받으려면 props를 인자로 받는 함수를 만들어 사용하면 된다.

1. Props로 조건부 렌더링하기

```javascript
const CheckBox = styled.input`
    value=${(props)=>props.isCheck?"체크":"안체크"}
`;

//형태
<CheckBox isCheck.../> -> 체크
<CheckBox/> -> 안체크
```

2. Props값으로 렌더링하기

```javascript
const CheckBox = styled.input`
    value=${(props)=>props.isCheck?props.isCheck:"안체크"}
`;

//형태
<CheckBox isCheck=true/> -> 'true'
<CheckBox isCheck="oK"/> -> 'oK'
<CheckBox isCheck="1"/> -> '1'

---

const CheckBox = styled.input`
    value=${(props)=>props.isCheck||"안체크"}
`;  //이런문법도 가능
```

#### 2-3-4. 전역 스타일 설정하기

전역 스타일 지정을 위해서는 Styled Components의 createGlobalStyle 함수를 사용한다.

```javascript
import { createGlobalStyle } from "styled-components";
```

```javascript
const GlobalStyle = createGlobalStyle`
    div {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        ...
    }
`;
```

```javascript
const App = () => {
  return (
    <section>
      <GlobalStyle />
      <div>...</div>
    </section>
  );
};
```

### 2-3-5 Styled-Components 리팩토링

1. createGlobalStyle과 개별값은 같이 사용하지 못하므로, 분리해야 한다. [방법](https://dilshankelsen.com/create-global-styles-with-styled-components/)
2. 효과의 경우

```javascript
cosnt Button = styled.button`
    ...attribute..
    $:hover {
        // 호버시 동작할 attribute: value;
    }
`;
```

## 참조

> [styled-component: document](https://styled-components.com/docs)  
> [진우형픽 검색엔진: hello](https://beta.sayhello.so/)  
> [진우형픽 검색엔진2: brave](https://search.brave.com/)  
> [storybook](https://storybook.js.org/)
