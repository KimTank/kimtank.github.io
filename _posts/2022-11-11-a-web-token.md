---
layout: post
title: "Web token"
date: 2022-11-11
categories:
- Web
tags:
- Javascript
- Web
- Token
- Hash
- Sha1
- rainbow table
- salt
- json web token
- JWT
- session
- access token
- refresh token
- header
- payload
- signature
- base64
---

보이지 않는것을 아는 것은 매우 어렵다. 실제로 동작하는걸 확인할 수 없기 때문이다. 다른사람이 만들어놓은 라이브러리를 쓰는것과 같은 느낌이지만, 더 효율적이고 생산적인 방법이 없다면 써야지. 알아야지.

---

## 1. Hasing

가장 많이 쓰이는 암호화 방식 중 하나로, 복호화가 가능한 다른 암호화 방식과 달리, 암호화만 가능하다.

Hash Function을 사용하여 암호화를 한다.

### 1-1. 특징

- 같은 길이의 문자열을 반환
- 서로 다른 문자열에 동일한 Hash Function 적용 시 반드시 다른 값 도출
- 동일한 문자열에 동일한 Hash Function을 사용하면 항상 같은 결과값 도출

[온라인 Sha1 생성기](https://www.convertstring.com/ko/Hash/SHA1)

### 1-2. rainbow table & salt

같은 결과값이 나온다는 특성을 이용해 Hash Function을 거치기 전 값을 알아낼 수 있도록 기록해놓은 rainbow table있다.

복호화가 쉽기때문에 보안에 위협이 될 수 있다. 이때 데이터가 유출이 되더라도 소금을 쳐 이전 값을 알아내기 어렵게 만드는 salt가 있다.

|---|---|
|hongsiiscute|4DE6F33A9FC0F84F0441F3DD3F28BA5F213FADE3|
|hongsiiscute + salt|829F6984F6E5B83E70B4534BFD0FC244525DB1DB|
|---|---|
|ggamsiishandsome|4E5A087854034DA4A62C5D8CBBF3C1A380274BE4|
|ggamsiishandsome + cat|16385FEB0D15E49AAC00BF629FE907749A45FE2C|

### 1-3. 목적

데이터를 사용하는게 아니라 동일한 값의 데이터를 사용하고 있는지의 여부만 확인하는 것이 목적이다.

DBA역시 유저의 복호화를 하는 key(salt)를 알 수 없으면 단순하게 유저가 입력한 비밀번호가 서버에 저장된 비밀번호와 일치하는지의 여부만 알 수있다.

이런 목적으로 Hashing은 데이터 유출의 위험성을 줄이고, 데이터의 유효성을 검증하기 위한 단방향 암호화 방식이다.

## 2. Token

출처: [보배드림 유머게시판](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.bobaedream.co.kr%2Fview%3Fcode%3Dstrange%26No%3D1594166&psig=AOvVaw0YO2FIGwKRIsNZGl4Yh5_h&ust=1668693576817000&source=images&cd=vfe&ved=0CBAQjhxqFwoTCKi3q5DusvsCFQAAAAAdAAAAABAE)
[https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.bobaedream.co.kr%2Fview%3Fcode%3Dstrange%26No%3D1594166&psig=AOvVaw0YO2FIGwKRIsNZGl4Yh5_h&ust=1668693576817000&source=images&cd=vfe&ved=0CBAQjhxqFwoTCKi3q5DusvsCFQAAAAAdAAAAABAE](https://file1.bobaedream.co.kr/strange/2016/10/17/18/1476695093467.png)

나는 돈을 지불했고, `야삐`를 위한 버튼을 누를 자격이 있어.(50개가 걸리면 50배를 먹는 국허유마 국딩 도박기계)

서버가 지는 부담을 클라이언트에게 암호화를 통하여 저장하게한다. 이로서 분산된 정보로 서버의 부담은 줄어든다.

착안: session인증 -> Sv or DB에 유저 정보를 저장 -> Ct에게 부여하자 -> 대표적 token기반 인증 -> JSON Web Token(JWT)

### 2-1. JSON Web Token

JWT는 Access Token과 Refresh Token으로 나눈다.

1. Access Token: 보호된 정보들에 접근할 수 있는 권한부여에 사용한다.
2. Refresh Token: 클라이언트가 처음 인증을 받게 될 시 두 토큰을 다 받지만, 권한을 얻는데 사용하는 토큰은 AT이다. 하지만 악의적 공격에 대비해 권한을 부여하는 AT은 기한을 짧게 잡고, 토큰을 탈취당하더라도 사용할 수 없게 만들고, AT이 만료되면 RT으로 새 AT을 발급받는다.

> Refresh Token까지 탈취당하는 경우 정말로 보안상 문제가 발생하므로 UX적 접근보다 정보보안이 중요할 시 RT를 사용하지 않는 곳이 많다.

```json
header.payload.signature
111111.2222222.333333333
```

- header: 어떤 종류의, 어떤 알고리즘으로 암호화하는가?

  ```json
  {
    "alg": "HS256",
    "typ": "JWT"
  }
  ```

- payload: 유저의 정보, 권한 부여 여부, 기타 정보

  ```json
  {
    "sub": "1234567890",
    "name": "ty",
    "iat": "05500061"
  }
  ```

  > 민감한 정보는 담지 않는것이 좋음. base64 인코딩은 간단

- signature: header, payload를 base64 encoding한 값과 salt값의 조합으로 암호화된 값

  ```json
  HMACSHA256 (
    BASE64URL(header) +
    '.' +
    BASE64URL(payload),
    seceret
  )
  ```

  악의적 공격에 탈취당하더라도 서버의 비밀키를 모른다면 Signiture가 일치하지 않아 인증이 되지 않는다.
  
### 2-2. 절차

1. from Ct to Sv access request
2. access requst's information verify, Sv create encryption key(AT, RC both created, not neccessary same information)
3. from Sv to Ct, Ct save token.(location: [Local Storage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage), [Session Storage](https://developer.mozilla.org/ko/docs/Web/API/Window/sessionStorage), [Cookie](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cookie))
4. from Ct to Sv, HTTP header(Authoriztion header) or cookie contain token, Authorization header usage(bearer authentication, [summary](https://learning.postman.com/docs/sending-requests/authorization/#bearer-token)/[detail](https://tools.ietf.org/html/rfc6750))
5. Sv decoding token who sended by Cv, if match true, send form Sv to Ct success response.


Ct -> POST /login(id, pwd) request -> Sv -> id, pwd 확인(DB or store) -> JWT token created -> JWT Token response -> Ct

Ct -> Get /information (Headers: {Authoriztion: "Bearer JWT_TOKEN"}) -> Sv -> JWT Token get -> access -> from request action to response action logic -> response information -> Ct

### 2-3. 장점

1. Statelessness & Scalability: 무상태성과 확장성으로 서버는 클라이언트에 대한 정보를 저장할 필요가 없고, 토큰을 헤더에 추가해 인증을 완료한다.(토큰이 해독되는지 판단만)
   - 서버가 여러개일 때 성능이 더 좋다. session같이 서버에서 저장할 시 여러서버가 모두 session에 대한 정보를 가지고 있어야 한다.
2. Stability: 안정성으로 암호화한 토큰을 사용하고, 암호화 키를 노출할 필요가 없다.
3. anywhere created: 토큰을 생성하는 서버가 만들지 않아도 되어 아무데서나 만들 수 있다.(다른회사조차도 가능(토스))
4. authorization: token의 payload 내부 정보에 접근 가능여부를 정할 수 있다.

---

## 참조

> [convertstring: hash/sha1](https://www.convertstring.com/ko/Hash/SHA1)   
> [mdn: local storage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)   
> [mdn: session storage](https://developer.mozilla.org/ko/docs/Web/API/Window/sessionStorage)   
> [mdn: cookie](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cookie)   
> [postman: authorization/bearer token](https://learning.postman.com/docs/sending-requests/authorization/#bearer-token)   
> [tool ietf: rfc6750](https://tools.ietf.org/html/rfc6750)