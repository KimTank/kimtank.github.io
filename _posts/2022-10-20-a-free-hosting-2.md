---
layout: post
title: "포트폴리오용 웹서버, HTTP서버 만들기 vol.2"
date: 2022-10-20
categories:
- Personal
tags:
- 포트폴리오
- HTTP서버
- Server
- CPU명령어
- Architecture
- Github pages
- Dex
- Termux
- NodeJS
- Ubuntu
- PortFowarding
- ip
- DDNS
- Dynamic Domain Name System
- Duckdns.org
- HTTP
- HTTPS
- :80
- :443
- stack over flow
- porting
- VPN
- Rooting
- sudo
- firmware
- Knox
- Bootloader unlock
- Ubuntu Touch
- UBport
- UBport instroller
- TPRM
- Odin3
- Debian noroot
- Anlinux
---

사실 이 글을 적는 시점은 아직 시도해보지 않은게 2개가 있는 시점이다.

동기분이 cpu명령어가 달라서 오류가 났을거라고 했다.

하지만 오기가생겨서 Web은 Github pages, Server는 데탑으로, 1번.

동작하면, 사양문제일거라는 상상력으로 실패하더라도 다른 플래그쉽 폰으로 Dex북쓰듯이 쓸 수 있도록 2번

만약 두가지 다 실패면 Github pages가 문제일수도 있으니 기대된다.

---

## 3. 진행과정

### `Termux`

