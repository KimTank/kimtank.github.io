---
layout: post
title: "Codestates Agora Toy Project"
date: 2022-09-15
categories:
- Codestates
tags:
- Web
- Project
- Codestates
---

사실 문서화를 할 생각이 없었지만 문서화가 필요한 내용들이 꽤나 있어서 문서를 만들면서 진행하기로 했다.

---

## 1. Component

컴포넌트는 정의하기 쉽지 않다. 디자이너나 PM에게는 **'하나의 역할을 하기 위해 모은 디자인 요소'**가 UI컴포넌트이고, Front-End Developer에게는 **'하나의 기능 구현을 위한 여러 종류의 코드 묶음'**이기 떄문이다. 코드스테이츠의 강의를 제작한 제작자는 컴포넌트를 **'하나의 역할을 하기 위해 모인 무언가의 집합'**이라고 정의한다.

## 2. Agorastates

아고라스테이츠는 코드스테이츠의 github저장소로 reddit이나 stackoverflow같은 커뮤니티와 비슷하게 질문과 답변을 github를 통해서 이루어지도록(천잰가) 만들어 놓았다.

github의 commit내역 히스토리를 보면 **CRUD**가 일어나고있는 기능이 결국 이번과제의 **핵심 목표**라고 볼 수 있다.

## 3. So What is Component?

그래서 컴포넌트는 github를 둘러쌓고있는 container, 각 태그(div라든가 ul, li 등등)들의 경계를 기점으로 각각의 요소들의 박스를 컨테이너라 한다. 시각적으로 확인하기 위한 도구로는 chrome console elements탭을 이용해 각 태그를 클릭하면 해당하는 컴포넌트가 선택되는걸 확인할 수 있다.

## 4. Dummy Data Structure

```javascript
 {
    id: "",
    createdAt: "2022-05-16T01:02:17Z",
    title: "",
    url: "",
    author: "",
    answer: { //배열로 만들면 답변이 여러개겠네?
      id: "",
      createdAt: "2022-05-16T02:09:52Z",
      url: "",
      author: "",
      bodyHTML: "내용이 태그였다니!!!"
      avatarUrl: "",
    },
    bodyHTML:"내용이 태그의 집합이였다니!!!",
    avatarUrl:
      "이걸어떻게 랜덤으로 한거야", //이건 왜안지웠지
  },
  ...
```

더미 데이터의 구조는 이렇게 생겼다

## 5. HTML Structure

```html
<li class="discussion__conatiner">
	<div class="discussion__avatar--wrapper">
		<img class="discussion__avatar--image"
			src="https://v=4"
			alt="avatar of kimploo">
  </div>
  <div class="discussion__content">
    <h2 class="discussion__title"><a href="https://github.com/6">[notice] 좋은 질문하는 법</a></h3>
		<div class="discussion__information">kimploo / 2022-04-22T14:08:33Z</div>
  </div>
  <div class="discussion__answered">☑</div>
</li>
```

그대로 가져왔다. 문제시 자삭.

## 6. 데이터 시각화

HTML Structure의 구조를 시각화 해주는 고마운 [사이트](https://software.hixie.ch/utilities/js/live-dom-viewer/)

![출처: SW.Hixie.ch](/assets/img/220915-util-livedomviewer.png)

## 참조

> [Github:KimTank/깃연습저장소](https://github.com/KimTank/git-practice-fuzzy-potato)   
> [Github:KimTank/내아고라스테이츠만들기 포크떠왔어요](https://github.com/KimTank/fe-sprint-my-agora-states)
> [SW.Hixie:JS/Live DOM Viewer](https://software.hixie.ch/utilities/js/live-dom-viewer/)