---
layout: post
title: "JavaScript textContent & innerText, innerHTML 차이"
date: 2022-09-14
categories:
  - JavaScript
tags:
  - JavaScript
  - DOM
  - Node
  - textContent
  - HTMLElement
  - innerHTML
  - Element
  - innerText
---

DOM은 생각보다는 분량이 방대하다. 굉장히 유용하게 쓰일 수 있는 정보들이 많기에 과제가 생각보다 빨리 끝나게되어 다른 중요할거 같은 개념을 추가로 본다.

# JavaScript textContent & innerText, innerHTML 차이

## Node.textContent

Node interface의 property로 node와 node의 children에 textContent

## Element.innerHTML

Element property로 요소 내 포함된 HTML 또는 XML 마크업을 가져오거나 설정한다.

## HTMLElement.innerText

HTMLElement interface의 property로 element와 element의 children의 렌더링된 textContent

## textContent vs innerText 차이

- textContent와 innerText는 text의 렌더링 중이 아니라면 값(string||null)이 똑같지만, text의 렌더링이 끝나기 전에는 innerText는 인식할 수 없다.
- textContent는 `<script>`, `<style>`요소를 포함한 모든 요소의 콘텐츠 가져오지만, innerText는 '사람이 읽을 수 있는 요소'만 처리한다.
- textContent는 노드의 모든 요소를 반환하지만, innerText는 스타일링을 고려하여 '숨겨진 요소'의 텍스트는 반환하지 않는다.
  - innerText는 CSS 스타일링을 고려하여 대화형 사이트에서 업데이트 한 후와 같이 browser가 웹 페이지의 일부 또는 전부를 다시 처리하고 그려야할 때 리플로우가 발생 => 리플로우의 계산은 비싸기떄문에 가능하면 피하세요.
- IE기준 innerText를 수정하면 요소의 모든 자식 노드를 제거하고, 모든 자손 텍스트를 영구히 파괴한다. 이후 해당 텍스트 노드를 다른 노드는 물론 같은 노드에 삽입하는 것도 불가능하다. => 예상치못한 에러발생으로 브라우저 호환성에 크리티털 이슈

## 예제

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="robots" content="noindex, nofollow" />
    <style>
      body {
        padding: 0;
        margin: 0;
      }

      svg:not(:root) {
        display: block;
      }

      .playable-code {
        background-color: #f4f7f8;
        border: none;
        border-left: 6px solid #558abb;
        border-width: medium medium medium 6px;
        color: #4d4e53;
        height: 100px;
        width: 90%;
        padding: 10px 10px 0;
      }

      .playable-canvas {
        border: 1px solid #4d4e53;
        border-radius: 2px;
      }

      .playable-buttons {
        text-align: right;
        width: 90%;
        padding: 5px 10px 5px 26px;
      }
    </style>

    <title>HTMLElement.innerText - 예제 - code sample</title>
  </head>
  <body>
    <!-- 원본 -->
    <h3>원본 요소:</h3>
    <p id="source">
      <style>
        #source {
          color: red;
        }
      </style>
      아래에서<br />이 글을<br />어떻게 인식하는지 살펴보세요.
      <span style="display:none">숨겨진 글</span>
    </p>

    <!-- textContent -->
    <h3>textContent 결과:</h3>
    <textarea id="textContentOutput" rows="6" cols="30" readonly>...</textarea>

    <!-- innerText -->
    <h3>innerText 결과:</h3>
    <textarea id="innerTextOutput" rows="6" cols="30" readonly>...</textarea>

    <script>
      //원본 글이 담김 <p>태그
      const source = document.getElementById("source");

      //textContent textarea
      const textContentOutput = document.getElementById("textContentOutput");

      //innerText textarea
      const innerTextOutput = document.getElementById("innerTextOutput");

      textContentOutput.innerHTML = source.textContent;
      innerTextOutput.innerHTML = source.innerText;
    </script>
  </body>
</html>
```

![출처:MDN](/assets/img/220914-tc-it-diffrence.png)

## textContent vs innerHTML

Element.innerHTML은 HTML을 반환한다. 그래서 성능적으로는 textContent가 낫다. 그리고 textContent는 XSS공격(cross site scripting)의 위험이 없다.

> ## 참조
> [MDN:WebAPI/Node/textContent](https://developer.mozilla.org/ko/docs/Web/API/Node/textContent)  
> [MDN:WebAPI/HTMLElement/innerText](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement/innerText)  
> [MDN:WebAPI/Element/innerHTML](https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML)  
> [MDN:Doctype](https://developer.mozilla.org/ko/docs/Glossary/Doctype)  
> [MDN:Reflow](https://developer.mozilla.org/ko/docs/Glossary/Reflow)  
> [Google:browser reflow](https://developers.google.com/speed/docs/insights/browser-reflow)  
> [MDN:Cross site scripting](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)
