---
layout: post
title: "Web oauth2.0"
date: 2022-11-14
categories:
- Web
tags:
- Javascript
- Web
- OAuth
- Resource Owner
- Client
- Local Server
- Resource Server
- Authorization Server
- Authorization Grant
- Authorization Code
- Access Token
- Refresh Token
---

처음으로 늦잠을 잔날로 기억한다. 오늘은 221116, 덕분에 효병님에게 본의아닌 폐를 끼치게되었다.

---

## 1. OAuth

구현하고 싶었으나 각 API사용법과 B2B이면서 데이터 장사를 하고싶었던 그분들은 유료에다 데이터를 뺏기는 행위자체를 용납할 수 없었기에(틀린말은 아니다 대한민국을 카카오가 잠식하고있다) 구현시도도 힘들었던 그게 이거였다.

레거시에서는 각 회사별 사이트별 서버가 인증처리를 직접해주었으나, OAuth는 인증을 중개한다. 보안에 액세스하귀 위한 권한을 Ct에게 제공하는 과정을 단순화한 프로토콜이다.

과거 제로보드나 소규모 커뮤니티(개인)에 일일이 개인정보를 입력하고 가입하고 탈퇴하는것을 까먹어 나의 소중한 핸드폰번호가 그나라에 들어간 덕에 번호를 바꾸기 전까지 한창 날라오던 이상한 문자들은 다 이유가 있는것이다.

OAuth를 사용하면 나조차도 편하다. 물론 구현방식이야 정해놓은 방법에 따르고, 각서비스 이용에 비용이 들어가지만, 그건 내가 고려할부분은 아니고, 나는 사용할수는 있어야하니 해보자

## 2. 용어

- Resource Owner: 유저, 정보제공자
- Client: RO를 대신해 보호된 리소스에 액세스하는 애플리케이션
- Local Server: Ct의 요청을 수락, 응답할 수 있는 Sv
- Resource Server: RO의 정보를 저장하고 있는 Sv
- Authorization Server: 인증을 담당하고 있는 Sv, AccessToken을 발급하는 인증 Sv
- Authorization Grant: Ct가 AT를 얻는 방법(Authorization Code Grant Type, Refresh Token Grant Type)
- Authorization Code: AT를 발급받기 위한 Code
- Acess Token: 보호된 리소스 액세스하는데 쓰는 AT, RS에 접근할 수 있다.
- Refresh Token: AT가 만료될 시 RT를 통해 새 AT발급 한다.

## 3. 흐름

- Ct: Client
- Sv: Server
- AC: Authorization Code
- LS: Local Server
- AT: Access Token
- AS: Auth Server
- Ur: User
- RS -> Resource Server

### 4. ACGT

Authorization Code Grant Type: AC받아 AT받는 방식, 사용자나 브라우저에 표시되지 않는것 의미한다. AT가 누출될 위험이 준다.

User -> Ct -> login action -> AuthSv -> AC 전달 -> Ct -> LS -> AT 요청 -> AS -> AT 전달 -> LS -> Ur정보 요청 -> RS -> Ur정보 전달 -> LS -> Ur정보 전달 -> Ct

### 5. RTGT

Refresh Token Grant Type: AT발급 받은 후 AT 만료 시 RT 활용 새 AT교환으로 사용한다.

LS -> RT로 AT요청 -> AS -> 새 AT 전달

---

각 사이트별 구현은 다르고, 유료로 기억하고 있다. 개발자들에게 무료로 제공하는 횟수가 존재하는 곳도 있으니, 해보면 재밋을지도 모른다.(예전에 안되서 머리아팟어요)

---

## 참조

> [oauth: oauth2(php base)](https://www.oauth.com/oauth2-servers/getting-ready/)   
> [kakao api: kakao login](https://developers.kakao.com/product/kakaoLogin)   
> [naver api: login](https://developers.naver.com/products/login/api/api.md)   
> [google cloud: authentication](https://cloud.google.com/docs/authentication?_ga=2.174955938.-121637756.1665038631)   
> [facebook doc: login](https://developers.facebook.com/docs/facebook-login/)   
> [twitter doc: authentication](https://developer.twitter.com/en/docs/authentication/overview)