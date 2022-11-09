---
layout: post
title: "Network deep vol.2"
date: 2022-11-09
categories:
- Network
tags:
- Network
- Client
- Server
- Stateless
- Connectionless
- Representation Headers
- Content Type
- Content Encoding
- Content Language
- Content Length
- Transfer Encoding
- Request Headers
- From
- Referer
- User Agent
- Host
- Origin
- Authorization
- Response Headers
- Server
- Date
- Location
- Allow
- Content Negotiation Headers
- Accept
- Accept Charset
- Accept Encoding
- Accept Language
- Quality Values
---

ㅑㅑㅑㅑㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐ
고양이가 말했습니다

---

## 1. HTTP 특징

### 1-1. 역사

|---|---|---|---|
|연도|version|spec|note|
|1991|HTTP/0.9|GET method only||
|||HTTP header X||
|1996|HTTP/1.0|method, header added|tcp|
|1997|HTTP/1.1 RFC2068|현재 사용버전|tcp|
|1999|         RFC2616||tcp|
|2014|         RFC7230~7235||tcp|
|2015|HTTP/2|성능 개선|tcp|
|현재|HTTP/3 개발중|UDP사용 성능개선|udp|

### 1-2. 특징

- Client Server
  - Request Response
  - Ct -> req -> Serv -> rep -> Ct
- Stateless, Connectionless(무상태 프로토콜, 비연결성)
  - Stateful: 서버(점원?)가 상태를 기억하는 것을 유지함.
  - Stateless: 클라이언트(고객)가 상태를 기억함.
    - good: 서버 확장성 높음(scale out)
    - bad: 클라이언트 추가 데이터 전송
    - limit: 무상태로만 가능할수도 하지않을수도 있음.(ex: 로그인 필요할 시 브라우저 쿠키, 서버 세션, 토큰 등 이용)
  - Connection Oriented: 연결을 유지하는 모델 -> 연결을 유지하는 서버의 자원 계속 소모
  - Connectionless: 서버 연결유지 X, 최소한의 자원 사용
    - 기본 연결을 유지하지 않는 모델
    - 초단위 이하의 빠른 응답
    - 1시간 내 수천명이 서비스를 이용해도 실서버에서 동시 처리요청은 수십개 이하
    - limit
      - TCP/IP 연결 새로 맺어야됨, 3 way handshake 시간 증가
      - HTML 외 js, css, asset등 많은 자원이 함께 다운로드
      - Persistent Connections(지속 연결)로 해결
      - HTTP/2, HTTP/3에서 최적화
- HTTP Message
- 단순함, 확장성

### 1-3. HTTP header

#### 1-3-1. Representation Headers

표현 헤더는 표현 헤더와 표현 데이터로

```json
HTTP/1.1 200OK
Content-Type:text/html;charset=UTF=8
Content-Length:3423
// 표현헤더
//<field-name>:<field-value>

<html>
   <body>...</body>
</html>
//표현 데이터
```

- msg body를 통해 표현 데이터 전달한다.
- msg body = payload
- 표현: 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더: 표현 데이터를 해석할 수 있는 정보 제공(데이터 유형(html, json), 데이터 길이, 압축 정보 등)
- HTTP header
  - 전송에 필요한 모든 부가정보: msg body content, msg body size, auth, req client, server info, cache admin info
  - 너무 많음.[List of HTTp header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
  - 필요 시 임의헤더 추가 가능
- Representation Headers(요청, 응답 둘다 사용)
  - Content-Type: 표현 데이터의 형식
    - mediaType;encoding
  - Content-Enhoding: 표현 데이터의 압축 방식
    - 표현 데이터 압축위해 사용
    - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
    - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  - [Content-Language: 표현 데이터의 자연 언어](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Language)
  - [Content-Length: 표현 데이터의 길이](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Length)
    - 단위 byte
    - [Transfer-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Transfer-Encoding)을 사용 시 Content-Length 금지: chunked방식

#### 1-3-2. Request Headers

1. From: 유저 에이전트의 이메일 정보
   - 검색엔진 주로 사용
   - 요청에 사용
2. Referer: 이전 웹 페이지 주소
   - 현재 요청된 페이지 이전 웹 페이지 주소
   - A->B 시 B요청할때 Referer: A 포함
   - 유입경로 수집가능
   - referrer 오탈자지만 referer로 굳어짐
3. User-Agent: 유저 에이전트 애플리케이션 정보
   - 클라이언트 애플리케이션 정보
   - 통계 정보
   - 어떤 종류의 브라우저에서 장애 발생하는지 파악 가능
4. Host: 요청한 호스트 정보(domain)
   - 필수 header
   - 하나의 서버에 여러 도메인을 처리해야 할때 호스트 정보 명시위해 사용
   - 하나의 ip주소에 여러 도메인이 적용도ㅟ 있을 때 호스트 정보 명시위해 사용
5. Origin: 서버로 POST 요청을 보낼 때, 요청을 시작한 주소를 나타냄
   - 보낸주소, 받는주소 다르면 CORS 에러 발생
   - 응답 헤더 Access-Control-Allow-Origin과 관련
6. Authorization: 인증 토큰을 서버로 보낼 때 사용하는 헤더
   - 토큰의 종류 + 실제 토큰 문자를 전송

#### 1-3-3. Response Headers

1. Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
2. Date: 메세지가 발생한 날자와 시간
3. Location: 페이지 리다이렉션
   - 3xx응답 결과에 Location헤더 있으면 Location위치로 리다이렉션
   - 201(created): Location값은 요청에 의해 생성된 리소스 URI
4. Allow: 허용 가능한 HTTP메서드
   - 405(Method Not Allowed)에서 응답에 포함

#### 1-3-4. [Content negotiation Headers](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation)

클라이언트가 선호하는 표현 요청(콘텐츠 협상)
협상헤더는 요청시에만 사용

- Accept: 클라이언트가 선호하는 미디어 타입전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클아이언트가 선호하는 자연 언어
  - A-L except: Ct(ko브라우저) -> Get /event -> Serv(다중 언어 지원, en, ko) -> Content-Language:en -> Ct(Hi)
  - A-L use: Ct(ko) -> Get /event -> A-L:ko -> Serv(다중 언어 지원, en, ko) -> Content-Language:ko -> Ct(안녕)
  - A-L complex: Ct(ko) -> Get /event -> A-L:ko -> Serv(다중 언어 중 한글없음, fr, en) -> Content-Language:fr => Ct(Bonjour)
    - Quality Values(q)
      ```json
      GET /event
      Accept-Language:ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
      ```
      - 0~1, 클수록 순위 높음
      - 생략 시 1
  - A-L Q-V use -> Get /event -> Accept-Language;ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7 -> Serv(다중 언어 중 한글 없음, fr, en) -> Content-Language: en -> Ct(Hi)

---

## 참조

> [wiki: List of HTTP header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)   
> [mdn: http/header/content-language](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Language)   
> [mdn: http/header/content-length](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Length)   
> [mdn: http/header/transfer-encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Transfer-Encoding)   
> [mdn: http/content negotiation](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation)