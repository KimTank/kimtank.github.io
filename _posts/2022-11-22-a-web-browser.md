---
layout: post
title: Web Browser
date: 2022-11-22
categories:
- Web
tags:
- Web
- Browser
- Browser Engine
- Rendering Engine
- Networking
- JavaScript Interpreter
- V9 Engine
- Heap Memory
- Call Stack
- Web Storage
- Local Storage
- Session Storage
---

오랜만에 주말 북악을 다녀왔더니 주말에 노곤노곤해져 푸우우우욱쉬었다. 껄껄

---

## 1. Browser

javascript는 browser(software)에서 컴파일된다음 동작한다. 웹브라우저, 웹탐색기, 웹서버와 클라이언트간 양방향 통신하며, Data(html doc, 그림, 멀티미디어 등)의 resource를 볼 수 있게 해주는 GUI software program(이후 p/g)이다.

- web: World Wide Web, 인터넷상의 resource를 hypertext방식으로 연결해 제공한다.
- web page: html language를 사용해 작성된 문서의 형태
- web site: 서로 관련된 내용으로 작성된 web page의 집합

### 1.1. 특징과 동작원리

user가 선택한 resource를 server에 request, server response를 browser rendering

- resource: 대부분은 html doc이지만, pdf, multi-media 등과 같은 다른 형태일 수 있고, uniform resource identifier(URI) 주소로 접근할 수 있다.