1. `Termux`로 `Android`에서 `nodejs`돌리기[Kasterra's Archive: 안드로이드에서 nodeJS...](https://kasterra.github.io/setting-nodejs-in-android/)
2. `ubuntu`와 저장소가 달라 안될거같았지만, `nodejs`가 정상적으로 설치가 되었고, 간단한 서버를 돌릴 수 있었다.[RoyalTurtle: 루팅없이 안드로이드폰을 node.js...](https://royalturtles.tistory.com/5)
3. [`포트포워딩`](https://ko.wikipedia.org/wiki/%ED%8F%AC%ED%8A%B8_%ED%8F%AC%EC%9B%8C%EB%94%A9)을 하는것도 2번의 RoyalTurtle님의 글에 잘나와 있으니, `공유기 주소(iptime기준 192.168.0.1)`로 접속하여 `내부ip(핸드폰ip)`, `외부포트(80: http, 443: https)`, `내부포트(서버을 연포트 ex: 3000, 4000, 5000...)`를 통하여 외부에서 `ip`를 통하여 접속할 수 있게 `포트포워딩`을 구성했다.
4. [DDNS(Dynamic Domain Name System)](https://namu.wiki/w/DNS#s-2.3)을 통해서 우리는 `동적IP`를 고정된 `host주소`로 변경할 수 있다. `공유기` 제조사에서 제공도 하고, 무료로 제공하는 사이트도 여럿있다. 마음에 드는 사이트를 찾아 `http://hostname:80` 으로 접속할 수 있게 구성했다.[duckdns.org](https://www.duckdns.org/domains)
5. `클라이언트`와 `서버`부분을 변경한다.
   1. `클라이언트`: `react`이므로 `Github pages`는 정적인 파일만 `컴파일`이 가능하다(`JSX`가뭐야???), `build`하여 다른 저장소에 저장하고 `Github pages`를 `deploy`한다.[에브리원: 깃허브로 나만의 웹사이트 만들기](https://brunch.co.kr/@everiwon/42), [Hohyeon Moon: ReactJS를 Github Pages에 호스팅하기](https://www.hohyeonmoon.com/blog/react-js-github-pages-deploy/)
   2. `서버`: `build`하는 법을 몰라 서버에 `React`프로젝트를 하드카피하여 `npm install`을 하다 `CRASH..` -> android의 파일주소 접근 권한문제[stack over flow: q](https://stackoverflow.com/questions/61943494/how-can-i-install-npm-on-termux), [stack over flow: q2](https://stackoverflow.com/questions/73307285/termux-npm-err-error-eperm-operation-not-permitted-symlink)를 우회하는법. 관련 내용을 `vpn을 사용하여 우회`하는법도 있었는데 다시 찾으려니 못찾겠다(사용하고 싶지 않았다.)
6. `루팅`을하자. 해당폴더로 기본폴더를 변경하여 `sudo 권한`을 얻기위해 `루팅`이 필요하다. `루팅`은 과거에도 몇번해봤었기에 시도하다 실수(`펌웨어`를 올릴 시 `Knox`에서 일주일간 `부트로더 해제`를 잠궈버린다.)한 덕에 다른 방법을 찾게된다.

### Ubuntu Touch & UBport

`Ubuntu`를 스마트폰에 올릴 수 있는 방법을 찾다가, [`포팅`](https://namu.wiki/w/%ED%8F%AC%ED%8C%85)이란 개념을 알게 되었고, `OS`를 `Windows10`을 올릴 수 있으나 [`Driver`](https://namu.wiki/w/%EB%94%94%EB%B0%94%EC%9D%B4%EC%8A%A4%20%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84)문제로 인터넷을 못하게 될 경우 서버폰으로서의 의미가 없고, `포팅` 역시 잠깐 시간을 들여서 시도하기에는 전문지식이 필요다. 그래서 찾게된 것이 `Ubuntu Touch 프로젝트`. 하지만 이것역시 개발 중단이 되었고, `Ubuntu Touch`를 이어서 `UBport 커뮤니티`가 개발을 하다 2017년에 중단되었다고 한다. 그래도 `UBport instroller`를 이용 시 지원되는 기기들의 경우에는 원터치(지원되는 기기가 아니면 설치자체가 안되서 못해봄)로 설치가 가능하다.

하지만 해당기기는 내가 가진기기가 이니었고, 지원기기가 아니면 아애 설치를 못하는것으로 보아, 각 `cpu`를 지원해주는 개발이 선행되어야 하는거 같아 다른 방법으로 시도해 보았다.

### Andronix

`Tor noroot`라는 `멜웨어`(`구글 프로텍트`, `윈도우 디펜더` 기준)로 뜨는 프로그램을 찾아 위험을 무릎쓰고 실행해 보았으나, 지원기기가 아니면 `루팅`이 불가한 이슈가 있다는걸 확인하였다.(안된다 내건 ㅜㅜ)

하여 더 찾아본 결과 `Tor`이외에도 관련하여 `슈퍼루팅`이 꼭 과거 `TPRM`, `odin`을 통한 `루팅` 시 권한을 줄 수 있게 바꾸는 방식이 아니라, 단순하게 클릭한번으로 루팅을 할 수 있는 앱들이 개발이된걸 알게되었고(`갤럭시s2`를 루팅하면서 `커널질`을 했었다.), 그것들 역시 완벽하진 못하고, `반루팅`개념이라 풀린다는 것을 보고 안정성(이미 `무선통신`이라 불안정하지만)이 중요한 `서버`가 사용하기에는 적합하지 않다고 생각하고 다른 프로그램을 찾아보던 중, 꽤나 평이 좋았고 리뷰어의 말에는 `windows10`도 쉽게 올렸다는 것을 보고 `Andronix`에 `과금`을 하게된다. `Ubuntu`도 있고, `moded`(최적화)된 버전도 한번 구매하면 `Andronix`를 배포한 회사가 없어지기 전까지 무한으로 사용할 수 있는 어플을 설치하고 설치를 진행하던 중, 중간에 에러를 3번 내더니 하루 이용한도 초과라고하며 관리자에게 문의하거나, 내일(당시 새벽 1시) 다시 시도라하라는것을 보고 문서를 읽어가면서 다시 환경설정을 해야되고, 과금을 했음에도 불구하고 내시간을 배로 투자하는건 말이 안된다고 생각하여 또 다른 방법을 찾게된다.

### Debian noroot

`stack over flow`를 뒤지던 중 알게된 `debian noroot`의 경우는 쉽게 설치가능하고, 원하는것을 동작하게 된다는 것을 알게되어 `debian noroot`를 설치했다.

아.. 정말로 설치하니까 `GUI`환경(필요없다 `GUI`)의 `Debian`이 설치가 되었다. 해당 `Debian`을 통해 다시 시도한다고 `git`, `nodejs`를 설치 후 환경설정하고, 시도했으나 `debian noroot`의 경우 이동용기기 화면에 데스크톱화면이 들어가버려, 해당 세팅을 하는데도 시간을 많이 날렸고, 할당되는 램의 크기가 `1G`밖에 되지않아, `메모리`로 나가버리는 경우가 있다는 이슈를 확인하여 `Debian`이 설치된다는 것은 다른 `OS`역시 설치된다는 것으로 이해하고, 방법을 더 찾기로 한다.

### Termux addon Anlinux

처음 `Termux`로 사용할때는 ~~유사~~애뮬이라는 것을 모르고, `addon`들도 사용안하고(뭐많이 설치되는걸 안좋아함) 진행했고, `Anlinux`도 설치는 하고 `ubuntu`가 있는걸 보고 들어는 가봤으나, 어플에서 제시하는 `message`를 읽지않고, 사용법도 몰라 그냥 넘어가버렸던 것이 화근이었다. `Anlinux`를 이용해서 단순하게 `Termux`에 복사된 명령어만 입력하게되면 쉽게 `Ubuntu`가상머신(가상머신 아닐지도모름 그렇다고 명시된것은 아직 못봤음.)을 설치한다. 그 `메세지`만 똑바로 읽고 실행했으면 위 시행착오를 겪지 않아도 될것을 결국 겪어 버렸다.

## 반의 성공

`안드로이드`에 `Termux`를 이용한 간단한 `Ubuntu` 설치와, 정상적인 `npm install`, 정상적인 `서버`실행에 성공하였다. 사실 이과정을 진행하면서 굉장히 시간을 날렸기에, 그 시간이 아까워 서버를 돌리기 전 자동으로 서버를 재실행해주는 `library`를 설치하여 나중에 혹시모를 서버 이슈를 해결하고 싶었지만, 거의 몇일동안 잠도 2~4시간 자가면서 시행착오를 겪은 덕에 먼저 실행을 해 보고 이슈가 발생했을 때 대응하기로했다. 서버가 정상적으로 실행되었고 오류가 발생했다. `Gitub Pages`는 `https`였던것이다. 관련이슈는 검색하여, `https`와 `http`통신에 필요한 규약을 `head`에 `meta`로 추가하고, 다시 시도.. 이번엔 `Promise.fetch`에서 문제가 발생하였다. 처음에는 관련사항을 검색해 보았지만 검색에는 나오지 않는 것을 미루어보아, `클라이언트`와 `서버`간의 주소값을 수정하며 생긴 오류인가 `로그`로 `디버깅`을 했다. 애초에 `서버`측에서는 받아서 `200 성공`이라고 떳지만, `클라이언트`측에서는 똑같이 `Promise.fetch`에서 오류가 생기는 것을 확인할 수 있었다. 이방법 저방법 여러가지 시도해보던 중에 서버를 다시 닫기 위해서 끄려고하니, `터미널`이 뻗었다.

재차 재실행 후 테스트해보았으나, 역시 `터미널(Ubuntu 가상머신)`이 뻗었다.

새벽4시. 물러나자

이후 동기선생님들께 질문 후 `cpu명령어`가 달라 발생한 문제라는 의견과, 전공자 동생에게 애초에 정상적이지 않은 방법을 통해 서버를 구동하려는데 뭐가 문제일지는 예측하기 힘들다, 개발을 10년전 접고 지금은 커피를 말아주는 c언어 고수친구가 그러지말고 그냥 정상적으로 `워크스테이션`을 만들(돈없어 임마)어라고 핀잔을 듣기도 했다.

## 남은 경우의 동작확인

- Clinet -> C
- Server -> S

|---|---|---|---|---|
|num|C|S|성공|실패|
|1|Github pages|데스크탑|성능 혹은 명령어 문제|C 혹은 외부적 요인|
|2|Github pages|S10 5G|성능 문제|C 혹은 외부적 요인|
|3|데스크탑|S10 5G|Github pages 문제|알수없는 요인|

상위 케이스는 해봐야 미련이 없을거같아, 무식하면 용감하고, 무지하면 손발이 고생한다고 했다. 해보자 물론 그건 다다아으으응으ㅡㅁ에 ㅜㅜ

[이전으로](https://kimtank.github.io/personal/2022/10/18/afree-hosting-1.html)
//아직 진행중

//Termux를 이용한 Ubuntu 설치

---

## 참조

> 상단 링크로 궁금한거 찾아보세요