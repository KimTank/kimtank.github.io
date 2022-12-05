---
layout: post
title: "Optimization"
date: 2022-12-05
categories:
  - Web
tags:
  - Web
  - Javascript
  - Optimization
  - CDN
  - Content Delivery Network
  - Cache
  - Last-Modified
  - ETag
  - If-Modified-Since
  - If-None-Match
  - Tree shaking
  - Babelrc
  - Lighthouse
---

거의 막바지에 이르른거같다. 최적화의 개념이 나오는걸보니, 늘어지면 안되는데 늘어진다.

---

## 1. Optimization

한국정보통신기술협회에서의 정보통신 용어사전에서의 최적화(最適化, optimization)란 "주어진 상황에서 원하는 가장 알맞은 결과를 얻을 수 있도록 처리하는 과정이다. 최적화는 허용된 자원의 한계 내에서 주어진 요구사항을 만족시키면서 최선의 결과를 얻는 과정이다. 수익과 관련되는 분야에서는 이익을 최대로 내는 과정을 말하기도 한다. 다양한 분야와 때에 따라 다르게 정의할 수 있고, 물류(logistics), 설계(design)문제 등에 응용된다."

컴퓨터 공학의 근간 사람대신 기계가 일을하여 비용을 줄일 수 없을까 -> 곧 효율성을 기반으로한 주어진 조건으로 최대 효율을 내는 것을 의미한다.

예를들어 쿠팡이 전국인프라 구축하기위해 전국에 물류센터를 짓고, 각 상점에 물건들을 미리 물류에 비치한 뒤 로켓배송이라는 구독으로 당일배송을 가능하게한것도 어떤면에서는 고객들의 니즈를 반영한 최적화라고 볼 수 있다.

### 1.1. 필요성 및 효과

1. 이탈율 감소: 페이지 로드가 3초이상 걸릴 시 53%의 사용자가 이탈한다. 3초늘 시 32%, 5초늘 시 90%, 6초 늘 시 106%, 10초 늘 시 123%라고 한다. 근래에는 무선통신기술의 발전과 고급칩쳇을 탑재한 기기의 보급화로 더 빨라졌을 거라고 본다. 회사의 수익입장에서는 고객유치에 실패는 곧 폐업의 지름길이다.
2. 전환율 증가: 사라져버린 토종검색엔진이었던 까치넷으로부터, 엠파스, 한미르, 알타비스타, 라이코스, 야후, 심마니, 파란 등 전부 다음, 네이버, 그리고 구글에 거의 모든 국내 유저를 잃었고, 특히 구글의 경우는 특유의 가벼움으로 많은 조선컴퓨터의 전환을 불러왔다.
3. 수익 증대: IT회사의 처음은 무료배포로 볼 수 있다. 그 비용이 투자이든 투자유치이든을 떠나 무료로 사용하게 만든 뒤 유저가 익숙해질때 즈음 유료화를 시킨다. 일단 전환이되어 대다수의 유저가 해당 url의 서비스를 이용중이라면, 광고수익이나 유료 구독을 통한 수익모델적용으로 수익의 증가를 얻을 수 있다.
4. UX 향상: 국내는 지역적특성(땅이좁다)에 맞게 인터넷이 북녁 두메산골에서부터 남녁 땅끝 섬마을까지 유선망과 무선망이 상당히 잘구축되있다. 그래서 그런건지는 몰라도 가까운 일본(땅넓음)이나 미국(그냥넓음)의 검색엔진들과 비교시 상당히 다른 UX를 보여준다. 아직도 100kb속도를 쓰는건지 가벼운 구성의 메인화면으로 다른 정보없이, 텍스트만 보여주는 경우가 많고, 대한민국에서 네이버나 다음이 정치색(뉴스탭이나 실시간검색 등)을 띄는것과는 다르게 구글은 전혀 그런것과는 연관없이 객관적 정보만 전달한다. 그래서 abc를 안쓸래야 안쓸(대체제가 없어)수가없다.

## 2. Optimization 기법

### 2.1. HTML, CSS 최적화

화면 렌더링 시 html, css파일이 필요하다. html은 DOM트리, CSS는 CSSOM트리를 만들고 두개를 병합하여 렌더링할떄 쓴다. 이 중 하나라도 변경 시 리렌더링이되는데, 트리의 크기가 크고 복잡할수록 비용이 비싸기때문에 두가지의 최적화로 렌더링 성능을 향상 가능하다.

#### 2.1.1. HTML 최적화 방법

