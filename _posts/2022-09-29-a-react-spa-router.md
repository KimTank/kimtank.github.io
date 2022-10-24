---
layout: post
title: "JavaScript React SPA & Router"
date: 2022-09-29
categories:
- JavaScript
tags:
- JavaScript
- React
- SPA
- React Router
- Single Page Application
- Wireframe
- Mockup
---

근래에 경기가 힘든만큼 사람들이 집에서 숨쉬는, 내게는 필요하지만 본인에게는 필요없는 물건들을 막 던지기 시작했다.

중고거래는 중학교때부터 왕왕해왔다. 당시에는 중고나라나 다나와를 통해 내능력으로는 사지못하는 물건을 싸게 구입해서 쓸만큼 쓰고, 비싸게 판매한다던지 그런 식으로 해왔다. 그게 나중에는 자동차나 자전거, 핸드폰 등 고가물건의 경우는 대부분 그런식으로 A/S(어차피 잘 안받기에)지난 물건들을 들고와 잘쓰고 다시 되파는 방식으로 해왔다.
 
중고거래라는건 전제조건이 깔린다. 1. 필요하다. 2. 시간이 많다. 3. 돈이 있다. 필요하지 않은건 없다. 다 필요하니까 사놓는거다. 하지만 잘 안쓸뿐, 돈은 없다. 하지만 싼걸사면된다(함정).. 현재의 내게는 2번이 문제였다. 사람들이 이전 중고나라카페와 다나와중고장터를 이용하던 시절에는 정보를 아는사람이나 안전결재에대한 이해가 되지 않으면 대부분 사기를 당했기에 중고에대한 인식이 매우 안좋으나, 당근마켓이라던가 헬로마켓, 번개장터, 중나(모바일) 등 중고시장이 매우 커짐에 따라, 학습하기 시작했다. 리셀이라던가 어차피 비싸게 올려도 살사람은 산다라던가? 무튼 그래서 중고시장가격이 전체적으로 올랐기에 접었던 줍줍질을 바쁘기도했고, 바쁘니 별쓸일도없어 거의 접었다가 최근. 필요하다와 시간이있다(출퇴근시간이 안들어서 2시간을 벌었다 :D)라는 핑계로 펑펑쓰기 시작했다.

발단은 내물건을 팔려고 올려놓고 뭐가요새는 있나 구경하면서부터 시작일것이다. 그로서 나는 시간을 어떻게보면 비효율적으로 사용했고, 심심하면 앉아서 잠들어버리는 최악의 실수를 반복하게 된다. 오늘도 벙커침대 3개 주으러간다. 아마 이거 이후로는 티비와 필요하다면 홈시어터, 4k급 모니터 등 대부분은 새걸로 살만한 것들만 남기에 온전히 집중할 수 있는 여건을 만들겠지만. 

정말 바쁘다고 거절해도 생일이라고 핑계대고 넘어오는 친구(~~화내서 삐졌다 ^^ 오지마 진짜 줘패버린다~~)들부터 생일챙겨줬다고 고맙다고 또 놀려고 핑계대는 내모습(~~할땐하자 제발 미친자야~~)까지 이젠 그것도모자라 필요함을 핑계삼아 중고거래(직거래위주)로 시간을 엄한데 쓰는 나는 혼나야한다. 

적어도 포스팅만은 미루지말자던 그 약속은 요단강을 건너셨나 시작의 나 데리고와라 지금의나 정신차리자. 눈깜짝할새 리액트다. 가자.

---

## React SPA

SPA(Single-Page Application)

이름만봐서는 android fragment와 비슷한 구조일거같다. Activity 하나에서 여러 fragment들을 생성 삭제하면서 activity 이동간에 발생하는 문제들을 보완하려했던? 물론 추후에는 한 Activity에서 모든걸 해결하려다 보니 구조가 복잡해질 수 밖에 없게 되어, 나중에는 필요한곳에서만 사용되도록 설계권장되었던 android의 중요기능 맥락은 다를거같지만 개념은 비섯할거같다.

### SPA histories

|---|---|---|---|---|
|Client|-|action|-|Server|
|pc(me)|->|Request|->|google...|
|user(other)...|<-|index.html|<-|HTML files|

