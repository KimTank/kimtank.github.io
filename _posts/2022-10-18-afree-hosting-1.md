---
layout: post
title: "포트폴리오용 웹서버, HTTP서버 만들기 vol.1"
date: 2022-10-18
categories:
- Personal
tags:
- 포트폴리오
- HTTP서버
- Server
- React
- local
- Android
- OS
- Linux
- unix
- Web
- Linux in dex
- Ubuntu touch
- UBport
- Termux
- F-droid
- m205n
- Github pages
---
updateAt 22-10-23

글을 적는 시점은 하루만에 끝낼거라 생각하고 오만하게 시작했던, 실수에서 비롯되었다.

언제나 그렇듯 사람은 겸손해야된다.

A가 a를 Aa한다고 해서,

A가 b를 Aa하는건 아니니까..

나는 A가 a를 Aa하는걸로 Aa == Ab, Ab == Aa, Ba == Aa, Bb == AA일줄 알고 이걸 시작했다.

오만했다. 간략하게 키워드 중심으로 실수했던 과정들을 적어보자한다.

---

createAt 22-10-18
~~두둥 나의 꿈은 일하지않아도 먹고살수있는것.~~
~~이전에는 이걸 장사를 통한 내가 놀아도 수익이 들어오는 소위 auto로 돌린다는 개념으로 생각하던때가 있었다. 그러기위해 고민한건 창업. 무언가의 커뮤니티를 만들어 ad센스광고수익으로 250만원 이상만 매달 채워진다면 하고싶은거(배우고싶은 거라든지, 덕질이라든지)하면서 살수있는게 행복이라고 생각했다. 하지만 늘상 서버라는 측면에서 무너질수밖에 없었고, 그런 나를 위해 네트워크에 대한 기본 지식을 얻게해준 Codestates고마워요 :D 민과장님도 살다가 만나면 인사합시다, 무튼. 이건 이론에관한 정리라든지 포스팅은 아니고 내가 겪었던 과정들을 의식의 흐름대로 정리해서 읽어보면서 참고하실 부분만 참고하시란 부분이기에, 정독안해도되요. 키워드만 보셔도 충분.~~

---

## 1. 발상

1. 토이프로젝트인 아고라스테이츠를 `React`로 리팩토링했다.
2. 서버와 연동하여 `local`에서 동작 확인.
3. 옛날부터 계획했던, `"안쓰는 스마트폰을 활용해서 뭔가 할 수 있는일이 있을까?"`를 회상.
   1. `스마트폰` -> `컴퓨터`
   2. `Android` -> `unix`기반 `os`
   3. `Linux` -> `unix`
   4. `Android` == `Linux`
   5. `OS` 변경
   6. `스마트폰`에 `웹서버`와 `서버`를 구축해서 매핑하면 동작할거야

## 2. 검색

   1. [linux in dex(close 2019)](https://namu.wiki/w/Linux%20on%20DeX): `삼성`이 이런걸 기획했다는 걸 처음 알았다. 풍문에는 `abc`에서 중단요청한걸로 들었다.
   2. [ubuntu touch(close 2015)](https://ko.wikipedia.org/wiki/%EC%9A%B0%EB%B6%84%ED%88%AC_%ED%84%B0%EC%B9%98): [공홈](https://ubuntu-touch.io/)은 아직존재한다. 상당히 깔아보고 싶었던 것 중 하나이다.
   3. [ubports(close 2017)](https://en.wikipedia.org/?title=UBports&redirect=no): [공홈](https://ubports.com/), `ubuntu touch`의 뒤를 이어 `ubports` 커뮤니티에서 개발되어있고, 개발중이다. 국내 제조사인 `삼성`, `LG`의 경우에는 역시나 구현이 많이 되어있지 않고, 그렇다고하니, 해외 제조사인 `Google`, `Xiaomi`, `Sony`등 도 그렇게 최신기기는 지원하지 않고있다. 하지만 파일하나와 간단한 세팅으로도 설치가 가능하다고하니, 관심있다면 [지원기기목록](https://devices.ubuntu-touch.io/)에서 해당되는 남는게 있으면 시도해봄직하다. 종료 선언은 했지만, 우리의 덕후형님들은 열심히 자기가쓸걸 만들어서 '야 이거 써봐 만들었는데 어때'를 해주고 계신다.([앱마켓](https://open-store.io/)도 존재해서 우분투폰이 생기는거다.)
   4. [Termux(ing)](https://namu.wiki/w/Termux): 처음 찾은 방법이자, 결국 설치에 근간이 된 ~~유사~~`애뮬레이터`. [공홈](https://termux.dev/en/), [Github](https://github.com/termux/termux-app), 해당 `애뮬레이터`로 `git`, `nodejs` 설치, `npm` 설치,  진입은 가능하지만, 서버실행 시 추후에 언급될 글에서 나오겠지만, android 자체 문제로 인해 우회하는 방법으로 매번 실행(`vpn`으로 `http://127.0.0.2/home/username/`)해줘야한다. 해당 어플은 `Google play store`에서는 `deprecate`되어(`abc`가 막았대요, 그래서 소송중) `f-droid`에 들어가서 받아야한다.
   5. [f-droid](https://ko.wikipedia.org/wiki/F-Droid): [공홈](https://f-droid.org/), 소문으로만 듣던, `Android`를 벗어나 자유롭게 `안드로이드 운영체제`를 사용하자는 진영(아닐지도 모름)의 `Free Android`, `FOSS`(`Free Open Source Software`) [저장소](https://gitlab.com/fdroid/)이다. 여담으로 `Github`, `Microsoft`의 그늘을 벗어나기위한 [GitLab](https://namu.wiki/w/GitLab)이 있다.(사람마다 말이 다틀려요, 누구는 그래서이다. 누구는 경쟁사거라서 견제한다. 재미로봐주세요.)
   6. [Andronix](https://docs.andronix.app/): [공홈](https://andronix.app/), `android`에서 `windows`까지 편하게 올리게 만들어놓은 무언가(나는 안편했어요 유료에다 환경세팅하는 법을 내가 해야됬거든요)

## 기기환경

1. `클라이언트 서버`: 처음에는 둘다 `npm start`(무식하면 용감함)를 통해 `react`파일 채로 이동시킨 뒤 동작하려고 했다. 하지만 `Github pages`가 생각나게 되어 `Github pages`에서 제공하는 무료 `호스팅`(사실 이걸 호스팅이라고 부르는게 맞을까요)을 사용했다.
2. `서버`: 옛날옛적 사용하던 인도에서 국민폰이라 불린, [Samsung m20](https://namu.wiki/w/%EA%B0%A4%EB%9F%AD%EC%8B%9C%20M20), `m205n`을 사용하였다. 엔트리급 스마트폰으로 15만원정도로 한국에 정발된가아닌 글로벌판을 파는 한국판매자(네이버 쇼핑)에게 구매한것으로 기억한다.

## 중간 저장

이 과정은 18일부터 24일까지 거의 밤샘비슷하게 하면서 진행된 작업으로, 끝끝내 실패로 그쳤다. 하지만 실제로 간단한 서버는 구현해서 server open이라는 문구를 확인했고, 위 과정을 거치면서 원격설정하며 살짝 맛본, 포트포워딩과 ddns설정 등 재밋는 지식을 또 쌓을 수 있었다.

[다음으로](https://kimtank.github.io/personal/2022/10/20/a-free-hosting-2.html)

---

> ## 참조
>
> 상단 링크로 궁금한거 찾아보세요