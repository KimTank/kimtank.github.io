---
layout: post
title: "웹표준 & 접근성 vol.1"
date: 2022-11-04
categories:
- Web
tags:
- Web standard
- accessibility
- W3C
- Semantic HTML
- header
- nav
- aside
- main
- article
- section
- hgroup
- footer
- markup
- coss browsing
---

---

## 1. 웹표준

인터넷은 웹기반이 아니다. 인터넷은 전 세계적으로 연결되어있는 컴퓨터 네트워크 통신망이다. 웹또한 인터넷에 포함되는 인터넷이 더 포괄적인 개념이다. 웹은 공간이다. 여러가지 정보를 다른사람들과 공유할 수 있는 공간이 웹이다.

World Wide Web

2000년 초에는 여러 브라우저가 있었고, 화면의 표준이 없어 각 사이트마다 다 달라 UX가 좋지 않았다. 이런 춘추전국시대를 개발자들이 통일하고, 긍정적인 사용자 경험을 이끌어 낼 수 있는 웹개발의 형식이 웹표준이다.

### 1-1. 웹표준 개념

[W3C(World Wide Web Consoritium)](https://www.w3.org/)에서 권고하는 웹에서 표준적으로 사용되는 기술이나 규칙으로 사용자가 어떤 OS나 브라우저를 사용해도 웹페이지가 동일하게 보이고, 동작할 수 있도록하는 웹페이지 제작 기법이다. 웹개발의 언어인 HTML, CSS, JS를 기술한다.

### 1-2. 장점

1. 유지보수의 용이성: 영역 분리로 유지보수와 코드 경량화, 트래픽이 감소
2. 웹 호환성 확보: 특정OS나 브라우저 종속성을 벗어나, 동일한 결과 나올 수 있게함.
3. 검색 효율성 증대: 검색엔진에 노출 및 검색 효율성으로 홍보효과 증대
4. 접근성 향상: 다양한 환경에 대응할 수 있음.

HTML이 중요

## 2. Semantic HTML

이전 section1에서 나왔던 Semantic HTML이 다시 나왔다. 그만큼 중요하단 건가

- semeantic: 의미가 있는
- HTML: 마크업 언어

### 2-0. 화면구성

#### 2-0-1. div와 span 화면구성

출처: [codestates s3-u5-c1-2. semantic HTML #1 div와 span으로 화면구성](https://www.codestates.com/?gclid=CjwKCAjwzY2bBhB6EiwAPpUpZnTaBjb9ALdrERHndByCw80PWH8-6gWz-uXRV2zSfS2OHPzPc56snBoCQzUQAvD_BwE)
![https://www.codestates.com/?gclid=CjwKCAjwzY2bBhB6EiwAPpUpZnTaBjb9ALdrERHndByCw80PWH8-6gWz-uXRV2zSfS2OHPzPc56snBoCQzUQAvD_BwE](https://s3.ap-northeast-2.amazonaws.com/urclass-images/1qRj1tgnLi5Se2OXOJ_vH-1657000600375.png)

상기 그림으로만은 각 영역이 어떤 부분을 담당하는지 알기는 어렵다.

#### 2-0-2. semantic elements로 화면구성

출처: [codestates s3-u5-c1-2. semantic HTML #1 div와 span으로 화면구성](https://www.codestates.com/?gclid=CjwKCAjwzY2bBhB6EiwAPpUpZubqWcU8ttyrKECwgAUo2Z48iExWxB5mVnY28i8fEFD7mCfxr0JEWhoCJX4QAvD_BwE)
![https://www.codestates.com/?gclid=CjwKCAjwzY2bBhB6EiwAPpUpZubqWcU8ttyrKECwgAUo2Z48iExWxB5mVnY28i8fEFD7mCfxr0JEWhoCJX4QAvD_BwE](https://s3.ap-northeast-2.amazonaws.com/urclass-images/Auk-kv7mH-RiTFe1NG92V-1657000637391.png)

위 그림과 같이 semantic HTML로 구성 시 어떤 역할을 하는지 명확하게 구분이 가능하다.

### 2-1. 필요성

1. 개발자간 소통: 각요소에 대한 정의를 주석으로 남기거나, 코드리뷰를 하지 않아도 된다.
2. 검색 효율성: 검색엔진은 HTML요소를 보고 구조를 파악한다. 태그가 div와 span으로만 이루어져 있다면, 검색엔진은 페이지내 정보가 어떤게 있는지 알 수 없다.
3. 웹 접근성: semantic HTML 요소로 이루어져있을 경우 음성을 통해 요소 내 컨텐츠 전달 시 더욱 빠른 접근이 가능하다.

### 2-2 종류

|---|---|
|종류|설명|
|header|최상단 머릿말|
|nav|메뉴, 목차 등|
|aside|문서와 연관있으나, 직접연관 없는 내용|
|main|주요 content|
|article|게시글, 뉴스 기사 등 독립적 구분으로 재사용할 수 있는 내용. hgroup을 포함하는 방법으로 구분|
|section|독립적인 구획, 적합한 의미의 요소가 없을 때 사용. 제목 hgroup을 포함하는 경우 많음|
|hgroup|제목을 표시할 때 사용, h1~h6|
|footer|최하단에 위치하는 꼬릿말|

### 2-3. 자주틀리는 마크업

1. 인라인 요소 안 블록 요소 넣기: 대표적 인라인 요소는 span, 블록요소는 div이다. 인라인 요소는 항상 블록 요소안에 들어가야한다. 반대는 허용하지 않는다.
2. b, i 요소 사용: bold와 italic요소이나, semantic에서는 사용하지 않는 것이 좋다. 표현을 기준으로 이름이 지어진 요소이기에, 똑같은 스타일을 부여하여 콘텐츠에 의미를 부여하는 strong, em요소를 사용하는 것이 좋다.
3. hgroup 마구잡이 사용: 목차의 역할을 하며 콘텐츠의 상하 관계를 나타내기위해 사용하는데, bold효과나 띄워쓰기 효과를 위해서 사용하면 안된다.(고마워요 Markdown all in one)
4. br/ 연속 사용: 줄바꿈은 문맥을 끝내고 다음이야기를 하기 위해서 사용한다. 하지만 요소사이 간격을 만들기위한 수단으로 사용하면 안된다. 별도의 단락을 나누거나, css속성을 이용해 여백을 조정해야 한다.
5. 인라인 스타일링 사용: 웹표준으로 html/css/js를 분리한것을 인라인 스타일링으로 다시 합치면안된다.

## 3. cross browsing

웹사이트에 접근하는 브라우저의 종류에 상관없이 **동등한**(동일한아니에요) 화면과 기능을 제공할 수 있도록 만드는 작업이다. 브라우저마다 사용하는 렌더링 엔진(우와)이 다르기에 화면을 완전 동일하게 만드는 것은 불가능하다. 모든 브라우저에서 동등한 수준의 정보와 기능을 제공하는 것이다.

옛날옛적 천리안 -> explorer -> 파폭, 사파리 -> 크롬(오페라는 좀) 전세계 시장에서는 2012년, 한국시장에서는 2016년 크롬으로의 사용자 이동이 있었다. 아직도 일부 정부사이트는 멜웨어같은^^ ~~안랩~~과 비스무리한 activeX를 사용하는 아름다운 사이트들이 많다.

마소조차도 IE를 고이 보내드리고 엣지를 공개하며, 혁신을 꿈꾸지만.. 글쎄요 ~~나마스떼~~ 사티아 과연.. 윈도우에서만 잘돌아가는 엣지가 다른 기기에서의 호환성을 못맞추면 크롬이나 사파리 파폭처럼 될수있을까요?

무튼 중요한건 과거에 크로스 브라우징문제 때문에 개발자들이 욕을 봤다. 실지로도 생산성과 돈은 연관되어 있기에, 일정사이트들은 일정 브라우저만 정상지원한다고 명시해놓았다. 돈만있음 못할건없지만, 언제나 사업이란건 투자 대비해 많은 돈을 벌어들어야 하는 자본의 논리기에, 크로스 플랫폼도 고려하여 추후 확장은 보아야 겠으나, 처음부터 완벽할 필요는 없다.(개인생각)

## 3-1. workflow

1. 기획: 어떤 사이트인가? 어떤 내용과 기능이 있나? 디자인은 어떤가? 고객은 누구인가? 고객이 사용하는 브라우저는 무엇인가? 타켓의 브라우저와 기기에 따라 맞는 기술을 사용하도록 기획하자
2. 개발: [mdn](https://developer.mozilla.org/ko/), [can i use](https://caniuse.com/) 등을 통해 브라우저가 지원하는 호환성을 확인하자. 타켓이 IE가 많다면(고인은 좀 보내드립서다) 고려할것이 많다. 예를 들어 최신기술보다는 레거시한 기술로 [마이그레이션](https://www.redhat.com/ko/topics/automation/what-is-it-migration)한다던가 등.
3. 테스트: 기능 구현 후 테스트를 통해 요구사항이 충족되었는지 확인하고 다시 수정하고 출시하자. 안정적인 데스크톱 브라우저, 휴대폰 및 태블릿 브라우저, 초기 기획 목표 브라우저, 다양한 운영체제 등에 테스터를 고용해 돌리자(으아아아아), 자동테스트를 진행하는 도구도 좋다. TestComplete, LambdaTest, BitBar등이 있다.
4. 수정/반복: 테스트로 발견된 버그를 수정하고 다시 테스트하고를 반복한다.

---

## 참조

> [w3: main](https://www.w3.org/)   
> [codestates: main](https://www.codestates.com/?gclid=CjwKCAjwzY2bBhB6EiwAPpUpZnTaBjb9ALdrERHndByCw80PWH8-6gWz-uXRV2zSfS2OHPzPc56snBoCQzUQAvD_BwE)   
> [mdn: semantics](https://developer.mozilla.org/ko/docs/Glossary/Semantics)   
> [mdn: main](https://developer.mozilla.org/ko/)   
> [can i use: main](https://caniuse.com/)   
> [red hat: migration](https://www.redhat.com/ko/topics/automation/what-is-it-migration)