이전 클라이언트(유저)측에서 서버(홈페이지. 서버)측에 접속 후 페이지를 이동(화면을 불러오도록 요청)하면 매번 브라우저는 페이지를 HTML파일로 된 전체를 불러왔다.

이전에는 Header든 Footer든 Navigation이든 전부 페이지를 불러왔고(비효율적)이걸 깜빡인다라고 표현한다.

하지만 현재는 필요한건 그대로 놔둔 상태에서 변경될 부분만 샥샥 바꿔끼는 모양을 한다.(android랑 비슷하네)

언제나 그렇지만, 서비스가 조그만할때는 아무런 문제가 없다. 하지만 이용자수가 늘어나고, 서비스가 거대해질수록 트래픽문제라던지 중복된 요소들을 줄이지 않으면 ux적으로도 서비스의 접근성이 떨어지게된다.

1990년 후반 업데이트에 필요한 데이터만 전달받아 동적으로 HTML 생성하는 방식 -> 2000년 중반 그런 웹애플리케이션이 보편화되었고, Single-page Application.의 시대가 왔다.

### SPA 장점

메뉴 하나를 눌렀을 때 페이지전체 이동을 하는것이 아니라 해당 메뉴에 해당하는 내용만 바꿔치기(실제로는 덮어지는게 아니라 기존내용을 날리고 새로운걸 띄우겠지만)해버리는, 작은 예로 추천

대표적 서비스로 Youtube, facebook, Gmail, airbnb, netflix 등

### SPA 단점

1. 화면을 처음 불러올(로딩) 시 HTML파일을 리딩, `<script>`요소안의 JS파일 다시 받아온다. HTML파일은 가볍고, JS파일은 무거워질 수 밖에 없다(대부분의 기능이 여기있으니), 그러다보니 첫화면을 불러오는 시간(로딩시간)이 길어진다. 
2. 검색엔진 최적화가 안좋다. 크롤링하기 어렵다는 이야기같다. HTML DOCUMENT이지만 필요기능을 JS로 구현하니 그런거같다. 하지만 천재분들이 그것조차도 긁어오도록 바꿔가는 추세이므로 점점 줄어들고 있다고는 한다.

굉장히 android랑 비슷한데 맥락이 다르다. 처음의 예상과는 틀리구나.

## Wireframe & Mockup

그래서 SPA는 뭔지 알겠다. 그럼 React에서는 SPA를 어떻게 구현하는지 알아봅시다. 감도안와요 :D

### Wireframe

선과 윤곽선(frame)으로 웹페이지의 레이아웃과 UI요소등에대한 뼈대를 잡는것을 말한다.

### Mockup

목업으로 전직장에서 뻔질나게 들었던 목업목업목업, desktop이나 smartphone의 frame에 씌워 직관적으로 디자인한것을 말한다.~~(그게 그거아님메?)~~

## React Router

화면별 주소가 다른데 다른 주소에 따라 다른 뷰를 보여주는 과정을 '경로에 따라 변경한다'는 의미로 라우팅이라고 한다.

React에서는 따로 Routing기능을 내장하고 있지 않기에 React Router(1억다운로드??)라는 library를 가장 많이 사용한다.

## React Router Library

|---|---|---|
|router|route matchers|route changers|
|`<BrowserRouter>`|`<Routes>`|`<Link>`|
|-|`<Route>`|-|

### 설치

```bash
$npm install react-router-dom@^x.x.x
```

### import

```javascript
//비구조화 할당(destructuring assignment)과 비슷하게 이용할 수 있다.
import { BrowerRouter, Routes, Route, Link} from "react-router-dom";
```

### usage enviroment setting

```javascript
<BrowerRouter>
    <div>
        <nav>
            <ul>
                <li>
                    <Link to="/">Home</Link>
                </li>
                <li>
                    <Link to="/about">Mypage</Link>
                </li>
                <li>
                    <Link to="/dashboard">Dashboard</Link>
                </li>
            </ul>
        </nav>

        <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<Mypage />} />
            <Routes path="/dashboard" element={<Dashboard />} />
        </Routes>
    </div>
</BrowserRouter>
```

