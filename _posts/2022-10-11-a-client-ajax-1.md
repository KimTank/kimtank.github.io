---
layout: post
title: "React Client Ajax 1"
date: 2022-10-11
categories:
- React
tags:
- JavaScript
- React
- Client
- Ajax
- Effect Hook
- Data flow
- state
- Bottom up
- Top down
- Tree structure
- One way data flow
- props
- Lifting state up
---

월요병이 심하지만 오늘은 화요일이다. 4일뒤면 파주 통일전망대 자전거타고 룰루라랄할수있다. 룰루라랄!!!!!

---

## React Data Flow

React의 개발은 컴포넌트 단위로 작은 단위에서부터 Bottom-up, 상향식으로 큰단위로 앱을 만든다. 이는 테스트가 용이하고, 재사용이 쉽다. 개발자는 PM, UX designer에게 화면을 전달 받으면, 이를 hierarchy(계층구조)로 나누는 것을 가장 우선해야한다.

1. hierarchy(계층구조)화 하며 지켜야할 원칙은 "단일 책임 원칙"이다. "하나의 컴포넌트는 한가지 일"만 한다.
2. Tree Structure
3. 컴포넌트 밖에서 props을 통해 데이터를 arguments나 attributes처럼 전달한다. -> 부모 > 자식 > 자식의 자식 ...과 같은 Top-down의 Data flow를 갖는다. 이를, "단 방향 데이터 흐름(One-way data flow)"라 한다. 이것은 React를 대표하는 설명 중 하나다. 컴포넌트는 전달받은 데이터가 어디서 왔는지 전혀 모른다.
4. Application에 필요한 데이터를 변하는 값과 변하지 않는 값으로 나눈다.
   1. 변하는 값: 사용자 입력 event -> state
      - state는 최소화하는 것이 좋다.
   2. 변하지 않는 값: 정적인 값
      - 부모로부터 props를 통한 전달 X
      - 시간이 지나도 정적
      - 컴포넌트안 다른 state나 props 가지고 계산 X
5. state 위치 정하기
   - state가 특정 컴포넌트에서 유의미한게 아니라 여러개에서 영향을 받는다면, 공통 소유 컴포넌트를 찾아 그곳에 state를 위치해야한다.
   - n개의 자식위에 공통 소유 컴포넌트(부모 컴포넌트)에서 state를 위치해야한다.
6. 역방향 데이터 흐름 추가
   - state의 위치를 정한 후 부모 컨포넌트의 state가 하위 컴포넌트의 state가 하위 컴포넌트에 의해 변한다. -> 하위 컴포넌트의 이벤트로 부모의 상태를 변화시켜야한다.
7. **Lifting State Up: State 끌어 올리기(역방향 데이터 흐름), state를 변경시키는 function(handler)를 하위 컴포넌트에 props로 전달해서 해결**한다. -> callback function과 비슷

## Lifting state up(State 끌어 올리기)

One way data flow(단방향 데이터 흐름) 원칙에 따라 상위 컴포넌트는 전달받은 argument, attribute가 무엇인지 알 수 없다.

하위 컴포넌트에서 어떤 이벤트로 인해 상위 컴포넌트 state가 바뀌는 것을 "역방향 데이터 흐름"으로 원칙을 어기는 것으로 보인다. React가 제시하는 해결책은

> 상위 컴포넌트의 state를 변경하는 fuction 그 자체를 하위 컴포넌트로 전달하고, 이 function을 하위 컴포넌트가 실행한다.

상기 방식으로 One way data flow의 원칙을 위배하지 않는 해결이 가능하다.

```javascript
import React, { useState } from "react";

export default function ParentComponent() {
  const [value, setValue] = useState("날 바꿔줘!");

  const handleChangeValue = (someValue) => {
    setValue(someValue);
  };

  // 1. 하위 컴포넌트가 버튼 클릭 이벤트에따라 상태를 변경함.
  const handleButtonClick = () => {

  };

  return (
    <div>
      <div>값은 {value} 입니다</div>
      <ChildComponent handleButtonClick={handleButtonClick}/>
    </div>
  );
}

function ChildComponent({handleButtonClick}) {
  const handleClick = () => {
    // 이 버튼을 눌러서 부모의 상태를 바꿀 순 없을까?
    // 2. ParentComponent에서 handleButtonClick 전달
    handleButtonClick("전달할 어떤 값");
  };

  return <button onClick={handleClick}>값 변경</button>;
}
```

---

> ## 참조
>
> [React:JS Hello World](https://ko.reactjs.org/docs/hello-world.html)   
> [React:JS lifting-state-up](https://ko.reactjs.org/docs/lifting-state-up.html)