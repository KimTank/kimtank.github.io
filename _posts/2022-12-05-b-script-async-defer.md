---
layout: post
title: "defer, async script 리소스 로딩 시점"
date: 2022-12-02
categories:
  - HTML
tags:
  - Network
  - JavaScript
  - Web
  - defer
  - async
  - dynamic script
---

해림샘이 추가로 공부해보라고한 리소스 로딩 시점

---

## 1. 개요

모던웹은 html보다 무겁다. 용량이 커 다운로드 받는 데 시간이 오래걸리고 처리하는것도 마찬가지다.

브라우저는 html을 읽다가 `<script>...</script>` 태그를 만나면 스크립트를 먼저 실행해야 하므로 dom생성을 멈춘다. src속성이 있는 외부 스크립트를 만났을 때도 마찬가지이다. 외부에서 스크립트를 다운 받고 실행한 후에 남은 페이지를 처리할 수 있다.

- 발생하는 이슈
  1. 스크립트에서 스크립트 아래에 있는 dom요소에 접근할 수 없다. dom요소에 핸들러를 추가하는것과 같은 여러 행위가 불가능해진다.
  2. 페이지 위쪽에 용량이 큰 스크립트가 있는 경우 스크립트가 페이지를 막는다. 페이지에 접속하는 사람들은 스크립트를 다운받고 실행할때가지 스크립트 아래쪽 페이지를 볼수없다.

```html
<p>...스크립트 앞 콘텐츠...</p>

<script src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

<!-- 스크립트 다운로드 및 실행이 끝나기 전까지 아래 내용이 보이지 않습니다. -->
<p>...스크립트 뒤 콘텐츠...</p>
```

스크립트를 페이지 맨 아래 놓으면 해결할 수 있다. 스크립트위에 있는 요소에 접근할수있고, 페이지 콘텐츠 출력을 막지 않게 된다.

```html
<body>
  ... 스크립트 위 콘텐츠들 ...

  <script src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>
</body>
```

## 2. defer & async

html문서 자체가 아주 큰 경우 브라우저가 html문서 전체를 다운로드한 뒤 스크립트를 다운받게 하면 페이지가 느려진다.

네트워크 속도가 빠른 곳에서 접속 시 이런 종류의 지연은 큰 티가 나지 않으나, 3g모바일과같이 느린환경에서는 차이가 난다.

이를 위해 defer와 async가 당신을 기다리고있다.

### 2.1. defer

브라우저는 defer 속성이 있는 스크립트를 백그라운드에서 다운로드한다. 지연 스크립트를 다운하는 도중에도 html 파싱이 멈추지 않고, defer 스크립트 실행은 페이지 구성이 끝날때까지 지연된다.

```html
<p>...스크립트 앞 콘텐츠...</p>

<script
  defer
  src="https://javascript.info/article/script-async-defer/long.js?speed=1"
></script>

<!-- 바로 볼 수 있네요! -->
<p>...스크립트 뒤 콘텐츠...</p>
```

- 지연스크립트는 페이지 생성을 절대 막지 않는다.
- 지연스크립트는 dom이 준비된 후에 실행되지만 DOMContentLoaded이벤트 발생 전에 실행된다.

```javascript
<p>...스크립트 앞 콘텐츠...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("`defer` 스크립트가 실행된 후, DOM이 준비되었습니다!")); // (2)
</script>

<script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

<p>...스크립트 뒤 콘텐츠...</p>
```

1. 페이지 컨텐츠는 바로 출력된다.
2. DOMContentLoaded 이벤트는 지연 스크립트 실행을 기다린다. 따라 얼럿창은 DOM트리가 완성되고 지연스크립트가 실행된 후 뜬다.

지연 스크립트는 일반 스크립트와 마찬가지로 html에 추가된 순(상대, 요소)으로 실행된다.

길이가 긴 스크립트가 앞에, 길이가 짧은 스크립트가 뒤에 있어도 짧은 스크립트는 긴 스크립트가 실행될때까지 기다린다.

```javascript
<script defer src="https://javascript.info/article/script-async-defer/long.js"></script>
<script defer src="https://javascript.info/article/script-async-defer/small.js"></script>
```

> **작은 스크립트는 먼저 다운되지만 실행은 나중에 된다.**  
> 브라우저는 성능을 위해 페이지에 어떤 스크립트들이 있는지 쭉 살펴본 후 스크립트를 병렬적으로 다운한다. 스크립트 다운이 병렬적으로 진행되고, 크기가 작은 small.js가 long.js보다 먼저 다운될 수 있다.
>
> 하지만 명세서에서 스크립트를 문서에 추가한 순서대로 실행하라고 정의했기에 samll.js는 long.js다음에 실행된다.

> **defer 속성은 외부 스크립트에서만 유효하다.**  
> script에 src가 없으면 defer속성은 무시된다.

### 2.2. async

async속성이 붙은 스크립트는 페이지와 완전 독립적으로 동작한다.