출처: [코드스테이츠](https://www.codestates.com/)
![https://www.codestates.com/](/assets/img/221121-browser-workflow.gif)

1. `user` `web-page url path` `input`, `dns server`
2. `user input url in domain name` `search`
3. `domain name match ip` `find` `user input url information` `send`

4. `web page with recieve ip path` `http protocol` `use` `http request message` `create` `tcp protocol` `use` `throw internet` `send to` `match ip computer`
5. `http protocol` `convert` `webpage url information` `from` `request message`

6. `web server` `search` `converted message in data` `after` `from http protocol` `create` `http response message`
7. `message` `go throw` `tcp protocol` `to internet`, `send to` `user computer`

8. `user computer` `recieve` `http response message`, `use http protocol` `conver to` `webpage data`, `converted data` `rendering on webbrowser` `then float user interface(monitor)` `finally can SEE`

### 1.2. 구조

```
            User Interface →→↓
                        ↓    ↓
            Browser Engine →--→resource repository
                        ↓    ↓============ㄱ  
            Rendering Engine              ㅣ
      ↓=============↓===================↓  ↓
networking | JavaScript Interpreter | UI back-end
```

- UI: user interface, gui부분 통칭
- Browser Engine: UI, Rendering Engine 사이 동작 제어
  - HTML문서와 기타 자원의 웹페이지를 사용자 장치에 시각표현으로 변환, DOM자료구조를 구현한다.
  - Layout Engine이라고도 한다. Rendering Engine과 묶어 Browser Engine이라고도 한다.

    |이름|설명|
    |---|---|
    |Gecko|made by 모질라, firefox 탑재, 유명|
    |Webkit|KHTML 파생, safari 탑재, 가장 유명|
    |Blink|Webkit 파생, chorme, opera 탑재, 유명|
    |Trident|MS 엔진, IE, OE, MS OL탑재, 힘내라 마소|
    |EdgeHTML|Trident 파생, 엣지스파르탄(~2019) -> Blink로 교체|

    > 외에도 많다.

- Rendering Engine: 요청한 자원을 화면에 출력한다. html, css 파싱해 최종적으로 유저가 화면에서 볼 수 있게 paint, html, xml, image, plugin에 따라 pdf도 가능하다.
- Networking: 통신, HTTP 요청과 같은 네트워크 호출에 사용된다. 보통 플랫폼의 독립적인 인터페이스이고, 각 플랫폼의 하부에서 실행됩니다.
- JavaScript Interpreter: 한줄씩 읽어 내려가는 방식으로 parsing하는 Interpreted Language이다. JavaScript코드를 해석하고 실행하는 JavaScript Interpreter가 필요에 의해 만들어지고, JavaScript Engine이라고 부르는 JavaScript Interpreter는 여러 목적으로 사용이 되지만 대체적으로 Web Browser에서 이용이 되고, Browser마다 전용 Engine이 탑재되어 있다.

|이름|설명|
|---|---|
|Rhino|모질라 재단이 운영하는 오픈소스 엔진, Java로 개발되었다는 특징이 있다.|
|SpiderMonkey|최초의 JavaScript Engine 넷스케이프 내비게이터를 지원하였으며, 현재는 파이어폭스를 지원하고 있다.|
|V8|구글이 개발한 오픈 소스 엔진으로 구글 크롬의 JavaScript Engine이다.|
|JavaScriptCore|애플에서 개발하였으며 처음에 WebKit 프레임워크를 위해 개발되었지만 현재는 사파리와 React Native App를 지원하고 있다.|
|Chakra|마이크로소프트가 개발한 엔진이고, Edge 브라우저를 지원하고 있다.|

#### 1.2.1 V8 Engine

##### 1.2.1.1 Heap Memory

동적 메모리 할당에 사용되는 자료구조이다. 객체 또는 동적 데이터를 저장한다. v8 engine내부 가장 큰 공간을 차지하고 있으며, garbage collection이 발생하는 곳이다.

#### 1.2.1.2. Call Stack

JavaScript는 Single Thread 기반 language이다. call stack은 하나이고, 한번에 한 task만 수행할 수 있다. call stack은 프로그램 상에 우리가 어디에 있는지 기록하는 자료구조이다. 만약 함수를 실행한다면, 해당 함수는 call stack의 가장 상단에 위치한다. 이는 stack이 Last In First Out, 후입선출이라는 구조기 떄문이다. 함수가 끝나면 해당 함수는 call stack last in, 가장 상단이니 바로 제거한다.

```javascript
function eat(head, food) {
    return `${head}이(가) ${food}를 먹는다.`;
}

function when(name, food){
  let head = `${new Date(new Date().getTime())} ${name}`;
  return eat(head, food);
}

function printAteHistory(name, food){
  let ouput = when(name, food)
  console.log(output);
}

/**
 *  in----------------------------------out
 *  3 eat(head, food)                  l 1
 *  2 when(name, food)                 l 2
 *  1 printAteHistory('김군', '순대국') l 3
 *  ---------------------------------------
 */
```

콜스택에 쌓이는 데이터 하나하나를 StackFrame이라고 하고, 함수 하나가 프레임 하나이다. 스택프레임들은 순서대로 쌓이므로 trace, 추적(stack trace)이 가능하다.

콜스택은 힙과 달리 자료구조 자체 크기가 제한되 있어 Stack Overflow가 날 수 있다.

### 1.2.2. UI 백엔드

- Command Line Interface: 명령어 라인 인터페이스, 터미널이나 cmd와 같이 문자로만 명령어를 입력해 처리해야 하는 인터페이스를 의미한다.
- Batch Interface: 일괄 처리 인터페이스, 사용자가 배치 처리에 앞서 배치 작업의 모든 세부 사항을 지정하고, 모든 처리가 완료되면 출력을 수신하는 비대화형 사용자 인터페이스이다.(대규모 시스템, 대량 데이터 처리에 사용)

### 1.2.3. 자료 저장소

HTML5 명세에서는 Web Storage의 스펙이 정의되어 있다.

#### 1.2.3.1. Web Storage 특징

HTML5 이전 응용 프로그램이 서버에 데이터를 요청할 때마다 쿠키에다 그 정보를 저장했다. 쿠키는 보안상 취약과 절대적 허용 용량이 적다.

WS는 web browser가 직접 데이터를 저장할 수 있게한다. 사용자 측에 좀 더 많은 양의 정보를 안전하게 저장한다. 위 정보는 절대 서버로 전송하지 않아, 저장된 데이터가 클라이언트에만 존재하여 네트워크 트래픽 비용 또한 줄어든다.

#### 1.2.3.2. 종류

- LocalStorage: 보관기한이 없는 데이터를 저장한다. 브라우저탭이 닫히거나, 컴퓨터를 재부팅해도 저장소의 데이터는 사라지지 않는다. Windows 전역 객체의 localStorage라는 컬렉션을 통해 저장과 조회가 가능하다. 도메인마다 별도의 localStorage가 생성된다. 도메인만 같으면 전역으로 데이터의 공유는 가능하다.
- SessionStorage: 하나의 세션만을 위한 데이터를 저장한다. 데이터를 지속적으로 보관하지 않고 브라우징되고 있는 브라우저 컨텍스트 내에서만 데이터가 유지되어, 사용자가 브라우저 탭이나 창을 닫으면 이 객체에 저장된 데이터는 사라진다.
  - 브라우징: 브라우저 프로그램을 실행해서 인터넷에 들어가 필요한 정보를 찾는 행위이다.
  - 브라우징 컨텍스트: 브라우저가 문서를 표시하는 환경이다. 각 브라우징 컨텍스트는 특정 출처 및 활성화되고 있는 문서의 출처, 표시한 모든 문서의 방문기록을 가지고 있다.

> 저장과 조회는 Windows 전역 객체의 sessionStorage라는 컬렉션을  통해 이루어지고, 도메인별로 별도로 생성된다. 브라우저 컨텍스트가 다르면 서로 다른 영역이 된다. 브라우저 두개를 실행해 같은 페이지를 열었을 때, 브라우저의 컨텍스트가 달라 sessionStorage는 각 별개의 영역으로 인지되어 서로의 데이터 공유가 불가능해진다.
> [버전이 다르면 웹 스토리지를 사용할 수 없기 때문에 반드시 확인해야 한다.](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API)

#### 1.2.3.3 usage

- window.localStorage: 만료 날짜가 없는 데이터를 저장할 때 쓴다.
- window.sessionStorage: 세션이 있는 데이터를 저장할 때 쓴다.(브라우저 탭을 닫으면 손실되는 것을 의도한 데이터를 저장할때 사용)

```javascript
//window객체의 storage객체를 통해 확인
//객체가 존재하지 않는 브라우저면 undefined, 존재시 function return
if(typeof Storage !== 'undefined'){
  //web storage
} else {
  web storage를 지원하지 않는 경우
}
```

브라우저 컨텍스트 내에 저장한 데이터를 가지고 활용할 수 있어 복구 및 백업에 관련된 기능에 사용한다.

- 작성중인 글 내용 복구나 백업
- 입력form에 입력중인 정보
- 서버단에서 처리하지않고, 프론트단에서 처리가 가능한 정보들

---

## 참조

> [mdn: webAPI/Web Storage API](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API)