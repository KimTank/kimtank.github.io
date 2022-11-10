---
layout: post
title: "Web session"
date: 2022-11-10
categories:
- Web
tags:
- Javascript
- Web
- session
- sessionId
---

헐 과제 헐

---

## 1. Session

Sv가 Ct에게 unique, encryption id 부여하고, 중요 데이터는 서버가 관리한다.

### 1-1. Cookie와 비교

|---|---|---|
|\|Cookie|Session|
|설명|쿠키는 그저 http의 stateless한 것을 보완해주는 도구|접속 상태를 서버가 가짐(stateful), 접속 상태와 권한 부여를 위해 세션 아이디를 쿠키로 전송|
|접속상태 저장경로|Ct|Sv|
|장점|Sv부담줄어듬|신뢰할수있는 유저인지 서버에서 추가 확인 가능|
|단점|쿠키 그 자체는 인증이 아님|하나의 서버에서만 접속 상태를 가지므로 분산에 불리|

단점: 서버에 가용메모리를 잡고있어 서버성능이 저하됨.
cookie를 사용하고 있어, XSS공격에 취약

### 1-2. flow

Ct -> 로그인 -> Sv -> DB 저장 -> session store(sessionId, user info) -> sessionId 반환 -> Sv -> Set-Cookie: session_id=암호화된아이디 -> Ct -> sessionId, user action -> Sv -> sessionId check & update -> Ss -> s-i유효 & update -> Sv -> user action done -> Ct

- 인증에 따라 리소스 Authorization(접근 권한)이 달라진다.
- 웹사이트에서 로그인을 유지하기 위한 수단으로 cookie사용, cookie에 Sv에서 발급한 sessionId저장한다.
- sessionId없으면 인증되지 않았다고 응답한다.
- 용어
  - Sv: 사용자가 인증에 성공했음을 알고 있다.
  - Ct: 인증 성공 증명할 수단 갖고 있다.
  - session: 인증에 성공한 상태(in-memory(js object) or [redis](https://redis.io/)(트랜잭션이 빠른 DB))
  - sessionId: 세션을 구분할 수 있는 id, 세션 성공을 증명할 수단이다.

> 로그아웃 시   
> 
> - Sv: 세션 정보 삭제   
> - Ct: 쿠키 갱신 -> Ct의 cookie임의 삭제 불가능하여, set-cookie로 Ct에게 cookie전송 시 sessionId keyVal 무효화로 갱신.

## 2. nodejs express-session 모듈(middle-ware)

```javascript
const express = require('express');
const session = require('express-session');

const app = express();

app.use(
  session({
    secret: '@host',
    resave: false,
    saveUninitialized: true,
    cookie: {
      domain: 'localhost',
      path: '/',
      maxAge: 24 * 6 * 60 * 10000,
      sameSite: 'none',
      httpOnly: false,
      secure: true,
    },
  })
);
```

---

## 참조

> [github: expressjs/session](https://github.com/expressjs/session#reqsession)   
> [redis: main](https://redis.io/)