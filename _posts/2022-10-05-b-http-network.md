---
layout: post
title: "HTTP & NETWORK 2"
date: 2022-10-05
categories:
- Network
tags:
- HTTP
- Network
- HTTP Messages
- Requests
- Responses
- start line
- HTTP headers
- General header
- Request header
- Representation header
- empty line
- body
- Single-Resource bodies
- Multiple-Resource bodies
- Responses head
- payload
- Stateless
- 
---

양이 방대하지만 평소같았으면 찾아보진않고 넘어갈 좋은 내용들이 많다 가자!!

---

## HTTP

HyperText Transfer Protocol, HTML과 같은 문서를 전송하기위한 규약. Client-Server Architecture에서 Client가 HTTP Messages를 요청하면, Server에서 HTTP Messages를 응답한다.

## HTTP Messages

Client와 Server사이의 데이터가 교환되는 방식이다.

- Requests(요청)
- Responses(응답)

## Structure

1. start line: 요청이나 응답의 상태를 나타내며, 항상 첫번째 줄에 위치한다. 응답측에선 status line이라고 한다.
2. HTTP headers: 요청을 지정하거나, 메세지에 포함된 본문을 설명하는 헤더의 집합이다.
3. empty line: 헤더와 본문을 구분하는 빈줄이 있다.
4. body: 요청에 관련된 데이터나 응답과 관련된 데이터 또는 문서를 포함한다. 요청과 응답의 유형에 따라 선택적으로 사용한다.

- Responses head: start line, HTTP header
- payload: body

## [시각화](https://hahahoho5915.tistory.com/62)

