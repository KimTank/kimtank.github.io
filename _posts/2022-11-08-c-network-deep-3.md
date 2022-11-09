---
layout: post
title: "Network deep vol.3"
date: 2022-11-09
categories:
- Network
tags:
- Network
- https
- 대칭키 암호화
- 비대칭티 암호화
- SSL
- TLS
- Certificate Authority
- CA
- mkcert
- ngrok
---

눈을 감으니 천국의 중심에 누워 꽃내음을 맡으며 단잠을 청하였다.

눈을 뜨니 zoom에서 목이 꺽여 기절했다고 했다 ㄷㄷ

[Network deep vol.1](https://kimtank.github.io/network/2022/11/09/a-network-deep-1.html)
[Network deep vol.2](https://kimtank.github.io/network/2022/11/09/b-network-deep-2.html)

---

## 1. HTTPS

HTTP Secure, HTTP protocol을 더 안전하게 사용할 수 있도록 요청과 응답의 내용을 암호한 한다. HTTP를 하이재킹하면 요청 응답의 내용을 바로 볼 수 있다. 하지만 HTTPS를 통하면 암호화 되었기에 내용을 바로 볼 순없다.(복호화하면 볼수있다)

### 1-1. 암호화 방식

- 대칭키 암호화 방식: 암호화와 복호화의 키가 동일하다
- 공개키(비대칭 키) 암호화 방식: 키가 다르다.

#### 1-1-1. 대칭 키 암호화 방식

하나의 키만 사용한다. 암호화한 키로 복호화가 가능하다.

연산속도가 빠르다. 키를 주고 받는 과정에서 하이재킹 시 암호화가 무의하여 키관리에 신경써야한다.

#### 1-1-2. 공개 키(비대칭 키)암호화 방식

두 개의 키를 사용한다. 암호화 할때 사용한 키와 다른 키로만 복호화 된다.

공개키, 비밀키라고 칭하고, 공개키는 공개되어 있기에 누구든지 접근 가능하나, 비밀키를 가진 사람만 복호화할 수 있다. 서버가 해킹당하는게 아니면 탈취되지 않는다.

보안성이 좋다. 더많은 시간을 소모한다.

### 1-2. SSL/TLS Protocol

HTTPS는 HTTP통신을 하는 소켓 부분에서 SSl or TLS라는 Protocol을 사용하여 서버 인증과 데이터 암호화를 진행한다. 여기서 SSL이 표준화되며 바뀐 이름이 TLS이다.

- CA를 통한 인증서 사용
- 대칭키, 공개키 암호화 모두 사용

#### 1-2-1. 인증서와 CA(Certificate Authority)

HTTPS를 사용하면 브라우저가 서버의 응답과 한께 전달된 인증서를 확인할 수 있다. 이러한 인증서는 서버의 신원을 보증한다. 이때 인증서를 발급해주는 공인된 기관들을 Certificate Authority, CA라 한다.

서버는 인증서를 발급받기 위해서 CA로 서버의 정보와 공개 키를 전달한다. CA는 서버의 공개 키와 정보를 CA의 비밀키로 암호화하여 인증서를 발급한다.

서버는 클라이언트에게 요청을 받고, CA에게 발급받은 인증서를 보낸다. 사용자가 사용하는 브라우저는 CA들의 리스트와 공개키를 내장하고 있는데, 우선 해당 인증서가 리스트에 있는 CA가 발급한 인증서인지 확인 후 리스트에 있는 CA라면 해당하는 CA의 공개키를 사용해 인증서의 복호화를 시도한다.

CA의 비밀키로 암호화된 데이터는 CA의 공개키로만 복호화가 가능하여, CA에서 발급한 인증서가 맞다면 복호화가 성공적으로 진행된다.

- 복호화가 성공적으로 진행되면, 클라이언트는 서버의 정보와 공개 키를 얻게 됨과 동시에 해당 서버가 신뢰할 수 있는 서버임을 알 수 있게된다.
- 복호화가 실패한다면, 이는 서버가 보내준 인증서가 신뢰할 수 없는 인증서임을 확인하게 된다.

#### 1-2-2. 대칭 키 전달

공개키는 보안은 확실하지만, 연산이 복잡하여 시간을 많이 소모한다. 이것을 요청과 응답에 사용하지는 못한다.

클라이언트와 서버가 대칭키를 주고 받을 때 사용하는데, 대칭키는 속도는 빠르지만 탈취될 수 있는 위험이 있다. 하지만 클라이언트가 서버로 대칭키를 보낼 때 서버의 공개키를 사용해 암호화하면 서버의 비밀키가 없으면 복호화 할 수 없으므로 위험성이 줄어든다.

클라이언트는 생성된 대칭키를 서버의 공개 키로 암호화하여 전달한다. 서버는 전달받은 데이터를 비밀 키로 복호화하여 대칭키로 확보한다.

HTTPS 요청을 주고 받을 때 이 대칭키를 사용하여 데이터를 암호화하여 전달한다. 대칭키 자체는 오고 가지 않기 때문에 키가 유출된 위험이 없어졌다. 요청이 중간에 탈취되어도 암호화된 데이터를 복호화 할 수 없다. HTTPS는 이러한 암호화 과정을 통하여 요청과 응답을 주고 받는다.

## 2. https 실행

### 2-1. mkcert 설치

1. ubuntu

```bash
$sudo apt install libnss3-tools
$wget -O mkcert https://github.com/FiloSottile/mkcert/releases/download/v1.4.3/mkcert-v1.4.3-linux-amd64
$chmod +x mkcert
$sudo cp mkcert /usr/local/bin/
```

2. macOS

```bash
# Homebrew
$brew install mkcert

# firefox를 사용할 경우 필요에 따라 설치해주세요.
$brew install nss
```

### 2-2. 인증서 생성

```bash
# 로컬을 인증된 발급기관으로 추가
$mkcert -install

# localhost 로컬환경에 대한 인증서 생성
$mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

결과물 -> cert.pem, key.pem

### 2-3. HTTPS 서버 작성

1. https 모듈 사용

```bash
$npm init
$npm install https
$npm install

$touch https.js
$vim https.js
```

```javascript
const https = require('https');
const fs = require('fs');

https
  .createServer(
    {
      key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
      cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
    },
    function (req, res) {
      res.write('Congrats! You made https server now :)');
      res.end();
    }
  )
  .listen(3001);
```

```bash
$node https.js
```

2. express 사용

```bash
$npm init
$npm install express
$npm install

$touch express.js
$vim express.js
```

```javascript
const https = require('https');
const fs = require('fs');
const express = require('express');

const app = express();

https
  .createServer(
    {
      key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
      cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
    },
    app.use('/', (req, res) => {
      res.send('Congrats! You made https server now :)');
    })
  )
  .listen(3001);
```

```bash
$node express.js
```

https://localhost:3001 접속 후 확인

3. [ngrok](https://ngrok.com/) HTTPS 터널링

https로 접속하도록 터널링해주는 프로그램으로 보인다.
외부에서 http(80)를 통해 접속할 수 있었던 경험으로 포트포워딩과 https mkcert 443포트 사용 시 외부에서 접속하는건 ddns설정과 포트포워딩을 통해 충분히 외부에서 접속할 수 있으므로, 실지로 ngrok이라는 툴을 이용해야하는지는 의문이나, 만약 설정부분이 간소하고 한큐에 해결된다면 ngrok도 쓸만할거같으니 keep

---

서버와 클라이언트간의 CA를 통해 서버를 인증하는 과정과 데이터를 암호화하는 과정을 아우른 프로토콜을 SSL또는 TSL, HTTP에 SSL/TSL Protocol을 더한것이 HTTPS이다.

---

## 참조

> [CA키 유출로 파산](https://slate.com/technology/2016/12/how-the-2011-hack-of-diginotar-changed-the-internets-infrastructure.html)   
> [ngrok: main](https://ngrok.com/)   
> [Software Architect: lesstif blog/ngrok](https://www.lesstif.com/software-architect/ngrok-39126236.html)   
> [Alissa Yoon: velog blog/ngrok](https://velog.io/@dwa_all/ngrok-%EB%A1%9C%EC%BB%AC-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EC%99%B8%EB%B6%80%EC%97%90-%EA%B3%B5%EC%9C%A0%ED%95%98%EA%B8%B0)