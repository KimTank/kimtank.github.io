---
layout: post
title: "HTTP & NETWORK 1"
date: 2022-10-05
categories:
  - Network
tags:
  - HTTP
  - Network
  - 2-Tier Architecture
  - 3-Tier Architecture
  - 프론트엔드
  - 백엔드
  - Database
  - Client
  - Server
  - API
  - Application Programming Interface
  - Interface
  - Request
  - Response
  - CRUD
  - GET
  - POST
  - PUT
  - PATCH
  - DELETE
  - URL
  - Uniform Resource Locator
  - URI
  - Uniform Resource Identifier
  - scheme
  - hosts
  - uri-path
  - query
  - frament
  - IP
  - Internet Protocol address
  - IPv4
  - IPv6
  - Port
  - Domain
  - DNS
  - Domain Name System
  - DDNS
  - Dynimic Domain Name System
  - Chrome
  - Chrome Brower Error Message
---

가을이되니 체력이 급격하게 떨어지는 것인지, 엉덩이를 고정하니 불안감에 집중을 못하는것인지 어제 처음으로 지각을했다(무려 30분씩이나). 생활패턴이 깨지려한다. 정신차려야한다. 매번 알고싶었지만 접근하기 힘들었던 네트워크~!

---

## 1. Network

### 1.2. Client Server Architecture

리소스가 존재하는 곳, 리소스를 사용하는 앱을 분리한 것을 말한다.

- Client: 리소스를 사용하는 앱
- Server: 리소스를 제공하는 곳
- Request: 클라이언트가 서버에 요청
- Response: 서버가 클라이언트에서 요청한 신호에 응답

### 1.3. 2-Tier Architecture

|:---:|:---:|:---:|:---:|:---:|
|리소스를 사용하는 앱|||인터넷|리소스가 존재하는 곳|
|...기능들|||<-|...리소스들|
|클라이언트|||-|서버|
|요구사항|->|요청|->|반응|
|↑|-|-|-|↓|
|반영|<-|요청값|<-|응답|

### 1.4. 3-Tier Architecture

보통 서버의 경우는 Database에 리소스를 저장하고, 서버는 Database에 접근해 해당 요청에 대한 요청값을 응답한다.

이렇게 Database가 추가되면, 3-Tier Architecture라고한다.

### 1.5. 프론트엔드와 백엔드

- `프론트앤드`는 "클라이언트"측, 즉 리소스를 사용하는 앱을 말한다. 주로 유저에게 보이는면, UI나 터치 시 이벤트 등을 개발하는 인력을 프론트엔드 개발자라 한다.
- `백엔드`는 리소스를 전달해주는 측, 즉 "서버"를 말하고, 리소스를 저장하는 공간인 "데이터베이스"까지 포함한 영역을 말한다. 눈에 보이지 않는 부분, API나 권한관리, 세션, Database등의 시스템 설계를 개발하는 인력을 백엔드 개발자라 한다.

## 2. Client Server Communication & API

- Protocol: 통신 규약으로 약속이다.
- HTTP: 웹 애플리케이션 아키텍처에서의 프로토콜이다.
- HTTP Message: 클라이언트와 서버가 나누는 통신(대화)내용

### 2.1. Protocol

#### 2.1.1. OSI 7 Layers

- 7: 응용 계층

|:---:|:---:|
|프로토콜 이름|설명|
|HTTP|Web에서 HTML, JSON등의 정보를 주고받는 규약|
|HTTPS|HTTP에서 보안이 강화된 규악|
|FTP|파일 전송 규약|
|SMTP|메일 전송 규약|
|SSH|CLI환경의 원격 컴퓨터에 접속하는 규약|
|RDP|Windows계열의 원격 컴퓨터에 접속하기 위한 규악|
|WebSocket|실시간 통신, Push 등을 지원하는 규약|

- 6: 표현 계층
- 5: 세션 계층
- 4: 전송 계층

|---|---|
|TCP|양방향) HTTP, FTP 통신 등의 근간이되는 인터넷 규약|
|UDP|단방향) 단방향으로 작동하는 단순하고 빠르고 신뢰성이 높은 인터넷 규약|

- 3: 네트워크 계층
- 2: 데이터 링크
- 1: 물리

## 3. API

Application Programming Interface로 Server와 Client가 Communication을 할 수 있게 해주는 Interface(접점)이다.

