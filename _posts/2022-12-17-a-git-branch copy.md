---
layout: post
title: "git branch"
date: 2022-12-16
categories:
  - Git
tags:
  - Network
  - Git
---

github와 git은 다르다.

하지만 대부분의 초급은 같을거라 생각할거야(응 자기소개)

---

## 1. git branch

나뭇가지를 치는것과 비슷하게 곁두리로 쳐서 메인, 마스터 브랜치는 건들지 않고, 코드개발을 하게해준다.

### 1.1. 생성, 변경

git switch, git이 보는곳, HEAD를 변경하는 작업이다.

출처: [codestates](https://codestates.com)

```bash
# 변경
git switch -c ty
# git checkout -b ty

# 생성
git switch ty
git checkout main
```

### 1.2. 합체

merge, 합체 잘못합치면 개털린다

```bash
git commit -m "기능1"
git commit -m "기능1 오류수정"
git commit -m "기능2"

git checkout main
git merge ty
```

바로 합치면 큰일나므로(물론 crash난 곳을 수정해야하나, 나같은 초심자들은 보지도않고 local인지 remote인지 에라 모르겠다하다가 혼남) pull request요청하는것을 권장한다.

```bash
git commit -m "기능1"
git commit -m "기능1 오류수정"
git commit -m "기능2"

git push origin ty

# github일 시 pull request, 다른 원격저장소면 다른 방식
```

### 1.3. 삭제

git branch -d, 일이 끝났을 시 삭제, 이역시 잘못하면 merge가 된지 확인하지 않고, 혹은 pull request가 된지 확인하지 않고 올리면 지옥을 맛볼수있다.

```bash
# merge되지 않았을 시 삭제 안되게 막혀있음
git branch -d ty
# 그런거 모르겠고 강제삭제 -> 지옥에오신걸 환영해요
# git branch -D ty -> 
```

## 2. git usage

### 2.1. 설정

```bash
git config --global user.name 'ty'
git config --global user.name 'sycork@gmail.com'
git config --global core.editor 'vim'
```

### 2.2. help

```bash
git help -all
git [명령] -help
```

### 2.3. 세팅, 초기화

```bash
# 초기화
git init

# 복제
git clone [불러올 주소]
```

### 2.4. stage와 commit

```bash
# 확인
git status

# 파일 추가(stage)
git add [추가할파일]

# 추가한 파일 돌리기(언스테이징)
git reset [돌릴파일]

# 스테이징 되지않은 변경 사항보기
git diff

# 스테이지만 된(커밋안된) 변경사항
git diff --staged

# 스테이지된 컨텐츠를 메세지와 함께 커밋(스냅샷 생성)
git commit -m "설명할 메세지"
```

### 2.5. branch와 merge

진행중..............

---

> ## 참조
>
> [코드스테이츠](https://www.codestates.com)  
> [toastui: pull request code review](https://github.com/nhn/tui.editor/pull/2633)
