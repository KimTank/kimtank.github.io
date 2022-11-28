---
layout: post
title: "JavaScript React State & Props"
date: 2022-10-04
categories:
- React
tags:
- JavaScript
- React
- JSX
- State
- Props
- Controlled Component
- One-way Data Flow
---

미루고 미루던 state, prop에 대해 이제사 적는다. 시간은 한정적이다. 잠좀 그만잡시다 T^T

---

## 1. State

- 컴포넌트의 사용 중 컴포넌트 내부에서 변할 수 있는 값
- 내부에서 변화하는 값

## 2. Props

- 외부로부터 전달받은 값
- 컴포넌트의 속성(property)을 의미
- 부모(상위)컴포넌트로부터 전달받은 값
  - React컴포넌트는 JS function, class로 props를 함수의 arguments처럼 전달 받아 React element를 반환.
- 객체의 형태
- 읽기 전용

> props이 읽기전용이 아니면 직접 수정할 수 있게되고, 직접 수정하게되면 side effect발생. React is all about one-way data flow down the component hierarchy(단방향, 하향식 데이터 흐름 원칙) 위배.

## 3. usage

1. 하위 컴포넌트에 전달하고자 하는 data와 property를 정의한다.
2. props를 이용하여 정의된 value와 property를 전달한다.
3. 전달받은 props를 렌더링한다.

```javascript
const Parent = () => {
    const content = '뷰';
    return (
        <div className='parent'>
            <h1>부모뷰</h1>
            <Child header={"자식"} content={content}>
                내용
            </Child>
        </div>
    );
};

const Child = (props) => {
    console.log(props);
    // {header: "자식", content: "뷰"}
    return (
        <div className='child'>
            <h2>{props.header + props.content}</h2>
            <h3>{props.children}</h3>
        </div>
    );
};
```

## 4. State hook & useState

```javascript
//React로부터 useState 불러옴
import { useState } from "react";

const CheckBox = () => {
    //배열의 0번째 요소는 state변수, 
    //1번째 이 변수를 갱신할 수 있는 함수
    //useState인자는 state 초기값
    const [isChecked, setIsChecked] = useState(false);

    const handleChecked = (event) => {
        setIsChecked(event.target.checked);
    };
    return (
        <div className="App">
            <input type="checkbox" checked={isChecked} onChange={handleChecked}/>
            <span>{isChecked ? "true" : "false"}</span>
        </div>
    );
};

export default CheckBox;
```

## 5. React Event handling

DOM의 이벤트 처리방식과 유사하나, 문법 차이가 있다.

- 소문자대신 camelCase사용
- JSX를 사용하여 문자열이 아닌 이벤트 handler, 함수를 전달한다.

### 5.1. onChange

input, textarea select와 같은 form element는 유저 입력값을 제어할 때 사용된다. React의 state는 이런 변경할 수 있는 입력값을 관리한다. onChange 이벤트 발생 시 event.target.value를 통해 객체의 input값을 읽어온다.

```javascript
const Title = () => {
    const [title, setTitle] = useState('');

    const handleTitleChange = (event) => {
        setTitle(event.target.value);
    }

    return (
        <div>
            <input type="text" value={title} onChange={handleTitleChange} />
            <h1>{title}</h1>
        </div>
    );
};
```

### 5.2. onClick

a tag와 같이 링크 이동과 같은 클릭에 대한 상호작용 시 사용하는 이벤트이다.

```javascript
const AlertAction = (props) => {
    // # 방법2. 함수로 만들어 전달
    const handleAlertAcition = (event) => {
        alert(props.value)
    };

    return (
        <div>
            // 동작안함. -> 컴포넌트가 실행될때 alert가 실행됨.
            // <button onClick={alert(props.value)}>{props.buttonName}</button>

            // # 방법1. 함수로 만들어야 누를때마다 실행된다.
            <button onClick={(evnent) => alert(props.value)}>
                {props.buttonName}
            </button>

            // # 방법2. 함수를 전달
            <button onClick={handleAlertAcition}>
                {props.buttonName}
            </button>
        </div>
    );
};
```

### 5.3. togglePopup

```javascript
import React, { useState } from "react";
import "./styles.css";

const App = () => {
    const [showPopup, setShowPopup] = useState(false);

    const togglePopup = () => {
        setShowPopup(!showPopup)
    };
    
    return (
        <div className="App">
            <h1>Fix me to open Pop Up</h1>
            {/* 버튼을 클릭했을 때 Pop up 의 open/close 가 작동하도록 button tag를 완성하세요. */}
            <button className="open" onClick={togglePopup}>Open me</button>
            {showPopup ? (
                <div className="popup">
                    <div className="popup_inner">
                        <h2>Success!</h2>
                        <button className="close" onClick={togglePopup}>
                            Close me
                        </button>
                    </div>
                </div>
            ) : null}
        </div>
    );
};

export default App;
```

## 6. Controlled Component

React에서는 Data로 state를 따로 관리하고 싶어한다. **"React가 State를 Control할 수 있는 Component를 Controlled Component"**라고 한다. -> 추가적으로 React에 대해서는 학습이 필요하다.

## 7. React Data Flow

React로 앱을 설계할 시 Component 기준으로 Bottom-up으로 구현하면 테스트가 쉽고, 확장성이 좋다. 하여 설계 시 기획자, PM, UX 디자이너는 Component Hierarchy(계층구조)로 나눈다.

허나 Data의 경우는 다르다. Parent Component로 부터 시작하여 Child Component로 props를 통하여 Top-down방식으로 구현한다.

Data 전달의 원칙인 One-way Data Flow는 React가 갖는 중요한 원칙이다. Component는 props를 통해 전달받은 Data가 어디서(Where data from)온것인지 모른다.

## 참조

> [React with Hooks:forms](https://reactwithhooks.netlify.app/docs/forms.html)   
> [React:Main](https://ko.reactjs.org/)