---
layout: post
title: "React Client Ajax 2"
date: 2022-10-11
categories:
- JavaScript
tags:
- JavaScript
- React
- Effect Hook
- Side Effect
- fetch
- Pure Function
- useEffect
- dependency array
- Loading Indicator
---

React문서를 봐야되는데 엉덩이만 무거웠지 나는 왜이리 집중하지 못하는가

# Client side Ajax 2

## Side Effect

부수효과, 함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우 해당 함수는 Side Effect가 있다고한다.

React에서는 컴포넌트 내에서 fetch를 사용해 API 정보를 가져오거나, 이벤트를 활용해 DOM을 직접 조작할 떄 Side Effect가 발생했다고 한다.

```javascript
let gloval = 'window';

const setLocal = () => {
  gloval = 'local';
} 

setLocal();//Side Effect를 발생시킴
```

### Pure Function

순수함수, 함수의 입력만이 함수의 결과에 영향을 주는 함수이다. 순수 함수는 입력으로 전달된 값을 수정하지 않는다.

1. 네트워크 요청과 같은 Side Effect가 없다.
2. 어떤 전달 인자가 주어질 경우 항상 같은 값이 리턴되는걸 보장하는 예측가능한 함수이다.

```javascript
const immutablePureFunction = someVal => {
  return someVal.someKindOfImmutableFunction();
}

immutablePureFunction(someValue); // immutable한 값을 반환, Math.random은 난수를 생생하기에 예측 불가
```

-> fetch API를 사용한 AJAX 요청도 순수함수가 아니다. -> 예측불가능해서인가

### React의 함수 컴포넌트

```javascript
//input은 props, output은 JSX Element
//Side Effect 없고, 순수함수로 작동
const LinkElement = ({props}) =>{
  return (
    <li id={props.id}>
      <a herf={props.linkPath}>{props.linkName}</a>
    </li>
  )
}
```

상위의 코드와 달리, `fetch API`를 사용한 AJAX 요청이나, `LocalStorage` 또는 `setTimeout`와 같은 React와 관련없는 API를 사용하는 경우에 Side Effect가 발생하고, Side Effect를 위한 Effect Hook을 React에서는 제공한다.

## Effect Hook

### useEffect

컴포넌트 내에 Side Effect를 실행할 수 있게하는 Hook이다.

### API

useEffect(someFunction)

### 실행 시점

|---|---|---|
|컴포넌트 생성|새 props|state 변경|
|↓|↓|↓|
|||Render|
|||↓|
|||useEffect|

- 컴포넌트 생성 후 처음 화면에 렌더링(표시)
- 컴포넌트에 새로운 props가 전달되며 렌더링
- 컴포넌트에 state가 바뀌며 렌더링

컴포넌트가 렌더링 될떄마다 Effect Hook이 실행된다.

> 주의사항
>
> - 최상위에서만 Hook 호출
> - React 함수 내에서 Hook을 호출

## 조건부 effect 발생(dependency array)

useEffect의 두번째 인자는 배열이다. 이 배열은 조건을 담고 있다. boolean형태의 표현식이 아닌, 어떤 값의 변경이 일어날때를 의미한다. 해당 배열에는 어떤 값의 목록이 들어간다. 이 배열은 특별히 종속성 배열이라 부른다.

```javascript
// 두번째 인자에 빈배열(init: 단 한번만 외부 API를 통해 리소스를 받아올때)
useEffect(() => {
  //처음 생성될 때만 함수 실행
}, []);

//기본형태
useEffect(() => {
  //처음 생성, props 업데이트, state 업데이트 시 실행
});

useEffect(() => {
  // dep가 업데이트 될때마다 실행.
}, [dep]);
```

## 컴포넌트 내외별 호출 차이

|---|---|---|
|-|장점|단점|
|내부에서 처리|HTTP 요청 빈도 줄임|클라이언트 메모리에 많은 데이터로 부담 늘어남|
|외부에서 처리|클라이언트는 구현생각안함|빈번한 HTTP요청으로 서버 부담 증가|

출처: codestates
- [내부에서 처리](https://codesandbox.io/s/filter-by-client-vyzdc?from-embed)
- [외부에서 처리](https://codesandbox.io/s/useeffect-2-oute9?from-embed)

### AJAX 요청

```javascript
useEffect(() => {
  fetch(`http://server-path/endpoint?query=${value}`)
    .then(resp => resp.json())
    .then(result => {
      setValue(result);
    });
}, [value])
```

### Loading Indicator

네트워크 요청이 느릴 경우를 고려해 Loading Indicator는 구현해야한다.

```javascript
const [isLoading, setIsLoading] = useState(true);

//Loading Indicator 구현부 ex) style className visibility none

return {isLoading ? <LoadingIndicator/> : <div>{after rendering}</div>};

...

//fetch 요청 전후에 ux를 위한 setIsLoading 구현
useEffect(() => {
  setIsLoading(true);
  fetch(...)
    .then(...)
    ...
    .then(result => {
      setValue(value);
      setIsLoading(false);
    }, [value]);
})
```

> Effect Hook을 사용하지 않고 (fetch를 통한) 네트워크 요청 시 페이지가 멈추거나, 플리커링발생할 수 있다.

---

> ## 참조
>
> [Velog: Jake Seo/자바스크립트 개발자라면 알아야할 33가지 개념 20/순수 함수](https://velog.io/@jakeseo_me/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%9D%BC%EB%A9%B4-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A0-33%EA%B0%80%EC%A7%80-%EA%B0%9C%EB%85%90-20-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%88%9C%EC%88%98%ED%95%A8%EC%88%98)