출처: [99C0RN](https://hahahoho5915.tistory.com/62)

### Requests

![Requests](/assets/img/221005-request-structure.png)

### Responses

![Responses](/assets/img/221005-response-structure.png)

## Stateless

상태를 가지지 않는다. HTTP는 Client와 Server간의 통신(Communication) 중 어떤 것도 저장하지 않는다. HTTP는 단순한 Protocol, 통신규약일 뿐이다. 필요에 따른 다른 방법(Cookie-Session, API 등)을 통해 상태를 확인할 수 있다.

Stateless(무상태성)는 HTTP의 큰 특징이다.

## HTTP Requests

### Start line

HTTP header에 포함되는 start line에는 세가지 정보가 있다.

1. 수행할 작업(GET, PUT, POST 등)이나 방식(HEAD or OPTIONS)을 설명하는 HTTP method를 포함한다.
2. 요청 대상(URL, URI) 또는 Protocol, Port, Domain의 절대 경로는 Requests Context에 작성된다. HTTP method마다 Requests 형식은 다르다.
   - type example
     - origin: '?'와 쿼리 문자열이 붙는 절대 경로이다. GET, POST, HEAD, OPTIONS 등의 method와 함께 사용한다.
     - POST / HTTP 1.1
     - GET /background.png HTTP/1.0
     - HEAD /test.html?query=alibaba HTTP/1.1
     - OPTIONS /anypage.html HTTP/1.0
   - absolute: 완전한 URL type으로 proxy에 연결하는 경우 대부분 GET method와 함께 사용한다.
     - GET http://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1
   - authority: Domain name & Port number로 이루어진 URL의 일부분이다. HTTP 터널을 구축하는 경우 CONNECT와 함께 사용할 수 있다.
     - CONNECT developer.mozilla.org:80 HTTP/1.1
   - asterisk: OPTIONS와 함께 *로 서버 전체를 표현한다.
     - OPTIONS * HTTP/1.1
3. HTTP 버전에 따라 HTTP message의 structure가 달라진다.

### Headers

Requests의 Headers는 기본 Structure를 따른다. Header name(대소문자 구분이 없는 문자열), (:)값을 입력한다. 값은 헤더에 따라 다르다. 여러 종류의 Header가 있고, Grouping이 가능하다.

- General headers: 메세지 전체에 적용되는 헤더, body를 통해 전송되는 데이터와는 관련이 없는 헤더이다.
- Request headers: fetch를 통해 가져올 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더를 의미한다. User-Agent, Accept-Type, Accept-Language와 같은 헤더는 요청을 보다 구체화한다. Referer처럼 Context를 제공하거나 If-None과 같이 조건에 따라 제약을 추가할 수 있다.
- Representation headers: 이전에는 Entity headers로 불렀고, body에 담긴 리소스의 정보(콘텐츠 길이, MIME 타입 등)을 포함하는 헤더이다.

```
POST / HTTP/1.1
<!-- Request headers 시작 -->
HOST: localhost:3000
User-Agent: Mozilla/5.0 (Windows;...)... Chrome/xx.x
Accept: text/html, application/xhtml+xml,...,*/*;q=x.x
Accept-Language: ko-KR, kr;q=x.x
Accept_Encoding: gzip, deflate
<!-- Request headers 끝 -->
<!-- General headers 시작 -->
Connection: keep-alive
Upgrade-Insecure-Requests: 1
<!-- General headers 끝 -->
<!-- Entity headers 시작 -->
Content-Type: multipart/form-data; boundary=-xxxxxxx
Content-Length: 333
<!-- Entity headers 끝 -->

-xxxxxxxxxxx
(more data)
```

### body

Requests의 Content는 HTTP messages Structure의 마지막에 위치한다. 필수는 아니며, GET, HEAD, DELETE, OPTIONS처럼 서버에 리소스를 요청하는 경우에는 본문이 필요하지 않다. POST나 PUT과 같은 일부 요청은 데이터를 업데이트하기 위해 사용한다.

- Single-resource bodies(단일-리소스 본문): 헤더 두개(Content-Type & Content-Length)로 정의된 단일 파일로 구성된다.
- Multiple-resource bodies(다중-리소스 본문): 여러 파트로 구성된 본문에서는 각 파트마다 다른 정보를 지닌다. -> HTML form과 관련이 있다.

## HTTP Responses

### Status line

HTTP Responses는 Server가 Client에게 보내는 Message이다. Responses의 첫 줄을 Status line이라고한다.

1. Current Protocol Version(HTTP/1.1)
2. Status Code: Requests's result(200, 303, 400...)
3. Status Text: Status Code Description

### Headers

Responses에 들어가는 HTTP headers의 Requests header와 동일한 Structure를 가지고 있다.

- General headers: 메세지 전체에 적용되는 헤더로, body를 통해 전송되는 데이터와 관련이 없는 헤더이다.
- Response headers: 위치 또는 서버 자체에 대한 정보와 같이 응답에 대한 부가적인 정보를 갖는 헤더이다. Vary, Accept-Ranges와 같이 상태 줄에 넣기에 공간이 부족한 추가 정보를 제공한다.
- Representation headers: 이전에는 Entity headers, body에 담긴 리소스의 정보를 포함하는 헤더이다.

```json
R#: Response headers
E#: Entity headers
G#: General headers

HTTP/1.1 200OK
Access-Control-Allow-Origin:  *          R#
Connection: Keep-Alive                   G#
Content-Encoding: gzip                   E#
Content-Type: text/html; charset=utf-8   E#
Date: XXXXXXXXXXXXXXXXXXXXXXXX           G#
Etag: "XXXXXXXXXXXXXXXXXXXXXXX"          R#
Keep-Alive: timeout=5, max=999           G#
Last-Modified: XXXXXXXXXXXXXXXXX         E#
Server: Apache                           R#
Set-Cookie: xxxxxxxxxx                   R#
Transfer-Encoding: chunked               G#
Vary: Cookie, Accept-Encoding            R#
X-Frame-Options: DENY                    R#

(body)
```

### body

Responses의 Content는 HTTP Messages Structure의 마지막에 위치한다. 모든 Responses에 body는 필수가 아니다. 201, 204와 같은 Status Code가 있는 Response에는 Content가 필요하지 않다.

- Single-resource bodies(단일-리소스 본문)
  - 길이가 알려진 단일-리소스 본문은 두 개의 헤더(Content-Type, Content-Length)로 정의한다.
  - 길이를 모르는 단일 파일로 구성된 단일-리소스 본문은 Transfer-Encoding이 chunked로 설정되어 있으며, 파일은 chunk로 나뉘어 Encoding되어 있다.
- Multiple-resource bodies(다중-리소스 본문): 서로 다른 정보를 담고 있는 body이다.

> ## 참조
> [Wikipedia:payload](https://ko.wikipedia.org/wiki/%ED%8E%98%EC%9D%B4%EB%A1%9C%EB%93%9C_(%EC%BB%B4%ED%93%A8%ED%8C%85))   
> [99C0RN:HTTP Request/Response Structure](https://hahahoho5915.tistory.com/62)   
> [MDN:HTML forms](https://developer.mozilla.org/en-US/docs/Learn/Forms)   
> [MDN:Representation header](https://developer.mozilla.org/en-US/docs/Glossary/Representation_header)   
> [MDN:HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)