### BrowerRouter

HTML5 [History API](https://developer.mozilla.org/ko/docs/Web/API/History_API)를 사용해 페이지를 새로고침하지 않고 주소를 변경할 수 있게 한다.

상위에 작성되어 있어야 React Router 컴포넌트들을 사용할 수 있다.

### Routes & Route

경로를 매칭해주는 역할을 한다.

- Routes: Route를 감싸 경로가 일치하는 단 하나의 라우터만 렌더링한다. Routes를 사용하지 않으면, 매칭되는 모든 요소 렌더링함.
- Route: path attribute 지정하여 mapping한다. Link가 정해주는 URL과 일치해야 작동한다.

```javascript
<Routes>
    <Route path="/" element={<main />} />
    <Route path="/signin" element={<signin />} />
    <Route path="/signup" element={<signup />} />
    <Route path="*" element={<unkownrequest />} />
</Routes>

// /*의 경우 지정되지 않은 주소로 접근할 시 보여주는 페이지로 이동한다.
/**
 * 각 주소를 입력했을 시 예시
 * https://www.example.net/ -> main
 * ...net/signin -> signin
 * ...net/signup -> signup
 * ...net/* -> unkownrequest
 */
```

### Link

경로를 연결해주는 역할을 하는 컴포넌트로 페이지 전환을 통해 페이지를 새로 불러오지 않고, Application을 그대로 유지, HTML5 History API를 이용해 페이지의 주소만 변경해준다.

ReactDOM render 시 a태그로 변경됨(a태그는 페이지 전환하는 것이 있음. 그것을 wrapper나 ex)

Link의 to attribute를 사용해 Route에서 path로 설정해둔 주소를 연결한다.

```javascript
const App = () => {
    return (
        ...
        <ul>
            <li>
                <Link to="/">Main</Link>
            </li>
            ...
        </ul>
        ...
    )
}
```

### useNavigate

> IMPORTANT
> 일반적으로 'redirect'가  loders and hook action에 더 좋음.

```javascript
import { useNavigate } from "react-router-dom";

function useLogoutTimer() {
  const userIsInactive = useFakeInactiveUser();
  const navigate = useNavigate();

  useEffect(() => {
    if (userIsInactive) {
      fake.logout();
      navigate("/session-timed-out");
    }
  }, [userIsInactive]);
}
```

1. 선택적 두 번쨰 인수를 사용, 'to'값을 전달 하거나 Link to, {replace, state}
2. 히스토리 스택에 가고자하는 델타를 전달(ex: navigate(-1) back버턴 동일)

> ## 참조  
> [solwalk:UI, UX기획을 손쉽게, 와이어프레임](https://slowalk.com/2140)   
> [디지털타임스:목업](http://www.dt.co.kr/contents.html?article_no=2007090302012269718002)   
> [요즘IT:와이프레이밍, 목업, 프로토타이핑 뭐가 다른건가요?](https://yozm.wishket.com/magazine/detail/1306/)   
> [위키백과:Routing](https://www.google.com/search?q=routing+%EC%9C%84%ED%82%A4&sxsrf=ALiCzsZmVMU9gSgCeT5BSiHm4mS3xGRJGA%3A1664413535880&ei=X-80Y-agNc-12roPzqysWA&ved=0ahUKEwimzMLM57j6AhXPmlYBHU4WCwsQ4dUDCA4&uact=5&oq=routing+%EC%9C%84%ED%82%A4&gs_lp=Egdnd3Mtd2l6uAED-AEBMgUQIRigATIFECEYoAHCAgoQABhHGNYEGLADwgIEECMYJ8ICBBAAGBPCAgUQABiABMICChAAGIAEGIcCGBSQBgpIkSRQ6wtYzCJwBXgAyAEAkAEAmAHFAaABgQmqAQMxLjniAwQgQRgA4gMEIEYYAIgGAQ&sclient=gws-wiz)   
> [나무위키:Router](https://namu.wiki/w/%EB%9D%BC%EC%9A%B0%ED%84%B0)   
> [React Router:main](https://reactrouter.com/en/main)   
> [React Router:useNagative](https://reactrouter.com/en/main/hooks/use-navigate)