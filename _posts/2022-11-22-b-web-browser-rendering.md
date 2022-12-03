---
layout: post
title: Web Browser Rendering
date: 2022-11-22
categories:
  - Web
tags:
  - Web
  - Browser Rendering
  - parsing
  - DOM Tree
  - CSSOM Tree
  - Render Tree
  - Layout
  - Painting
  - Reflow
  - Repaint
  - 최적화
---

양이 많다고 미루면 계속 밀린다. 내일에 나는 내일에 할일이 있지만, 오늘의 나는 어제의 내가 못한일을 마무리지어야한다. 근래들어 이래저래 인간관계에 있어서 회의감이 많이 들긴하지만, keep it real.

---

## 1. Browser Rendering

HTML, CSS, JS 등 개발자가 작성한 문서가 브라우저에 출력되는 과정이다.

```
HTML    JS      CSS
↓       ↓       ↓
DOM    ←↔→      CSSOM
↓               ↓
→ → Render Tree ←
        ↓
    Layout
        ↓
    Paint
```

1. 사용자 브라우저로 웹사이트 접속
2. 브라우저 웹사이트 필요한 리소스 다운
3. 렌더링엔진 HTML 문서 파싱해서 Document Object Model(문서 객체 모델)트리 생성
4. 외부 CSS파일 + 스타일 요소 파싱 CSS Object Model(CSS 객체 모델)트리 생성
5. 만든 DOM트리와 CSSOM트리 결합 Render 트리 구축
6. 레이아웃 과정 통해 각 요소 어디에 배치할지 결정
7. 레이아웃 과정 끝나면 UI백엔드 Render트리 화면에 그림

### 1.1. 파싱(parsing)

프로그래밍 언어로 작성된 파일을 실행시키기 위해 syntax analysis(구문을 분석)하는 단계이다. parser가 진행하고, 인터프리터나 컴파일러의 구성 요소이다. 파서가 html파일 코드를 문법적 의므를 갖는 최소 단위인 token으로 한번 분해, 이 토큰들을 문법적 의미와 구조에 따라 node 요소로 변환한다. node들은 상하 관계에 따라 parse tree 또는 syntax tree라 하는것을 형성한다.

document parsing은 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것이다. HTML은 DOM으로 CSS는 CSSOM으로 파싱한다.

HTML을 DOM트리로 파싱할 때 HTML토큰이 생성되는데, 이 토큰에는 시작 태그와 미침태그가 포함, 속성 이름과 값도 포함된다. 이런 토큰으로 변환된 입력값은 parser에 의해 node가 된다. 결과로 tree structure인 DOM이 구성된다.

HTML 파싱 중 CSS를 만나면 CSS 스타일링 레이아웃과 페인팅에 사용하는 데이터 구조인 CSSOM 트리로 파싱하고, 태그를 만날 경우 렌더링을 차단하면서 HTML 파싱을 중단한다. 이어 script파일을 다운 받아 파싱하고 실행시킨 후 다시 HTML 파일을 파싱한다.

파싱은 문서에 작성된 언어 또는 형식의 규칙에 따르는 파싱할 수 있는 모든 형식은 정해진 용어와 구문 규칙에 따라야한다. 형식을 잘 갖춘 문서라면 파싱 과정은 직관적이고 빠르게 진행된다.

### 1.2. DOM Tree

DOM은 HTML문서의 요소들의 중첩관계를 기반으로 노드들을 트리 구조로 구성한 것을 말한다. 브라우저는 JS 언어만 알아듣기 때문에 HTML태그나 속성들을 이해하지 못한다. 그래서 이해할 수 있는 형태의 객체로 바꿔주는 것이 DOM이다.

### 1.3. CSSOM Tree

html 파일을 DOM트리로 파싱하던 브라우저는 link나 style태그를 만나면 파싱을 잠시 멈추고 해당 리소스 파일을 서버로 요청한다. html파일처럼 파싱을 하여 CSSOM을 구성한다. 구축이 끝나면 html파일의 파싱이 멈춘 부분으로 돌아가 DOM트리를 구축한다.

> CSS는 부모의 속성이 자식이 상속받는다. 중첩되면 연산이 중첩횟수만큼 되어 최적화를 위해서는 유의해야한다.

### 1.4. Render Tree

