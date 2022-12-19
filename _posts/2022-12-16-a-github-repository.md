---
layout: post
title: "github repository"
date: 2022-12-16
categories:
  - Network
tags:
  - Network
  - Github
  - Repository
  - readme.md
  - .gitignore
  - issue
  - milestone
  - pull request
  - project
  - 칸반
---

몰랐던 깃허브 원격저장소 readme 작성법

---

## 1. github repository file

### 1.1. readme.md

마크업으로 작성하는 readme.md, 이때까지는 그냥 있는파일이었는데, 실제로는 꼭 포함해야되는 정보가 있단다.

- project 이름
- 핵심 기능
- 팀원

가만 생각해보면, 대부분 사용법과 코드에 기여한사람, 그리고 도네를 기재했던거같다.

### 1.2. .gitignore

git으로 올리지 않는 파일에 대한 명세이다. 원격저장소는 공용인 경우가 많다. 이에 개인설정이나, 보안정보 등은 굳이 공유하지 않아도 된다. 거기에 대한 명세를 작성한다.

### 1.3. license

라이선스에 대한 부분은 github뿐 아니라 법적인 책임이 물렸을 때, 회사가 책임지지 않는 경우가 있으니, 상급자에게 물어본다거나 정확하게 알아보고 표기해야한다. 법적분쟁으로 갔을 시 가난에 접어들수있다.

### 1.4. usage

출처: [codestates](https://www.codestates.com/)

```markdown
# My Todo App

Todo 관리를 위한 웹 애플리케이션입니다.

## Features

- 편리한 UI로 Todo를 쉽게 생성하고 삭제할 수 있습니다.
- Todo에 기한과 카테고리를 설정할 수 있습니다.
- create-react-app으로 간편한 번들링과 배포가 가능합니다.
- Spring Boot로 쉽게 서버 배포를 할 수 있습니다.

## Contributors

- FE: 김코딩, 박해커
- BE: 나서버, 최디비

## Project Wiki

프로젝트 팀 정보, 기획, 아키텍쳐에 대한 자세한 안내입니다.
(링크)
```

## 2. github 기능

### 2.1. issue

PJ에 새로운 기능제안, 버그 제보, PJ의 이슈를 의미한다.

### 2.2. milestone

이정표, task card를 그룹화한다. issue인 task card가 종료 시 milestone 진행상황이 업데이트된다. 이슈 추적과 진행상황을 시각적으로 파악할 수 있다.

### 2.3. pull request

내코드를 git branch에 merge할 수 있는지 확인하는 요청이다. commit한 코드를 따로 선택하여 comment달 수 있다.

### 2.4. project

업무 관리기능, 칸반보드생성가능하다.

## 3. 칸반

팀과 조직이 작업을 시각화하고, 업무의 병목 현상과 리소스 낭비를 해결하는 업무 관리 방법

### 3.1. 보드를 통한 시각화

업무를 하나의 티켓으로 표현, 업무 단게를 하나의 열로 표현한다. 새로운 업무가 생기면 가장 왼쪽 열에 업무가 쌓이고, 업무가 잘 진행되면 가장 오른쪽으로 전달되 쌓인다.

출처: [codestates](https://www.codestates.com/)

| 백로그 | 할일  | 진행중 | 완료  |
| ------ | ----- | ------ | ----- |
| 업무a  | 업무b | 업무c  |       |
|        | 업무d |        | 업무0 |
|        |       |        |       |

work in progress, WIP로 진행중 업무 제한 및 흐름을 관리할 수 있다. WIP limit을 두어 해당열에 제한을 할 수 있다.

| 백로그 | 할일(wip:2) | 진행중(wip:2) | 완료  |
| ------ | ----------- | ------------- | ----- |
| 업무a  | 업무b       | 업무c         |       |
|        | 업무d       | (추가가능)    | 업무0 |
|        | (추가불가)  |               |       |
|        |             |               |       |

### 3.2. usage

- 업무 시각화
- 진행 중인 업무 제한
- 흐름 관리
- 명확한 프로세스 정책
- 피드백 루프 구현
- 협력적인 개선, 실험적인 발전

### 3.3. 원칙

칸반이 잘 이루어져있는가 중간중간 체킹

1. 하던 업무 칸반보드 올리기
2. 정진적 변화 추구
3. 직위 관계 없는 리더쉽

## 4. issue

- assigness: 해당 task 담당자
- label: 라벨링
- projects: PJ 지정
- mildstone: mildstone 지정

## 5. milestones

issue -> mildstones tab -> new mildstone

- title
- due date: 마감일

## 6. project

new project -> 햄버거버튼 -> settings

- manage access
  - base role: read로 변경
  - invite collaborators
- `#` 리파지토리 검색 후 선택
  - issue, PR선택, Add selected items버튼 눌러 모든 item 추가
- status
  - todo
  - in progress
  - done
  - 추가가능
- 상단tab collapse button -> group
  - assignees
  - status
  - milestone
  - repository
  - no grouping
- 상단tab collapse button -> Borad(칸반으로 보기)
- 완료 시 save changes

이슈 생성할 시 project 추가하면 자동으로 트래킹

> ## 참조
>
> [코드스테이츠](https://www.codestates.com)  
> [github: doc/issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)  
> [github: doc/mildstones](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/about-milestones)
