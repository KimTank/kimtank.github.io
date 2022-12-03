---
layout: post
title: "Redux 예제"
date: 2022-11-03
categories:
  - React
tags:
  - React
  - Redux
  - 예제
  - codestates
---

본과제를 가지고는 하기 규모가 있어, 예제를 가지고 하려고 본과제를 참고하며 구조화를 시도했지만 계속적으로 reducer를 undefined한다. 그냥 주석으로 처리하고 해당문제의 경우는 조금 더 연구가 필요하다.

## 1. package.json

```json
{
  "name": "react",
  "version": "0.0.0",
  "private": true,
  "dependencies": {
    "@types/react": "^16.8 || ^17.0 || ^18.0",
    "@types/react-dom": "^16.8 || ^17.0 || ^18.0",
    "react": "^18.1.0",
    "react-dom": "^18.1.0",
    // ??? react native도 자동으로 잡히나
    "react-native": ">=0.59",
    // react-redux
    "react-redux": "^8.0.2",
    // react
    "redux": "^4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  },
  "devDependencies": {
    "react-scripts": "latest"
  }
}
```

## 2. index.js

```javascript
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./App";
//Provider
import { Provider } from "react-redux";
//createStore -> 버전관련해 문제있어 legacy_createStore를 사용
import { legacy_createStore as createStore } from "redux";

const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

export const PLUS = "INCREASE";
export const MINUS = "DECREASE";
export const SET_INIT = "SET_INIT";
export const INIT_VAL = 0;

//action.js
export const increase = () => {
  return {
    type: PLUS,
  };
};

export const decrease = () => {
  return {
    type: MINUS,
  };
};

export const initialized = () => {
  return {
    type: SET_INIT,
  };
};

// reducer.js
// Reducer 생성 시 초기화 필수
const counterReducer = (state = INIT_VAL, action) => {
  // Action 객체의 type 값에 따라 분기하는 switch 조건문입니다.
  switch (action.type) {
    //action === 'INCREASE'일 경우
    case PLUS:
      return state + 1;

    // action === 'DECREASE'일 경우
    case MINUS:
      return state - 1;

    // action === 'SET_NUMBER'일 경우
    case SET_INIT:
      return state - state;

    // 해당 되는 경우가 없을 땐 기존 상태를 그대로 리턴
    default:
      return state;
  }
  // Reducer가 리턴하는 값이 새로운 상태가 됩니다.
};

const store = createStore(counterReducer);

// index
root.render(
  // 공급자에 상태 저장소 연결
  <Provider store={store}>
    <App />
  </Provider>
);
```

## 3. App.js

```javascript
import React from "react";
import "./style.css";
// react-redux 내 useDispatch, useSelector
import { useDispatch, useSelector } from "react-redux";
import { increase, decrease } from "./index.js";

export default function App() {
  //action 전달하는 dispatch 생성
  const dispatch = useDispatch();
  //useSelector로 상태 전달
  const state = useSelector((state) => state);

  //action.js
  //action creator
  const plusNum = () => {
    dispatch(increase());
  };

  const minusNum = () => {
    dispatch(decrease());
  };

  return (
    <div className="container">
      {/* 4 */}
      <h1>{`Count: ${state}`}</h1>
      <div>
        <button className="plusBtn" onClick={plusNum}>
          +
        </button>
        <button className="minusBtn" onClick={minusNum}>
          -
        </button>
      </div>
    </div>
  );
}
```

---

대충 구조는 이렇다. redux가 있음으로해서 불필요한 리렌더링이나 비효율적인 방법으로 값을 주고넘기는 사태는 줄어든다. 계속 사용해봐야 손에 익지 싶다.

---

## 참조

> [Redux: main](https://redux.js.org/)  
> [React-Redux: main](https://react-redux.js.org/)  
> [robinwieruch: Redux](https://www.robinwieruch.de/react-redux-tutorial)  
> [facebook: flux](https://facebook.github.io/flux/docs/in-depth-overview)