##### 2.1.1.1. DOM트리 다이어트시키기

DOM트리의 level의 깊고, 자식이 많을 수록 비용은 커진다. 필요한것만 사용한다.

```html
<div>
  <div>
    <p>이리오라</p>
  </div>
</div>

<!-- 변경 -->
<p>혼저옵서예</p>
```

##### 2.1.1.2. 인라인 스타일 사용금지

인라인 스타일은 개별요소에 스타일을 적용하는것으로 구조화시킬 속성을 중복으로 작성(설계없이 만들 시)되는 경우가 있다. CSS파일을 따로 작성하여 한번의 리플로우만 발생하는게 아닌, 계속 리플로우를 발생시켜 렌더링 완료 시점을 늦춘다. 웹표준에 위배되는 이유가 있다.

```html
<div style="background-color: grey">그레이 배경</div>
<section style="background-color: grey">그레이 배경</section>

<!-- 변경 -->
<div class="bg-grey">그레이 배경</div>
<section class="bg-grey">그레이 배경</section>

// style.css .bg-grey { background-color: grey; }
```

#### 2.1.2. CSS 최적화

##### 2.1.2.1. 사용하지 않는 CSS 제거

CSS파일의 모든 코드의 분석이 끝난 후 CSSOM트리가 생성되는데, 잉여 CSS코드가 있을 시 불필요한 비용이 들어간다. 리팩토링 시 확인하여 사용하지않는 요소에 대한건이나, 불러쓰지않는(html, css간 커넥트를 확인할수없음) 값들을 문서로 따로 관리를하던 만든사람이 외계인이라 다 기억을 하던, 진정한 의미의 리팩토링을 해야한다.

##### 2.1.2.2. 간결한 셀렉터 사용

```css
.bg-grey .tc-white #theme-grey {
  ...;
}

/* 변경 */
.theme-grey {
  ...;
}
```

### 2.2. 리소스 로딩 최적화

파일을 불러오는 위치, `<script>, <link>`에따라 렌더링 완료점이 변경된다.

1. CSS파일 불러오기: DOM트리와 CSSOM트리가 필요하다. css파일은 html상단의 head요소 안에서 불러와야한다.
2. JavsScript파일 불러오기
   - js는 dom트리와 cssom트리를 동적으로 변경할 수있다. html코드 파싱 중 스크립트태그를 만나면 해당 스크립트가 실행된다. 스크립트태그 요소 이전까지 생성된 DOM까지만 접근할수 있고, 스크립트 태그 요소를 HTML코드 중간에 넣으면 해당 요소 이후 생성된 dom을 수정하는 코드가 있는 경우에는 화면이 의도한대로 표시되지 않는다.
   - 스크립트 실행이 완료전까지 dom트리 생성이 중단된다. js파일을 다운받아서 사용하는 경우 다운로드 및 스크립트 실행이 완료시까지 dom트리 생성이 중단된다. dom 트리 생성이 중단된 시간만큼 렌더링 완료시간은 지연된다.
   - 상기의 이유들로 js파일은 dom트리 생성이 완료되는 시점인 html문서 최하단에 배치

### 2.3. 브라우저 이미지 최적화

실질적으로 ux을 위해서는 코드보다는 리소스, 미디어파일이 비용이 크다. 하여 파일에대한 최적화는 필수이다.

