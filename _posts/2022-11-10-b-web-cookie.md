---
layout: post
title: "Web Cookie"
date: 2022-11-10
categories:
- Web
tags:
- Web
- Authority
- Security
- Cookie
- Cookie Option
- Domain
- Path
- MaxAge
- Expires
- Session Cookie
- Persistent Cookie
- HTTPOnly
- Secure
- SameSite
- XSS
- CSRF
---

점점 시간은 다가오고있다. 한달정도는 늘어져있었던거같은데 개발바닥에서 내가 우려하던 이야기를 그대로 했던거때문일지도 모르겠다만.. 무슨상관인가. 현실이 어떻든 필요한 상품이 되면 그만인것을. 정신차리자

---

## 1. Cookie

HTTP는 stateless라고 했는데 어떻게 내 정보가 유지되는걸까? -> Cookie

쿠키는 서버에서 클라이언트에 연속성있는 데이터를 저장하는 방법이다. 서버가 일방적으로 Ct에게 전달하는 작은 데이터로 Serv가 웹브라우저에 정보를 저장하고 불러올 수 있다. domain에 대한 Cookie가 존재하면, 웹브라우저는 http요청 시 Cookie를 함께 전달한다.

ex) 사용자 선호 테마 등 장기간 보존해야되는 데이터

Serv -> Set-Cookie: data... -> Client -> Cookie: saved data -> Server

### 1-1. Cookie Options

```json
'Set-Cookie':[
  'cookie=information',
  'Secure=Secure; Secure',
  'HttpOnly=HttpOnly; HttpOnly',
  'Path=Path; Path=/cookie',
  'Domain=Domain; Domain=kimtank.github.io'
]
```

- domain: 서버와 요청의 도메인이 일치하는 경우 전송
  - 서버에 접속할 수 있는 이름
  - option에는 port, sub domain information(www, www3...), detail path를 포함하지 않는다.
  - `https://www.kimtank.github.io.github.io`, `kimtank.github.io`만 해당
- path: 서버와 요청의 세부경로가 일치하는 경우 전송
  - detail path, 서버가 라우팅할때 사용하는 경로
  - `https://www.kimtank.github.io.github.io/personal`, `/personal`만 해당, 명시하지 않으면 `/`로 설정
  - 설정된 경로의 하위경로, `/personal/2019/02/04/core-jv-chapter1-basic-programming.html`로 요청하더라도 쿠키 전송 가능
- maxage or expires: 유효기간 설정 -> 일정 시간 후 자동 소멸
  - 유효기간을 설정
  - maxage: 유효한 시간을 초단위로 설정
  - expires: 유요한 날을 설정
  - 기준은 Ct의 시간
    - session cookie: 상기 옵션이 없는 쿠키, 브라우저가 종료되면 삭제
    - persistent cookie(영속성): 상기 옵션의 값에 따르는 쿠키
- httponly: 스크립트의 쿠키 접근 가능 여부 결정
  - script태그로 접근 가능([XSS](https://namu.wiki/w/XSS)공격에 취약), 민감한 정보나 개인정보는 담지말자.
  - true: JS로 쿠키 접근 불가
  - 기본: false, `document.cookie`로 XSS공격 가능
- secure: https protocol에서만 쿠키 전송 여부 결정
- samesite: cors요청의 경우 옵션 및 메서드에 따라 쿠키 전송 여부 결정
  - **유저** 로그인 -> **서버** **유저**에게 유효한 토큰 발행 -> **해커** 서버위장한 위조 요청 **유저**에게 보냄 -> 해커링크 클릭한 **유저**는 **서버**에 위조요청 보냄 -> 위조된 요청은 처음 할당된 **유저**의 유효한 토큰을 통해 **해커**가 정상처리됨([CSRF 공격](https://namu.wiki/w/CSRF))
  - 옵션에 따른 서버의 쿠키 전송 여부
    - Lax: Cross-Origin 요청이면, GET 메서드 요청만 쿠키 전송 가능
    - Strict: 쿠키 전송 불가, same-site인 경우만 가능
    - None: 모든 메서드 요청에 대해 쿠키 전송 가능(Secure 쿠키 옵션 필요)

cookie를 통해 Stateless -> Stateful: Serv -> Ct 인증정보 쿠키 전송 -> Ct 받은 쿠키로 Serv 요청과 같이 전달하여 상태를 유지할 수 있으나, HttpOnly options을 사용하지 않으면 JS이용하여 접근이 가능하므로, 민감한 정보는 담지 않아야 한다.

---

## 참조

> [나무위키: XSS](https://namu.wiki/w/XSS)   
> [나무위키: CSRF](https://namu.wiki/w/CSRF)   
> [mdn: http/headers/set cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)