### 3.1. Example

예시: `https://bikemoa.net`

|---|---|
|자전거 목록 불러와|/bike/list|
|자전거 상세정보 불러와|/bike/detail|
|merida 브랜드 자전거 목룍 보여줘|/bike/list?brand="merida"
|specialized브랜드 자전거 상세정보 보여줘|/bike/detail?brand="specialized"&name="allez"&y_of_manufacture="2023"|

요청(Request)시에는 HTTP 프로토콜을 사용하고, URL, URI와같은 주소를 통해 접근할 수 있다.

```
http://bikemoa.net/bike/detail?brand="specialized"&name="allez"&y_of_manufacture="2023"
프로토콜://URL or URI/path?param_01="value"&param_02="value"...
```

### 3.2. Best Example

사용자 관리 API

|---|---|---|
|Request|URL Design|using method|CRUD|
|전체 사용자 조회|/users|GET|READ|
|사용자 추가|/users|POST|CREATE|
|a 사용자 갱신(수정)|/users/a|PUT or PATCH|UPDATE|
|a 사용자 삭제|/users/a|DELETE|DELETE|
|a 사용자 조회|/users/a|GET|READ|

## 4. URL & URI

`:scheme:` `:hosts:` `:url_path:` `:query:`
`file://` `127.0.0.1` `/Users/username/Desktop/` `쿼리없음`
`http://` `www.google.com:80` `/search` `?q=JavaScript`

### 4.1. URL

Uniform Resource Locator, 네트워크상 웹페이지, 이미지, 동영상 등의 파일이 위치한 정보 나타낸다.

- scheme: 통신방식(프로토콜)을 결정한다. ex) http, https
- hosts: 웹 서버의 이름이나 도메인, IP를 사용하며 주소를 나타낸다.
- url-path: 웹서버에서 지정한 루트 디렉토리로부터 시작하여 웹페이지, 이미지, 동영상 등이 위치한 경로와 파일명을 나타낸다.

### 4.2. URI

Uniform Resource Identifier, URL의 기본 요소인 scheme, hosts, url-path에 query, fragmet를 포함한다.

- query: 웹서버에 보내는 추가적인 질문 ex) `http://www.google.com:80/search?q=JavaScript`
- fragment: 일종의 북마크 기능을 수행한다. url에 fragment(`#`)와 특정 HTML요소의 id를 전달하면 해당 요소가 있는 곳으로 스크롤을 이동할 수 있다. ex) 각종 문서의 마크다운형식에서 `#`을 의미하는걸로 보인다.

### 4.3. 도식화

|---|---|---|
|file://, http://, https://|scheme|통신 프로토콜|
|192.168.0.1, www.naver.com|hosts|웹페이지, 이미지, 동영상 등의 파일이 위치한 웹서버, 도메인 또는 IP|
|:80, :443, :3000|port|웹서버에 접속하기 위한 통로|
|/search|url-path|웹 서버의 루트 디렉토리로부터 웹페이지, 이미지, 동영상 등의 파일위치까지의 경로|
|q=JavaScript|query|웹서버에 전달하는 추가 질문|

> 로컬PC IP: 127.0.0.1
> 공유기 IP: 168.192.0.1

## 5. IP & Port

### 5.1. IP address

Internet Protocol address, IP 주소는 네트워크상에 특정 PC를 나타내는 IP 주소와 그 주소에 진입할 수 있는 통로 Port이다.

인터넷에 연결된 모든 PC는 IP 주소체계에 따라 네덩어리의 구분된 숫자 IP주소체계, IPv4를 따른다. IPv4 -> Internet Protocol version 4

```bash
#nslookup google.com
```

IPv4: 각덩어리는 0~255까지 2^(32) 43억개의 IP주소를 표현할 수 있다. 그중 몇가지는 이미 용도가 정해져있다.

- localhost, 127.0.0.1: 현재 로컬 PC지칭
- 0.0.0.0, 255.255.255.255: broadcast address, 로컬 네트워크에 접속된 모든 장치와 소통하는 주소이다. 서버에서 접근 가능 IP주소를 broadcast address로 지정 시 모든 기기에서 서버에 접근할 수 있다.

IPv4의 이용범위를 넘어서자 IPv6(IP version 6)가 나온다. IPv6는 2^(128)

