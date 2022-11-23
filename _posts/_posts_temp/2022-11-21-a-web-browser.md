---
layout: post
title: Web Browser
date: 2022-11-21
categories:
- Web
tags:
- Web
- Browser
- 
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
- JavaScript Interpreter: 한줄씩 읽어 내려가는 Inpterpre


---

> ## 참조
>
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   