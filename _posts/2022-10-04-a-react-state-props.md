---
layout: post
title: "JavaScript React State & Props"
date: 2022-10-04
categories:
- JavaScript
tags:
- JavaScript
- React
- JSX
- State
- Props
- 
---



# React State & Props

## State

- 컴포넌트의 사용 중 컴포넌트 내부에서 변할 수 있는 값
- 내부에서 변화하는 값

## Props

- 외부로부터 전달받은 값
- 컴포넌트의 속성(property)을 의미
- 부모(상위)컴포넌트로부터 전달받은 값
  - React컴포넌트는 JS function, class로 props를 함수의 arguments처럼 전달 받아 React element를 반환.
- 객체의 형태
- 읽기 전용

> props이 읽기전용이 아니면 직접 수정할 수 있게되고, 직접 수정하게되면 side effect발생. React is all about one-way data flow down the component hierarchy(단방향, 하향식 데이터 흐름 원칙) 위배.

## usage

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

## State hook & useState

```javascript
//React로부터 useState 불러옴
import { useState } from "react";

const CheckBox = () => {
    //컴포넌
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


> ## 참조  
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   
> []()   