|---|---|
|IPv6|IPv4|
|128 bit each|4 bytes each|
|340 undecillion|4.3 billion|

### 5.2. PORT

포트는 항구에서 배가 정박할 수 있는 port와 같은 개념으로 로컬PC의 IP주소 뒤 :3000과같이 붙는다. Window와 Android의 경우 원격 접속 포트포워드 설정 시 :3389, mac의 경우 :5900을 기본으로한다.

일반적으로 react 서버실행구문인 npm start를 통한 서버 실행 시 :3000으로 포트가 열리고, 추가로 열 시 :3001처럼 다른 포트로 실행된다.

포트번호는 0~65535까지 사용할 수 있고, 0~1024까지의 포트번호는 주요통신 규약에 따라 정해져 있다.

- 22: SSH
- 80: HTTP
- 443: HTTPS
- 참조확인

잘알려진 포트의 경우는 포트번호를 생략해도 되지만(:3389, :5900 등), 잘알려지지 않은 경우 명시해야한다.

## 6. Domain & DNS

IP주소를 대신하여 사용하는 주소가 있다. 그것을 Domain이라고한다.

네트워크에 접속되어있는 모든 PC는 IP주소가 있고, 모든 PC가 Domain을 가진것은 아니다. Domain은 일정기간 대여하여 사용한다. 대여하여 사용한 Domain과 내 PC의 IP address를 매핑하는 작업을 DNS(Domain Name System)이라고 한다.

일반 개인PC의 경우 별도의 고유한 mac값을 가지고 있으며, 각 인터넷 공급업체(KT, SKT, 등등)가 대여해주는 동적IP를 가진다.

DNS는 호스틩 도메인 이름을 IP address로 변환하거나, 반대의 경우 수행할 수 있도록 개발된 Database System이다.

공유기의 DDNS설정을 이용하여 제조업체가 공급해주는 도메인을 이용할수도 있다.(동적 IP를 고정 IP처럼 사용할 수 있도록 공유기 제조업체에서 제공) -> Dynamic Domain Name System

## 7. Chrome Brower Error Code

### 7.1. Aw, Sanp

앗, 이런! 이라고뜬다는데 본적이 ㅇ..ㅄ..

|---|---|
|Error|Description|
|Aw, Sanp|페이지 로드 중 문제 발생|
|ERR_NAME_NOT_RESOLVED|호스트이름(웹주소)이 존재하지 않음|
|ERR_INTERNET_DISCONNECTED|사용 중인 기기가 인터넷에 연결되지 않음|
|ERR_CONNECTION_TIMED_OUT|페이지 접속 타임아웃, 인터넷이 느리거나, 접속자가 많아 시간초과|
|ERR_TIMED_OUT|상기 동|
|ERR_CONNECTION_RESET|웹페이지 연결 방해하는 요소 발생|
|ERR_NETWORK_CHANGED|웹페이지 로드 중 기기의 네트워크 연결이 해제되었거나, 새로운 네트워크에 연결|
|ERR_CONNECTION_REFUSED|웹페이지에서 Chrome 연결을 허용하지 않음.|
|ERR_CACHE_MISS|이전 입력정보 다시 제출하도록 요청받음|
|ERR_EMPTY_RESPONSE|웹페이지에서 데이터를 전혀 전송하지 않았으며, 데이터를 전송할 서버가 다운|
|ERR_SSL_PROTOCOL_ERROR|페이지에서 전송된 데이터를 Chrome 해석못함|
|ERR_BAD_SSL_CLIENT_AUTH_CERT|클라이언트 인증서에 오류발생하여 로그인안됨|

다른 에러들은 본적이 있는거 같다. 특히 Ubuntu깔면서 WIFI모듈 충돌로인한 ERR_INTERNET_DISCONNECTED, 크롬이 자체적으로 던져주는건지는 처음알았다. 껄껄

## 참조

> [KoreanJSON](https://koreanjson.com)  
> [MDN:HTTP 요청 메서드](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)  
> [Wikipedia:IPv6](https://en.wikipedia.org/wiki/IPv6)  
> [Widipedia:Port Number](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)  
> [Asus:Support/DDNS](https://www.asus.com/kr/support/FAQ/1011725/)  
> [Chrome Brower:Network Errors](chrome://network-errors/)
