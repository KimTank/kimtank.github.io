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

착안: session인증 -> Sv or DB에 유저 정보를 저장 -> Ct에게 부여하자 -> 대표적 token기반 인증 -> JSON Web Token(JWT)

### 2-1. JSON Web Token

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

  > 민감한 정보는 담지 않는것이 좋다.

- signature: header, payload를 base64 encoding한 값과 salt값의 조합으로 암호화된 값

  ```json
  HMACSHA256 (
    BASE64URL(header)
    .
    BASE64URL(payload),
    secret
  )
  ```
  
### 2-2. 절차

Ct -> POST /login(id, pwd) request -> Sv -> id, pwd 확인(DB or store) -> JWT token created -> JWT Token response -> Ct

Ct -> Get /information (Headers: {Authoriztion: "Bearer JWT_TOKEN"}) -> Sv -> JWT Token get -> access -> from request action to response action logic -> response information -> Ct

### 2-3. 장점

1. Statelessness & Scalability: 무상태성과 확장성으로 서버는 클라이언트에 대한 정보를 저장할 필요가 없고, 토큰을 헤더에 추가해 인증을 완료한다.
2. Stability: 안정성으로 암호화한 토큰을 사용하고, 암호화 키를 노출할 필요가 없다.
3. anywhere created: 토큰을 생성하는 서버가 만들지 않아도 되어 아무데서나 만들 수 있다.
4. authorization: 


---

## 참조

> [convertstring: hash/sha1](https://www.convertstring.com/ko/Hash/SHA1)   
> []()   
> []()   
> []()   
> []()   
> []()