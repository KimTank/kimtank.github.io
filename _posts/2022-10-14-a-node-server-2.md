---
layout: post
title: "Node Express"
date: 2022-10-14
categories:
  - NodeJS
tags:
  - Node
  - JavaScript
  - Express
  - Framework
  - Mddleware
  - Router
  - npm
---

서버 안보여서 더 어렵게 느껴지는것.

---

MERN stack(MongoDB, Express, React, Node.js)

Node.js환경에서 웹서버, 또는 API서버를 제작하기 위해 사용되는 framework

## 1. Express install

```bash
$npm install express
```

## 2. Simple started

```javascript
const express = require("express");
const app = express();
const port = 8080;
const ip = "192.168.0.1";

app.get("/", (req, res) => {
  res.send("server open");
});

app.listen(port, ip, () => {
  console.log(`terminal log: ${ip}/:${port}`);
});
```

method와 url(/endpoint)로 분기를 만드는것을 Routing이라고 한다.

Client는 특정한 HTTP Request Method(GET, POST, PUT, PATCH, OPTION, DELETE 등)와 함꼐 특정 URI, path로 HTTP Request 보낸다.

Routing은 Client의 Request에 맞는 Endpoint에 따라 Server Response 방법을 결정한다.

```javascript
//Node.js 방식
const requestHandler = (req, res) => {
  if (req.url === "/endpoint") {
    if (req.method === "GET") {
      res.end(data);
    } else if (req.method === "POST") {
      req.on("data", (req, res) => {
        // do something ...
      });
    }
  }
};

//Express framework 내에서 Router 제공
const router = express.Router();

router.get("/endpoint", (req, res) => {
  res.send(data);
});

router.post("/endpoint", (req, res) => {
  // do something...
});
```

|---|---|---|
|Incoming Request|||
|↓||ㅣ|
|Middleware|ㅡ|ㄱ|
|↓next()|ㄱ||
|MiddleWare|ㅣ|ㅣres.send()|
|↓next()|ㅣres.send()|ㅣ|
|MiddleWare|ㅣ|ㅣ|
|↓next()|↓|↓|
|Res-|pon-|se|

Middleware는 중간에 문제가 있는 요청을 검증하거나 기능을 추가한다던가의 중간자의 역할을 가능하게한다.

## 3. frequency usage middleware

1. POST request 등 포함된 body(payload)를 구조화(쉽게 얻고 싶음)
2. - request/response에 CORS header 추가 시
3. - request -> url이나 method를 확인 시
4. requst에 사용자 인증 정보(certification)가 있는지 확인

### 3.1. POST request 등에 포함된 body(payload)를 구조화할 때

````javascript
// # 1. nodeJS, chunk: 조각
let body = [];
request.on('data', (chunk) => {
  body.push(chunk);
}).on('end', () => {
  body = Buffer.concat(body).toString();
  // body 변수에는 문자열 형태로 payload가 담겨져 있습니다.
});

/**
 * body-parser middleware를 사용하여 효율적으로 바꿀 수 있음.
 * ```bash
 * $npm install body-parser
 * ```
 */
// # 2. body-parser middleware usage
const bodyParser = require('body-parser');
const jsonParser = bodyParser.json();

...

app.post('/endpoint', jsonParser, (req, res) => {
    //action
})

// # 3. Express v4.16.0 ~ body-parser
const jsonParser = express.json(/* TODO 확인 -> {strict: false} */);

...

app.post('/resource/endpoint', jsonParser, (req, res) => {
    //action
});
````

### 3.2. \* Req/Res CORS header added

```javascript
// # 1. NodeJS
const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10
};

...

if (req.method === 'OPTIONS') {
  res.writeHead(responseCode, defaultCorsHeader);
  res.end();
} else if {
  res.writeHead(...);
  ...
} else if ... //계속 반복

/**
 * $npm install cors
 */
// # 2. cors middleware usage
const cors = require('cors');

...

//모든 요청 OK
app.use(cors());

//특정 요청만 CORS 허용
app.get('endpoint/:parameter', cors(), (req, res, next) => {
    res.json({msg: 'this is CORS-enabled for a Specific Single Route'});
});
```

### 3.3. \* req about url or method verify

```javascript
/**
 * get: middleware function(이하 m-w f) HTTP method
 * '/': m-w f, path, route
 * function parameter: m-w f
 * req: m-w f, HTTP request parameter
 * res: m-w f, HTTP response parameter
 * next: m-w f, callback parameter
 */
app.get('/', (req, res, next) {
    next();
});

// # usage
const express = require('express');
const app = express();

const loggerBot = (req, res, next) => {
    console.log(`${req.method}, ${req.url}`);
    next();
};

app.use(loggerBot);

app.get('/', (req, res) => {
    res.send('server open');
});

app.listen(8080);
```

### 3.4. req header in user certification verify

```javascript
app.use((req, res, next) => {
  if (req.header.token) {
    req.isLoggedIn = true;
    next();
  } else {
    res
      .status(/* responseCode user certification Denied */)
      .send("no authority");
  }
});
```

---

## 참조

> [velog:soshin0112/Node.js CORS, SOP](https://velog.io/@soshin0112/Node.js-CORS-SOP-%EA%B0%9C%EB%85%90)  
> [Express.js:Routing](https://expressjs.com/ko/guide/routing.html)  
> [Express.js:main](https://expressjs.com/ko/)  
> [Express.js:getting started](https://expressjs.com/ko/starter/installing.html)  
> [Express.js:Hello, World!](https://expressjs.com/ko/starter/hello-world.html)  
> [Express.js:Basic routing](https://expressjs.com/ko/starter/basic-routing.html)  
> [Express.js:middleware/body-parser](http://expressjs.com/en/resources/middleware/body-parser.html)  
> [Express.js:express.json](https://expressjs.com/ko/4x/api.html#express.json)  
> [Express.js:cors](http://expressjs.com/en/resources/middleware/cors.html)
