---
layout: post
title: "DOM DocumentFragment"
date: 2022-09-14
categories:
  - DOM
tags:
  - DOM
  - DocumentFragment
---

DOM은 생각보다는 분량이 방대하다. 굉장히 유용하게 쓰일 수 있는 정보들이 많기에 과제가 생각보다 빨리 끝나게되어 다른 중요할거 같은 개념을 추가로 본다.

# DOM DocumentFragment

## DocumentFragment

아주 작고 부모를 갖지않는 문서객체이다. 일반 document처럼 문서 구조를 저장할 수 있어 document의 가벼운 버전으로 사용한다. document와는 달리 활성화된 문서 트리구조의 일부가 아니기 때문에 내부트리를 변경해도 문서나 성능에 아무영향도 주지 않으며 **리플로우도 방지할 수 있다.**

EventTarget <== Node <== DocumentFragment

## Constructor

DocumentFragment(): 새로운 객체를 생성하여 반환한다.

```javascript
new DocumentFragment();
```

## Property

- .childElementCount: **Read Only(이후 R-O)**, 자식 Element의 수(number)를 반환한다.
- .children: **R-O**, 현재 상태 요소의 HTMLCollection(argument같은 유사배열)을 반환한다.
- .firstElementChild: **R-O**, 첫번째 자식 요소를 반환한다. 없으면 null을 반환한다.
- .lastElementChild: **R-O**, 마지막 자식 요소를 반환한다. 없으면 null을 반환한다.

## Method

부모인 Node의 메서드를 상속한다.

- .append(): 마지막 자식 뒤에 Node 객체들이나 문자열 객체들을 추가한다.
- .prepend(): 첫번째 자식 앞에 Node 객체들이나 문자열 객체들을 추가한다.
- .querySelector(): 주어진 선택자와 일치하는 첫번째 요소 노드를 반환한다.
- .querySelectorAll(): 주어진 선택자와 일치하는 모든 요소의 노드를 포한한 NodeList를 반환한다.
- .replaceChildren(): 자식 하나를 일련의 새로운 자식으로 대체한다.
- ~~.getElementById()~~: ~~링크가 끊어져있어 deprecate된것으로 예상~~, 주어진 ID와 일치하는 첫번째 요소 노드를 반환한다. 기능적으론 Document.getElementById()와 동일하다.

## Usage Note

DocumentFragment의 일반적 용도는 그안에 DOM 하위트리를 만들어 Node 인터페이스의 appendChild()나 insertBefore()과 같은 메서드로 DOM 하위트리를 삽입하는것이다. 이 방법은 노드들이 모두 DOM으로 이동하고 빈 DocumentFragment만 남게된다. 이때 모든 노드가 한번에 document에 삽입되었기 때문에 reflow도 한번만 발생한다. 하지만 노드를 DocumentFragment를 사용하지 않고, 각각 하나씩 삽입했다면, 매 삽입시마다 reflow가 발생한다.

Web Component에서도 유용하다. 예를들어 `<template>`요소의 HTMLTemplateElement.content속성이 DocumentFragment이다.

document.createDocumentFragment() 메서드나 DocumentFragment() 생성자를 사용해 만들 수 있다.

## Example

```html
<ul id="list"></ul>
```

```javascript
const list = document.querySelector('#list');
const brands = ['Masi', 'Fuji', 'Derosa', 'Specialized'];

const fragment = new DocumentFragment();

brands.forEach((brand) => {
  const li = document.createElement('li');
  li.textContent = brand;
  fragment.appendChild(li);
})

list.appendChild(fragment);
```

> ## 참조
> [MDN:WebAPI/HTMLCollection](https://developer.mozilla.org/ko/docs/Web/API/HTMLCollection)   
> [MDN:WebAPI/Node](https://developer.mozilla.org/ko/docs/Web/API/Node)   
> [MDN:WebAPI/NodeList](https://developer.mozilla.org/ko/docs/Web/API/NodeList)   
> [MDN:Element/template](https://developer.mozilla.org/ko/docs/Web/HTML/Element/template)   
> [MDN:WebAPI/DocumentFragment](https://developer.mozilla.org/ko/docs/Web/API/DocumentFragment)
