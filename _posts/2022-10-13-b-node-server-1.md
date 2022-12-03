---
layout: post
title: "Node Cross Origin Resource Sharing"
date: 2022-10-13
categories:
  - NodeJS
tags:
  - Node
  - JavaScript
  - Cross Origin Resource Sharing
  - CORS
  - PreFlight Request
  - nodemon
  - serve
  - middleware
---

눈뜨니 침대 뭔가싶다. 껄껄

---

교차 출처 리소스 공유

## 1. MDN 개념

교차 출처 리소스 공유는 추가 HTTP헤더를 사용, 한 Origin에서 실행 중인 Web Application이 다른 Origin이 선택한 자원에 접근할 수 있는 권한을 부여하도록 Client(브라우저)에 알려주는 체제이다.

Clinet(브라우저)는 SOP에 의해 다른 출처의 리소스 공유를 막는다. 그러나, CORS를 사용하면 접근권한을 얻을 수 있다.

```
X Access to fetch at 'protocol path ...' from origin 'null' has been blocked by ....html:1 CORS policy: Response to preflight reque4st doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaue response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.

<!--
  다른 출처의 리소스 갖고오기엔 SOP로 접근 불가.
  CORS 설정으로 서버 응답 헤더에 'Access-Control-Allow-Origin'을 작성, 접근권한 얻을 수 있어.
 -->
```

상기 에러 CORS가 아닌 SOP -> CORS를 통해 해결 가능.

## 2. How act

### 2.1. PreFlight Request

#### 2.1.1. 개념

실 요청 보내기 전 OPTIONS 메서드로 사전 요청으로 보내, 해당 출처 리소스에 접근 권한 있는지 확인하는 것.

#### 2.1.2. Structure

|---|---|---|---|---|---|
|클라이언트||브라우저||서버||
|ㅣ|-실요청→|ㅣ|-Preflight Request(Origin: path)→|ㅣ||
|ㅣ||ㅣ|←Response(A-C-A-O: path)-|ㅣ||
|ㅣ||ㅣ|-실요청→|ㅣ||
|ㅣ|←Response-|ㅣ|←Response-|ㅣ|ㅡ요청 수행|

> A-C-A-O: Access-Control-Allow-Origin

#### 2.1.3. Server Side has no Response Header

|---|---|---|---|---|---|
|클라이언트||브라우저||서버||
|ㅣ|-실요청→|ㅣ|-Preflight Request(Origin: path)→|ㅣ|
|ㅣ|←CORS-|ㅣ|←Response(A-C-A-O: 응답헤더 없엉)-|ㅣ|

> 요청을 보낸 Origin에 접근 권한이 없으면, 브라우저에서 Cors error thorw, 실 요청 전달 안됨.

#### 2.1.4. why PreFlight Request require

- 리소스 측면에서 효율적: 실 요청 전 권한 확인 가능
- CORS 대비안된서버 보호: CORS이전 SOP만 고려, 다른 Origin 대응 안해놓음.

|---|---|---|---|---|---|
|클라이언트||브라우저||서버||
|ㅣ|-실요청(Origin: path)→|ㅣ|-실제 요청(Origin: path)→|ㅣ|요청-|
|ㅣ|←CORS 에러-|ㅣ|←Response(A-C-A-O: 응답헤더 없엉)-|ㅣ|수행|

> 서버 요청을 받은 후 CORS를 확인하여 응답 헤더가 없을 시 error throw, -> 비효율적 하여 PreFlight는 CORS 기본 사양

### 2.2. Simple Request(단순 요청)

특정 조건이 만족되면, 프리플라이트 요청 생략 후 요청 보냄.

|---|---|---|---|
|클라이언트||서버||
|ㅣ|-실제 요청(Origin: path)→|ㅣ|요청|
|ㅣ|←Response(A-C-A-O: \*)-|ㅣ|수행|

- GET, HEAD, POST method 중 하나이다.
- 자동으로 설정되는 헤더
  - Accept
  - Accept-Language
  - Content-Language
- 수동으로 설정
  - Content-Type
    - application/x-www-form-unlencoded
    - multipart/form-data
    - text/plain

### 2.3. Credentialed Request(인증정보를 포함한 요청)

요청 헤더에 인증 정보 담은 요청, Origin다른 경우 별도 설정없이 쿠키 보낼 수 없다. 민감한 정보이므로 Client, Server 모두 CORS 설정이 필요하다.

- Client측 요청 헤더
  - withCredentials: true
- Server측 요청 헤더
  - Access-Control-Allow-Credentials: true
- Access-Control-Allow-Origin: \* -> error throw -> 인증정보의 경우 출처 정확하게 설정해야 한다.

## 3. setting

### 3.1. Node.js Server

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  // 모든 도메인
  res.setHeader("Access-Control-Allow-Origin", "*");

  // 특정 도메인
  res.setHeader("Access-Control-Allow-Origin", `${host}${path}`);

  // 인증 정보를 포함한 요청을 받을 경우
  res.setHeader("Access-Control-Allow-Credentials", "true");
});
```

```javascript
const cors = require("cors");
const app = express();

//모든 도메인
app.use(cors());

//특정 도메인
const options = {
  origin: "https://codestates.com", // 접근 권한을 부여하는 도메인
  credentials: true, // 응답 헤더에 Access-Control-Allow-Credentials 추가
  optionsSuccessStatus: 200, // 응답 상태 200으로 설정
};

app.use(cors(options));

//특정 요청
app.get("/endpoint/:parameter", cors(), function (req, res, next) {
  res.json({ msg: "this is message" });
});
```

### 3.2. Express Server

Express framework로 Server 만들 시, cors 미들웨어로 간단하게 CORS설정 가능하다.

## 4. Node.js Server Library

서버 코드 변경 시 리빌드해줄 필요 없이 자동으로 리빌드해준다.

```json
./package.json
...
dependencies {
  ...,
  "start": "nodemon server/basic-server.js"
}
```

```bash
# terminal
$npx nodemon servr/serverScriptFile.js
```

### 4.1. 특정 포트로 실행

```bash
$npx serve -l portNumber client/
```

---

## 참조

> [velog:soshin0112/Node.js CORS, SOP](https://velog.io/@soshin0112/Node.js-CORS-SOP-%EA%B0%9C%EB%85%90)  
> [NodeJS:HTTP](https://nodejs.org/dist/latest-v16.x/docs/api/http.html)  
> [NodeJS:HTTP transaction anatomic](https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction/)  
> [Github:Nodemon](https://github.com/remy/nodemon)  
> [Github:Serve](https://github.com/vercel/serve)