1. 이미지 스프라이트: 이미지 요청수를 줄이기위해 한이미지파일만 불러온 뒤 css의 background-position으로 이미지의 필요부분만 보여주는 방법이다.
2. 아이콘폰트 사용: 일반적인 이미지보다는 아이콘폰트를 사용해 비용을 줄일 수 있다.
   1. [font-awesome](https://fontawesome.com/docs/web/setup/use-kit): icon font를 제공해주는 서비스
      - CDN으로 사용
      - font awesome 모듈 설치
   2. WebP또는 AVIF이미지 포맷 사용: WebP는 PNG대비 26%용량이 감소되었고, AVIF는 JPEG대비 50% 감소되었고, WebP대비 20%감소된다. 모든브라우저에 호환은 되지않으며, 구버전 브라우저에서는 안된다. 하여 이미지 호환에 맞게 `<picture>`태그를 사용하면 분기를 대체할수있다.

```html
<picture>
  <source srcset="pic.webp" type="image/webp" />
  <img src="pic.png" alt="너의 얼굴" />
</picture>
```

### 2.4. CDN 사용

Content Delivery Network로 콘텐츠를 빠르고 효율적으로 제공하기위해 설계되었다. 네트워크 지연(latency)은 유저와 호스팅 서버간의 물리적 거리의 한계가 존재하기에 발생할수밖에없고, 유저와 서버의 거리가 멀다면 지연은 늘어난다. CDN은 서버를 분산하여 이러한 문제를 해결하고자 했다.

출처: [알리바바 클라우드](https://www.alibabacloud.com/ko/knowledge/what-is-cdn)

![https://www.alibabacloud.com/ko/knowledge/what-is-cdn](/assets/img/221205-cdn.png)

## 3. Cache 사용

캐시는 임시장소이다. 다운로드 받은 데이터나 값을 미리 복사해놓는 곳으로 데이터에 접근하는 시간이 오래 걸리는 경우나 값을 다시 계산하는 시간을 절약하기위해 사용한다. `Cache-Control: max-age=${value}`라는 명세로 value초만큼 cache에 저장한다. 첫번째 요청에 저장했을 시 두번째부터는 캐시를 우선조회한다. cache에 해당 값이 남아있을 시 cache에서 데이터를 가져온다. cache 유효기간이 지날 시 는 서버에서 받아온다.

- 캐시 유효시까지 네트워크 비용 절감
- 불필요한 연산없어 로딩 속도 개선
- ux향상(...)

```bash
<!-- response -->
HTTP/1.1 200 OK
Content-Type: image/png
Cache-Control: max-age=60
Content-Length:...

...
```

### 3.1. 캐시 검증 헤더와 조건부 요청

캐시 유효 만료이나 서버에서 다시 받는 리소스가 캐시에 저장된 리소스와 완전히 동일할 때, 서버의 파일과 캐시파일이 동일한지 확인해 재사용하는걸 가능하게하는게 캐시 검증헤더와 조건부 요청 헤더이다.

#### 3.1.1. 캐시 검증 헤더

캐시에 저장된 데이터와 서버의 데이터가 동일한지 확인하기 위한 정보를 담은 응답헤더이다.

- Last-Modified: 데이터가 마지막으로 수정된 시점을 의미하는 응답 헤더이다. 조건부 요청헤더인 If-Modified-Since와 같이 사용한다.
- ETag: 데이터버전을 의미하는 응답헤더이다. 조건부 요청헤더인 If-None-Match와 묶어서 사용한다.

#### 3.1.2. 조건부 요청 헤더

캐시의 데이터와 서버의 데이터가 동일하다면 재사용하게 해달라는 의미의 요청 헤더이다.

- If-Modified-Since: 캐시된 리소스의 Last-Modified값 이후에 서버 리소스가 수정되었는지 확인하고, 수정되지 않았다면 캐시된 리소스를 사용한다.
- If-None-Match: 캐시된 리소스의 ETag값과 현재 서버 리소스의 ETag값이 같은지 확인하고, 같으면 캐시된 리소스를 사용한다.

#### 3.1.3. usage

##### 3.1.3.1. Last-Modified & If-Modified-Since

- 첫번째 요청을 보내고 응답을 받으며 캐시 유효시간이 있는 리소스를 같이 받아온다. 서버의 파일이 마지막으로 수정된 시간을 의미하는 Last-Modified헤더에 담긴 내용도 캐시에 함께 저장한다.
  1. 웹브라우저 요청: GET /resource.확장명
  2. HTTP 헤더: Last-Modified: 데이터가 마지막에 수정된 시간
  3. 서버: 리소스 + 데이터 최종 수정
  4. 1.1M 전송: HTTP 헤더: 0.1M, HTTP바디: 1.0M
  5. 웹브라우저 렌더링
  6. 브라우저 캐시: 캐시와 수정일 정보 담김, 지정한 유효시간 + 데이터 최종 수정일
- 유효시간 초과 후 두번째 요청 보내면, 유효시간이 지났어도 해당 데이터를 재사용해도 되는지 확인을 위해 verify를 한다. 데이터 수정이 없었지만 유효기간은 지나 동일한 데이터를 받아와야할 때 If-Modified-Since를 작성하고 캐시에 함께 저장해놓았던 Last-Modified값을 담아 요청을 보낸다. 이 값을 이용해 서버 데이터의 최종 수정일과 캐시에 저장된 데이터의 수정일을 비교한다. 두 데이터가 동일한 데이터라면 최종 수정일이 같아야한다.
  1. 웹브라우저: GET /resource.확장명 + If-Modified-Since: `${value}`
  2. 서버
  3. resource + 데이터 최종수정일
  4. 캐시 데이터최종수정일 비교해서 데이터 수정이 없다.
  5. 그대로 사용
- 서버와 캐시의 데이터가 동일한 데이터임이 검증되었다면 서버는 변경없음이라는 304 Not Modified라는 응답을 보내고, 캐시 데이터 유효시간이 갱신되며 해당 데이터를 재사용할 수 있다.
  1. 캐시의 데이터수정일 - 서버 데이터 최종 수정일 검증
  2. 0.1M 전송: HTTP헤더: 0.1M, `HTTP/1.1 304 Not Modified ... Last-Modified: ${value}` HTTP Body가 없다.
  3. 캐시의 유효시간 갱신
  4. 웹브라우저 렌더링

##### 3.1.3.2. ETag & If-None-Match

- 첫번째 요청을 보내고 응답을 받으면서 캐시 유효시간인 리소스를 받아온다. 서버파일버전을 의미하는 ETag헤더에 담긴 내용도 캐시에 함께 저장한다.
  1. 웹브라우저 요청: GET /resource.확장명
  2. HTTP/1.1 200 OK ... ETag: `${value}`
  3. 서버
  4. resource 1.1.M전송: HTTP 헤더: 0.1M, HTTP 바디: 1.0M
  5. 브라우저 렌더링
  6. 캐시에 저장: 유효시간 + ETag: `${value}`
- 캐시 유효시간을 초과한 후에 두번째 요청을 보내면 유효시간이 지났어도 해당 데이터를 재사용해도 되는지 확인을 위해 ETag로 캐시와 서버의 데이터의 버전을 검증한다. 동일할 시 If-None-Match를 작성하고 캐시에 함께 저장한 ETag값을 담아 요청을 보낸다.
  1. 웹브라우저 요청: GET /resource.확장명 + If-None_Match: `${value}`
  2. 서버
  3. resource.확장명 + ETag: `${value}` - 캐시 유효시간 초과 + ETag: `${value}` => 비교
- 서버와 캐시의 데이터가 동일한 데이터임이 검증되면 서버는 데이터가 수정되지 않았다는걸 의미하는 304 Not Modified라는 응답을 보내주고, 캐시 데이터 유효시간이 갱신되면서 해당 데이터를 재사용할 수 있다.
  1. 브라우저 캐시 유효기간 살아있음 + ETag: `${value}` - 서버 + ETag: `${value}` => 검증
  2. 0.1M 전송: HTTP 헤더: 0.1M, HTTP/1.1 304 Not Modified + ETag: `${value}`, HTTP Body가 없음
  3. 웹브라우저

## 4. Tree shaking

나무를 흔들어 불필요한 코드를 제거하는 것을 의미한다.

### 4.1. JavaScript Tree shaking

Webpack 4이상에서는 ES6 모듈(import, export)을 대상으로 기본적 tree shaking을 제공한다.

#### 4.1.1. 필요한 모듈만 import하기

```javascript
import {useStates, useEffect} from 'react'
```

#### 4.1.2. Babelrc 파일 설정하기

js문법이 구형 브라우저에서도 호환되기 위해 ES5문법으로 변환하는 라이브러리이다. ES5문법은 import를 지원하지 않기에 commonJS분법의 require로 변경시킨다. require가 export되는 모든 모듈을 불러오기때문에 tree shaking이 어렵다. 그리하여 Barbelrc 파일에 설정을 해줘야한다. 해당값을 true로 놓을 시 항상 ES5문법으로 변환한다.

```json
{
  “presets”: [ 
    [
      “@babel/preset-env”,
      {
      "modules": false
      }
    ]
 ]
}
```

#### 4.1.3. sideEffects 설정

webpack은 side effects를 일으킬 수 있는 코드의 경우, 사용하지 않는 코드라도 tree shaking 대상에서 제외시킨다.

순수함수가 아니기에 tree shaking을 통해 제외하는 경우 문제가 생길 수 있다고 webpack은 판단하기에 제외하지 않는다. package.json파일에서 sideEffects에 대한 설정하여 app전체에 사이드 이펙트가 없을 것이라고 설정한다.

```json
{
  "name": "tree-shaking",
  "version": "x.x.x",
  "sideEffects": false
}

// 특정파일 설정시

{
  "name": "tree-shaking",
  "version": "x.x.x",
  "sideEffects": ["./src/some-path/some-javascript.js"]
}
```

#### 4.1.4. ES6문법 사용하는 모듈 사용하기

ES5로 작성된 모듈이 있을 수도 있기때문에 ES6로 작성된 다른 라이브러리를 사용하는 것을 권장한다.

## 5. Lighthouse

구글에서 개발한 오픈소스 자동화툴로 성능, 접근성, PWA, SEO 등을 검사하여 웹페이지 품질검사를 한다.

1. chrome 개발자 도구에서 실행
   1. generate report로 실행
2. Node CLI 실행

```bash
# 전역으로 설치하는게 좋다.
$npm install -g lighthouse

$lighthouse `${url}`

$lighthouse --help
```

### 5.1. 분석 결과 항목

1. Performance: 웹성능을 측성, 화면에 콘텐츠가 표시되는데 걸리는 시간, 표시 된 후 사용자와 상호작용시간, 불안정요소 등을 검사한다.
2. Accessibility: 웹페이지가 웹접근성을 갖는지 확인한다. 대체 텍스트, 배경색과 콘텐츠 색상, 대비, WAI-ARIA속성 사용여부 등을 검사한다.
3. Best Practices: 웹페이지가 웹 표준모범사례를 따르는지 확인한다. HTTPS 프로토콜 사용여부, 콘솔에 오류 표시 여부를 검사한다.
4. SEO: 웹페이지가 검색엔진에 최적화가 잘 되었는지 확인한다. robots.txt 유효여부, meta 요소, 텍스트 크기 확인
5. Progressive Web APP(PWA): 해당 웹사이트가 모바일 앱에서 잘 작동하는지 확인한다. 앱 아이콘 동작, 스플래시 화면 여부, 화면 크기에 맞게 콘텐츠 배치여부를 체크리스트로 확인한다.

### 5.2. Performace 측정 메트릭

1. First Contentful Paint(FCP): 성능지표 메트릭이다. 1.8초 이하여야한다.
2. Largest Contentful Paint(LCP): 뷰포트를 차지하는 가장 큰 콘텐츠의 렌더 시간을 측정한다.

|LCP time(in seconds)|Color-coding|
|---|---|
|0-2.5|fast(green)|
|2.5-4|moderate(orange)|
|over 4|slow(red)|

3. Speed Index: 성능 지표를 추적하는 메트릭이다. 페이지를 로드하는 동안 얼마나 빨리 컨텐츠가 시각적으로 표시되는지 측정한다.

|Speed Index(in seconds)|Color-coding|
|---|---|
|0-3.4|fast(green)|
|3.4-5.8|moderate(orange)|
|over 5.8|slow(red)|

4. Time to interactive: 페이지가 로드되는 시점부터 사용자와의 상호작용이 가능한 시점까지의 시작을 측정한다.
   - 페이지에 FCP로 측정된 컨텐츠가 표시되어야한다.
   - 이벤트 핸들러가 가장 잘보이는 페이지의 엘리먼트에 등록된다.
   - 페이지가 0.05초안에 사용자의 상호작용에 응답한다.

기준: 아카이브된 HTTP 데이터

|TTI metric(in seconds)|Color-coding|
|---|---|
|0-3.8|fast(green)|
|3.9-7.3|moderate(orange)|
|over 7.3|slow(red)|

5. Total Blocking Time: 유저와 상호작용하기까지 막혀있는 시간을 측정한다. FCP와 TTI사이에 긴시간이 걸리는 작업들을 모두 기록하여 TBT를 측정한다.
6. Cumlative Layout Shift: 사용자에게 컨텐츠가 화면에 얼마나 많이 움직였는가(불안정한가)를 수치화한 지표이다.

## 참조

> [한국정보통신기술협회: main](https://www.tta.or.kr/)  
> [font awesome: main](https://fontawesome.com/)  
> [google: introducting material symbols](https://fonts.google.com/icons)  
> [font awesome: doc](https://fontawesome.com/docs/web/setup/use-kit)  
> [caniuse: webP](https://caniuse.com/webp)  
> [caiuse: avif](https://caniuse.com/?search=AVIF)  
> [aws: cloudfront](https://aws.amazon.com/ko/cloudfront/)  
> [cloudflare: main](https://www.cloudflare.com/)  
> [httparchive.org: state of javascript/bytesjs](https://httparchive.org/reports/state-of-javascript#bytesJs)  
> [github: speedline](https://github.com/paulirish/speedline)  
> [httparchive.org: report/loading-speed/ttci](https://httparchive.org/reports/loading-speed#ttci)  
> [CLS 지표 작동원리](https://www.youtube.com/watch?v=zIJuY-JCjqw)