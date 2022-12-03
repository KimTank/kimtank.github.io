---
layout: post
title: "HTTP & NETWORK 3"
date: 2022-10-05
categories:
  - Network
tags:
  - HTTP
  - Network
  - AJAX
  - JavaScript
  - DOM
  - Fetch
  - XHR
  - XMLHttpRequest
  - SSR
  - Server Side Rendering
  - CSR
  - Client Side Rendering
---

어마어마하군. 실제로는 방대한 양이지만 최소한으로 알 지식만 압축해놓은거같다.

---

## 1. AJAX

Asynchronous JavaScript And XMLHttpRequest, JavaScript, DOM, Fetch, XMLHttpRequest, HTML 등의 다양한 기술을 사용하는 웹 개발 기법이다.

웹 페이지에 필요한 부분에 필요한 데이터만 비동기적으로 받아와 화면에 그린다(렌더링한다).

### 1.2. Core Technology

1. JavaScript, DOM
2. Fetch

SPA에서도 이야기했었던 새로운 웹페이지를 요청하고 새로운페이지를 가져오는 방식에서 Fetch를 사용하여 현재 페이지에서 작업을 하는 동안 서버와 통신할 수 있도록, Fetch가 서버에 요청을 보내고, 응답을 받을 때까지 페이지를 멈추지 않고 계속 사용할 수 있도록하는 비동기적인 방식이다.

### 1.3. XHR & Fetch

Fetch이전에는 XHR(XMLHttpRequest)을 사용했다. XHR의 단점을 보완하고, XML보다 가볍고 JS와 호환되는 JSON을 사용하는 것이 Fetch이다.

XHR은 Cross-Site 등의 이슈가 있었고, Fetch는 promise의 지원과 같은 장점이 있다.

```javascript
// XMLHttpRequest
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://127.0.0.1:3000/information);
xhr.onreadystatechange = function(){
  if(xhr.readyState !=== 4) return;
  //readyState 4: 완료

  if(xhr.status === 200){
    //200성공
    console.log(xhr.responseText);//서버 응답
  }

  console.log('error: ' + xhr.status);//요청 중 에러
}

xhr.send();//요청 전송

// Fetch 사용문 promise 지원
fetch('http://127.0.0.1:3000/information')
  .then((response) => response.json();)
  .then((json) => ...);
```

### 1.4. AJAX 장점

- Server에서 HTML을 완성하여 보내주지 않아도 웹페이지를 만들 수 있다.

  이전에는 서버에서 HTML을 완성해 전송받아야 화면에 렌더링할 수 있었으나, AJAX사용 이후 서버에서 완성된 HTML을 전송 받지 않아도 필요한 데이터를 비동기적으로 가져와 브라우저 화면 일부만 업데이트하여 렌더링 할 수 있게 되었다.

- 표준화된 방법

  이전 브라우저마다 다른 방식으로 AJAX를 사용했으나, XHR이 표준화되면서 브라우저에 상관없이 AJAX를 사용할 수 있게 됬다.

- 유저 중심 애플리케이션 개발

  AJAX를 사용하면 필요한 일부분만 렌더링하기 때문에 빠르고 더 많은 상호작용이 가능한 애플리케이션을 만들 수 있다.

- 더 작은 대역폭

  이전에는 서버로부터 완성된 HTML파일을 받아왔기에 한번에 보내는 데이터의 크기가 컷으나, AJAX에서는 필요한 데이터를 텍스트(JSON, XML 등)로 보내기에 '비교적' 데이터의 크기가 작다.

> 대역폭: 네트워크 통신 한 번에 보낼 수 있는 데이터의 크기

### 1.5. AJAX 단점

- Search Engine Optimization(SEO)에 불리

  AJAX방식의 웹 애플리케이션은 한번 받은 HTML을 렌더링 후, 서버에서 비동기적으로 필요한 데이터를 가져와 그린다. 처음 받는 HTML 파일에는 데이터를 채우기 위한 틀만 작성되어 있는 경우가 많다. 크롤링(?)과 같이 검색엔진이 데이터가 없는 틀만 읽을 시 원하는 정보를 모아 유저에게 검색결과를 보여줄 수 없다.

- 뒤로가기 문제

  일반적으로 유저가 뒤로가기를 누를 시 이전 상태를 유지할것이라 생각하겠지만(UX적으로 근래에는 이전상태를 유지하는 사이트가 많다), AJAX 자체적으로는 이전상태를 기억하진 못하여 History API를 사용한다.

## 2. SSR & CSR

### 2.1. Server Side Rendering(SSR)

|---|---|---|---|
|HTML|JS|React|onResume|
|Server Sending Ready to be rendered HTML Response to Browser|Browser Renders the page, Now Viewable, and Browser Downloads JS|Page Now Interactable|

웹페이지를 브라우저가 아닌 서버에서 렌더링한다.

1. 브라우저가 서버의 URI로 GET 요청 전송
2. 서버는 정해진 웹페이지 파일 브라우저로 전송
3. 서버의 웹페이지가 브라우저에 도착하기 전 완전 렌더링
   - 데이터베이스의 데이터가 필요한 경우 데이터를 불러와 입히고 렌더링이 끝나면 클라인트에 응답한다.

페이지 이동시 위 동작(서버가 웹페이지를 보낸다)을 반복한다.

### 2.2. Client Side Rendering(CSR)

|---|---|---|---|
|HTML|JS|React|onResume|
|Server Sending Response to Browser|Browser Downloads JS|Brower executes React|Page Now Viewable and Interactable|

클라이언트에서 페이지를 렌더링한다.

1. 브라우저(클라이언트)의 요청을 서버로 보내면 웹페이지의 골격이 될 단일 페이지(Single Page)를 클라이언트에 보낸다.
2. 서버는 웹페이지와 함께 JS파일을 보낸다.
3. 클라이언트가 웹 페이지를 받으면, 웹페이지와 함꼐 전달된 JS파일은 브라우저의 웹페이지를 완전히 렌더링된 페이지로 바꾼다.
   - 브라우저는 데이터베이스에 저장된 데이터를 가져와서 웹페이지에 렌더링해야한다. 이에 Fetch같은 API가 필요하다.

페이지 이동 시 SSR과 같이 서버가 웹페이지를 다시 보내지 않고, 브라우저는 브라우저가 요청한 경로에 따라 이미 받아온 페이지를 다시 렌더링한다.

### 2.3. 차이점

페이지가 렌더링되는 위치이다. SSR(Server Side Rendering), CSR(Client Side Rendering) CSR은 동적으로 라우팅을 관리한다.

- SSR usage

  - SEO(Search Engine Optimization)가 우선순위인 경우
  - 웹 페이지 첫 화면 렌더링이 빠르게 필요할 경우 -> 단일 파일의 용량이 작아 유리
  - 웹 페이지가 사용자와 상호작용이 적은 경우, SSR 활용가능.

- CSR usage
  - SEO가 우선순위가 아닌 경우
  - 사이트에 풍부한 상호작용이 있는 경우, CSR은 빠른 라우팅으로 강력한 UX 제공

## 참조

> [MDN:SEO](https://developer.mozilla.org/ko/docs/Glossary/SEO)  
> [MDN:Progressive Web App Structure](https://developer.mozilla.org/ko/docs/Web/Progressive_web_apps/App_structure)
