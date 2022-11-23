---
layout: post
title: "Chrome CodeBlock None Translate"
date: 2022-09-04
categories:
- JavaScript
tags:
- JavaScript
- Chrome
- CodeBlock
- Translate
---

크롬에서 번역기능을 사용하면 코드블럭 내 소스들까지 번역되버려 보기 힘든 경우가 종종 있어 생활코딩 egoing님이였나? 김포프님이였나 누군가 가르쳐준 방법(명령어를 북마크로 저장)을 가지고 있었으나, 영어공부한다고 생각하고 읽자고 했지만 당연히도 시간은 한정적이고 ^^ 내게는 아직 영어공부보다는 기본 문법과 언어 사용법이 우선이기에 다시 찾아보았다. 코드블럭 번역 안하는법 ㅋㅋㅋㅋ

```javascript
//한글 번역 적용시 코드블럭 내 코드가 번역되버린다 ㅜㅜ
함수 추가DoesOverflow(a, b){
    바 c = a + b;
    반환 !== cd || !== ca;
}

//적용 후 번역 안되는 원형의 모습
function additionDoesOverflow(a, b){
    var c = a + b;
    return a !== c-b || b !== c-a;
}
```

## notranslate class 추가

개발자 도구를 열고 콜솔창에 notranslate class를 추가하면 된다.

```javascript

document.querySelectorAll('pre, code').forEach(function(e){e.classList.add('notranslate');})
```

## 북마크로 만들어 버리자

우리는 개발자다. 개발자는 늘 효율적으로 시간을 줄이는 생산성을 고민하여야 한다.~~(좋게 말해서 그런거지 나는 사실 귀찮아서 고민한다)~~ 코드를 복사 붙여넣기 하는 것 역시 방법이지만, 북마크로 명령어를 지정하면 북마크를 누르고 번역을 누를 시 코드블럭은 번역이 되지 않는다^^

```javascript
javascript:document.querySelectorAll('pre, code').forEach(fuction(e){e.classList.add('notranslate');});
```

## 출처

> [HackTam:기술백서/Tools/크롬 소스부분은 번역 안되게 하기](https://hacktam.kr/etclec/153)