DOM과 CSSOM은 리소스가 다른 독립적인 트리이다. 웹사이트에 그리기 위해서는 둘을 합쳐야 한다. Rendering을 목적으로 만들어진 Render Tree는 보이지 않을 요소들은 트리에 포함시키지 않는다.(ex: meta태그, display: none 속성)

### 1.5. Layout

렌더트리를 기반으로 HTML요소의 레이아웃을 계산하여 브라우저 화면 어디에 배치할지 결정하는 과정이다. painting이라는 작업을 거쳐야 브라우저 위의 화면에 그려진다.

화면에 어디에 위치할지에 대한 연산은 브라우저의 렌더링 엔진이 한다. 위에서 아래로 읽어가며, 모든 값은 절대적 단위 px을 사용한다.

### 1.6. Painting

브라우저 화면은 픽셀로 이루어져있고, painting은 각 정보를 가진 픽셀들이 모여 픽셀에 대한 정보를 바탕으로 픽셀을 채워나간다.

## 2. Reflow & Repaint

화면에 위치한 크기나 모양이 변경이 될 시 모든 요소의 위치와 크기를 다시 계산하고, 다시 그려준다.

### 2.1. 최적화

초당 60프레임은 유지해야 유저의 눈에는 부드럽게 처리된다. 1초의 시간동안 브라우저는 60장의 레이아웃과 페인트 과정을 동시에 처리한다. DOM이 조작되면 렌더트리를 구축하므로 변경이 될때마다 리플로우와 리페인트를 다시한다. 리플로우 과정은 렌더링을 다시 하기에 배치를 위한 연산을해 CPU를 많이 쓰고, 리페인트는 픽셀을 다시 변화시키기에 GPU를 쓴다. Frame Drop현상도 CPU와 GPU를 많이 사용해 생긴다. -> UX상 좋지않다.

- 불필요한 레이아웃을 줄인다.
- CSS에서 레이아웃, 페인트를 발생시키는 속성들 중 리플로우 보다 리페인트만 발생하는 속성을 사용하는게 좋다.

#### 2.1.1. 리플로우 속성

`position`,`width`,`height`,`reft`,`top`,`right`,`bottom`,`margin`,`padding`,`border`,`border-width`,`clear`,`display`,`float`,`font-family`,`font-size`,`font-weight`,`line-height`,`min-height`,`overflow`,`text-align`,`vertical-align`...

#### 2.1.2. 리페인트 속성

`background`,`background-image`,`background-position`,`background-repeat`,`background-size`,`border-radius`,`border-style`,`box-shadow`,`color`,`line-style`,`outline`,`clear`,`display`,`float`,`font-family`,`font-size`,`font-weight`,`outline-color`,`visibility`...

- 리플로우는 위치나 너비가 많다. left 속성으로 애니메이션을 만들 시 프레임 유지를 보장못한다. 이에 transform이라는 속성을 쓴다. transform의 translate을 사용하여 위치를 이동ㅎ면, 프레임을 유지할 수 있다.(layout X -> paint O)
- opacity를 사용하면 visibility/display보다 빠르다.

#### 2.1.3. 영향을 주는 node 줄이기

JS + CSS를 조합한 애니메이션이 많거나, 레이아웃의 변호가 많은 요소일 시 position을 absolute나 fixed를 사용할 시 영향을 받는 node들이 줄어든다. fixed처럼 영향을 받는 node가 없을 시 리페인트만 연산한다.

---

안드로이드도 꽤나 뷰성능에 대한 고민을 해야되는 부분이 많았는데, web역시 모양만 만든다고 막만들 시 문제가 발생할 여지가 많다는걸 알았다. 상당히 어렵지만 알고 있으면 추후 유지보수 비용을 줄일 수 있다.

---

## 참조

> [ui toast: web render](https://ui.toast.com/weekly-pick/ko_20171016)  
> [mdn: web performance how browser work](https://developer.mozilla.org/ko/docs/Web/Performance/How_browsers_work#%EA%B0%99%EC%9D%B4_%EB%B3%B4%EA%B8%B0))  
> [mdn: web performance](https://developer.mozilla.org/ko/docs/Web/Performance)  
> [mdn: browser](https://developer.mozilla.org/ko/docs/Glossary/Browser)  
> [mdn: reflow](https://developer.mozilla.org/ko/docs/Glossary/Reflow)  
> [mdn: browser-reflow](https://developers.google.com/speed/docs/insights/browser-reflow)