- async는 defer와 마찬가지로 백그라운드에서 다운된다. html페이지는 async다운이 완료되길 기다리지 않고 페이지 내 컨텐츠를 처리 후 출력한다. 하지만 async 실행중에는 html 파싱이 멈춘다.
- DOMContentLoaded 이벤트와 async는 서로를 기다리지 않는다.
  - 페이지 구성이 끝난 후 async 다운로딩이 끝난 경우, DOMContentLoaded는 async 실행 전 발생할 수 있다.
  - async가 짧아서 페이지 구성이 끝나기 전 다운로드 되거나 스크립트가 캐싱처리된 경우, DOMContentLoaded는 async 실행 후 발생할 수 있다.
- 다른 스크립트들은 async스크립트를 기다리지 않는다. async 역시 다른 스크립트을 기다리지 않는다.

이런 특징 때문에 페이지에 async스크립트가 여러개있는 경우, 그 실행 순서가 제각각이 된다. 실행은 다운로드가 끝난 스크립트 순으로 진행된다.

```javascript
<p>...스크립트 앞 콘텐츠...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("DOM이 준비 되었습니다!"));
</script>

<script async src="https://javascript.info/article/script-async-defer/long.js"></script>
<script async src="https://javascript.info/article/script-async-defer/small.js"></script>

<p>...스크립트 뒤 콘텐츠...</p>
```

1. 비동기 스크립트 다운로드는 페이지 로딩을 막지 않기 떄문에 페이지 컨텐츠가 바로 출력된다.
2. DOMContentLoaded 이벤트는 상황에 따라 비동기 스크립트 전이나 후에 실행된다. 정확한 순서를 예측할수없다.
3. 비동기 스크립트는 서로 기다리지 않는다. 위치상 small.js가 아래긴 하나 long.js보다 먼저 다운로드되었기 때문에 먼저 실행된다. 이렇게 먼저 로드가 된 스크립트가 먼저 실행되는 것을 load-first order라고 부른다.

비동기 스크립트는 방문자 수 카운터나 광고 관련 스크립트처럼 각각 독립적인 역할을 하는 서드 파티 스크립트를 현재 개발중인 스크립트에 통합할때 유용하다. async는 개발중인 스크립트에 의존하지 않고, 반대도 마찬가지이다.

```javascript
<!-- Google Analytics는 일반적으로 다음과 같이 삽입합니다. -->
<script async src="https://google-analytics.com/analytics.js"></script>
```

## 3. 동적 스크립트

js를 사용하면 문서에 스크립트를 동적으로 추가할 수 있다. 이것을 dynamic script라고한다.

```javascript
let script = document.createElement("script");
script.src = "/article/script-async-defer/long.js";
document.body.append(script); // (*)
```

외부 스크립트는 관련 요소가 문서에 추가되자마자 \*부분을 다운시작한다.

동적 스크립트는 기본적으로 async처럼 동작한다.

- 그 어떤것도 기다리지 않는다. 다른것도 동적 스크립트를 기다리지 않는다.
- 먼저 다운된 스크립트가 먼저 실행된다: load-fist order

```javascript
function loadScript(src) {
  let script = document.createElement("script");
  script.src = src;
  script.async = false;
  document.body.append(script);
}

// async=false이기 때문에 long.js가 먼저 실행됩니다.
loadScript("/article/script-async-defer/long.js");
loadScript("/article/script-async-defer/small.js");
```

## 4. 요약

async & defer는 다운로드 시 페이지 렌더링을 막지않는다는 공통점이 있다. 적절히 사용ㅎ면 사용자가 오래 기다리지 않고 페이지 콘텐츠를 볼수있다.

|                  | async                                                                                                                                                                         | defer                                                                                        |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 순서             | load-first order. 문서 내 순서와 상관없이 먼저 다운로드된 스크립트가 먼저 실행                                                                                                | 문서에 추가된 순                                                                             |
| DOMContentLoaded | 비동기 스크립트는 html문서가 완전히 다운로드되지 않은 상태라도 로드 및 실행될수있다. 스크립트 크기가 작거나 캐싱 처리 되어있을때 html문서 길이가 아주 길때 이런일이 발생한다. | 지연 스크립트는 문서 다운로드와 파싱이 완료된 후에 DOMContentLoaded이벤트 발생전에 실행된다. |

> **스크립트 다운로드가 끝나지 않았어도 페이지는 동작해야 한다.**  
> defer를 사용하면 스크립트가 실행되기 전 페이지가 화면에 출력되는 점을 항상 유의해야된다.
>
> 사용자는 그래픽 관련 컴포넌트들이 준비되지 않은 상태에서 화면을 볼수도있다.
>
> 지연 스크립트가 영향을 주는 영역에선 반드시 '로딩 인디케이터'가 있어야된다. 관련 버튼도 disabled처리를 해줘야한다. 이렇게 해야 사용자에게 현재 어떤것은 사용할 수 있는지, 어떤것은 사용할 수 없는지 알려줄 수 있다.
>
> 실무에서도 defer를 DOM전체가 필요한 스크립트나 실행 순서가 중요한 경우에 적용한다. async는 방문자 수 카운터나 광고 관련 스크립트와 같이 독립적인 스크립트에 혹은 실행 순서가 중요하지 않은 경우에 적용한다.

## 5. 동작 시각화

![https://ko.javascript.info/script-async-defer](/assets/img/221205-defer.png)

---

하위사이트가 상당히 내용이 좋은거같다. 따로 시간내서 봐야되겠음.

---

## 참조

> [javascript.info: script-async-defer](https://ko.javascript.info/script-async-defer)
