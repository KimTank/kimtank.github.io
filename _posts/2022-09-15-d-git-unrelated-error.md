---
layout: post
title: "Git error? fatal:refusing to merge unrelated histories"
date: 2022-09-15
categories:
- Git
tags:
- Git
- fatal-error
- refusing to merge unrelated histories
- educative.io
---

시킨대로안하면 에러가 발생한다 ^^ 늘 그렇지만 해결하면 즐겁다.~~(해결못하면 두통이..아앙ㅇ대)~~

---

관련없는 이력 병합을 거부하는 에러. 관련이 없는 두 프로젝트를 merge해야될때 발생한다. 서로를 모르고, 커밋 이력이 일치하지 않아서 발생한다.

![출처: https://www.educative.io](/assets/img/220915-git-merge.png)

## 1. Situation

- 프로젝트 복사하였고, .git 디렉토리가 삭제되거나 손상되어 git이 로컬기록을 인식하지 못해 원격 저장소로 푸시하거나 풀할때 발생한다.
- 새 저장소를 만들고 몇가지 커밋을 추가하였고, 이미 만들어져있는 원격저장소(자체적으로 커밋 이력이 따로 있음)에서 풀하려고 할때 git은 둘사이에 연결고리를 찾지못하여 오류를 던져준다.

> 이외의 상황도 있을 수 있다.

## 2. Solution

해당 오류는 allow-unrelated-histories 스위치를 토글하면 해결된다. `git pull||git merge` 태그를 추가하면 된다.

```bash
$git pull origin main --allow-unrelated-histories
```

## 3. For Real

```bash
ty@DTHOME:~/Workspace/cs/git-parctice$ git branch -M main
ty@DTHOME:~/Workspace/cs/git-parctice$ git status
On branch main
nothing to commit, working tree clean
ty@DTHOME:~/Workspace/cs/git-parctice$ git remote add origin git@github.com:KimTank/git-practice-fuzzy-potato.git 
ty@DTHOME:~/Workspace/cs/git-parctice$ git push -u origin main
# 이때부터 진땀..
To github.com:KimTank/git-practice-fuzzy-potato.git
! [rejected]
main -> main (fetch first)
error: failed to push some refs to 'git@github.com:KimTank/git-practice-fuzzy-potato.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
ty@DTHOME:~/Workspace/cs/git-parctice$ git pull
# 아아악
warning: no common commits
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 5.90 KiB | 5.90 MiB/s, done.
From github.com:KimTank/git-practice-fuzzy-potato
    * [new branch]main -> origin/main
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> main

# pull을 땡겼는데 뭐라뭐하니까 파일이 받아와졌는지 확인
ty@DTHOME:~/Workspace/cs/git-parctice$ ls
index.css  index.html
# 하라는대로 해보자
ty@DTHOME:~/Workspace/cs/git-parctice$ git branch --set-upstream-to=origin/<branch> main
-bash: branch: No such file or directory
# 브랜치를 지정하자
ty@DTHOME:~/Workspace/cs/git-parctice$ git branch --set-upstream-to=origin/origin main
# 오리진이 아니래 ㅜㅜ
error: the requested upstream branch 'origin/origin' does not exist
hint:
hint: If you are planning on basing your work on an upstream
hint: branch that already exists at the remote, you may need to
hint: run "git fetch" to retrieve it.
hint:
hint: If you are planning to push out a new local branch that
hint: will track its remote counterpart, you may want to use
hint: "git push -u" to set the upstream config as you push.
# 인터넷에서 찾아서 일단 해보자
ty@DTHOME:~/Workspace/cs/git-parctice$ git branch --set-upstream-to=origin/main
Branch 'main' set up to track remote branch 'main' from 'origin'.
# 이제 되겠지???
ty@DTHOME:~/Workspace/cs/git-parctice$ git pull
# 롸?
fatal: refusing to merge unrelated histories
# merge하면 안되냐?
ty@DTHOME:~/Workspace/cs/git-parctice$ git merge
# rhah?
fatal: refusing to merge unrelated histories
# ?????????????
ty@DTHOME:~/Workspace/cs/git-parctice$ git push -u origin main
To github.com:KimTank/git-practice-fuzzy-potato.git
    ! [rejected]
main -> main (non-fast-forward)
error: failed to push some refs to 'git@github.com:KimTank/git-practice-fuzzy-potato.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
# 왜안됭 ㅜㅜ
ty@DTHOME:~/Workspace/cs/git-parctice$ git pull
fatal: refusing to merge unrelated histories
# 된자아아앙아아!!ㅇㅊ
ty@DTHOME:~/Workspace/cs/git-parctice$ git remote -v
origin  git@github.com:KimTank/git-practice-fuzzy-potato.git (fetch)
origin  git@github.com:KimTank/git-practice-fuzzy-potato.git (push)
# 젭알
ty@DTHOME:~/Workspace/cs/git-parctice$ git push origin main
To github.com:KimTank/git-practice-fuzzy-potato.git
    ! [rejected]  main -> main (non-fast-forward)
error: failed to push some refs to 'git@github.com:KimTank/git-practice-fuzzy-potato.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
# 검색해서 원인과 해결책을 찾음 :D 
# 하지만 master는 노예제도를 연상시킨다고 deprecate feat.운도샘
ty@DTHOME:~/Workspace/cs/git-parctice$ git pull origin master --allow-unrelated-histories
fatal: could not find remote ref master
# 내걸로 변경해서 다시시도
ty@DTHOME:~/Workspace/cs/git-parctice$ git pull origin main --allow-unrelated-histories
# git core editor 지정해둔 vim이 떳따!!! 왔다!!!!!!!
# 왜 merge하는지 기록을 남긴 후 :wq 우왕
From github.com:KimTank/git-practice-fuzzy-potato
    * branchmain -> FETCH_HEAD
Merge made by the 'recursive' strategy.
    LICENSE   | 373 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    README.md |   2  2 files changed, 375 insertions(+)
    create mode 100644 LICENSE
    create mode 100644 README.md
# 뭔가 일어났다 :D
ty@DTHOME:~/Workspace/cs/git-parctice$ ls
# 우와아앙
LICENSE  README.md  index.css  index.html
# 드디어 ㅋㅋㅋㅋ 와우
ty@DTHOME:~/Workspace/cs/git-parctice$ git push
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 723 bytes | 723.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To github.com:KimTank/git-practice-fuzzy-potato.git
    43800f0..4465e44  main -> main
ty@DTHOME:~/Workspace/cs/git-parctice$ git remote -v
origin  git@github.com:KimTank/git-practice-fuzzy-potato.git (fetch)
origin  git@github.com:KimTank/git-practice-fuzzy-potato.git (push)
ty@DTHOME:~/Workspace/cs/git-parctice$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
ty@DTHOME:~/Workspace/cs/git-parctice$ clear
```

변태라고해도 좋다. 재밋다 꺄륵

## 참조

> [Educative:Git fatal error refusing to merge unrelated histories](educative.io/answers/the-fatal-refusing-to-merge-unrelated-histories-git-error)