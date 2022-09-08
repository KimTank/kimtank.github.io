---
layout: post
title: "JavaScript Chrome Console"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- Chrome
- Console
- Inspect
- alert
- prompt
---

Chrome 브라우저의 검사 기능의 콘솔을 이용하여 가장 간단하게 코드를 작동시킬 수 있다. Java의 콘솔기능을 사용하기 위해서는 runCode를 해야하지만 브라우저에서 바로실행할 수 있어 매우 편하다. Android의 경우에도 실행할 가상머신이나, 디버깅용 스마트폰을 이용해 계속 빌드해서 올려야 확인할 수 있는데, 이에 비해 브라우저의 Console은 정말 이루 말할 것이 없다.

# JavaScript Chrome Console

## Running Code in The Console

- 각 os마다 지정된 단축키가 존재하니 확인하고 이용하면 편하다.
- 계속 상주하며 돌아가며 실행되니 단편적이지 않고, 간단한 코드 테스트시 유용하다.
- 창을 분리시켜 사용할 수 있다.
- 콘솔 내용 지우기 clear();, 단축키 ctrl + L(윈도우), cmd + k(mac)

## Console

다른 언어들에서는 print()로 사용하는 console.log();

파라메터를 출력한다.

- .log(): print와 같은 역할을한다. Java에서 .println();을 하는것처럼 엔터효과(`<br>`, `\n`)가 있다.
- .error(): 에러를 던질 수 있다.

## Alert

alert(params); => params에 담긴 내용을 경고창처럼 띄워줄 수 있다. android Toast객체나 SnackBar객체와 비슷한 효과.

## Prompt

prompt(param); => 입력창이 담긴 prompt를 띄울 수 있다. 입력한 정보를 변수에 저장할 수도 있다.

## html connect js

html파일과 js파일은 이름만 같다고해서 동작하지 않는다. 우리는 명시적으로 html파일에 `<script>`태그를 이용하여 연결(정확하게 연결이라는 표현이 맞는지는??)해줘야한다.

```html
//our.html
<!DOCTYPE html>
<html>
    <head>
        ...
        <script src="our.js"></script> 
        <!-- 일반적으로 head에 위치하지는 않는다. -->
    </head>
    <body>
        ...
        <!-- TODO 여기가 좋음. lifeCycle처럼 화면이 뜨고난 뒤 제어하기 때문일거라 예상-->
    </body>
</html>
```

```javascript
let someCodeHere = prompt('input what you want');

console.log(someCodeHere);

alert('i want your js file throws error');

console.error('Happppyyyyy :D');

console.log('this letter started by France..');
//내가 당신이 받을 행운의 편지를 에러를 던져 막아주었다 :D
```

> ## 참조
> [Chrome:Developer/Devtools/Console](https://developer.chrome.com/docs/devtools/console/)   
> [MDN:WebAPI/console](https://developer.mozilla.org/ko/docs/Web/API/console)   
> [MDN:WebAPI/Window/alert](https://developer.mozilla.org/ko/docs/Web/API/Window/alert)   
> [MDN:WebAPI/Window/prompt](https://developer.mozilla.org/ko/docs/Web/API/Window/prompt)