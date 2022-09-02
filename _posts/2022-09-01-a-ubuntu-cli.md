---
layout: post
title: "Linux!!!!!"
date: 2022-08-31
categories:
- ubuntu
tags:
- Linux
- Ubuntu
- CLI
- Vmware
---

처음 사용해본 OS는 Dos였다. 황금도끼라는 게임을 하기 위해 Dos에서 cd.. cd game과 같은 명령어로 golden-axe.bat?이였던가? 같은 실행구문을 치고 게임을 즐겼던 기억이 난다. 이후로는 Windows3.1, Windows95, Windows98, Windows2000?, WindowsXP를 거칠때 즈음 컴퓨터를 판매할때 가격에 OS가격도 녹아난단 것을 알고, 그때까진 컴퓨터를 사용하기 쉽게 만들어 주었고, 처음 프로그램이란걸 접하게 해주었던 마소 창업자인 빌게이츠(이후 빌형)를 신처럼 생각하다 이후로는 "와우 장사잘하는구나" 라고 생각을 바꾸었다. 

그러던 도중 인터넷 세상에서 이것저것 뒤져보던 중 리눅스를 알게되었고, 당시는 우분투같은 GUI시스템이 발전하기 전 DOS와 같은 무언가가 있구나 라는걸 알게되었었다. 그때 처음 다가온 리눅스 토발즈(이후 토형)님은 새로운 컴퓨터 세상의 신으로 다가왓었다. 그도 그럴 것이 자본주의 시장의 악랄한 장사꾼들의 OS(빌형 미안해요)를 완성되지도 않은걸 판매하고 부자가되는 것을 부정한다는 느낌의 소개글을 봐서 뭔가 독립투사같은 오픈소스진영의 철학이 마음에 불을 지핀것일지도 모른다. 당시 학생이던 나는 선조들의 독립운동이나, 학생운동, 민주화운동에대한 묘한 동경을 하고 있었기에 더욱 그랬다.

물론 지금에서야 감성비라고 생각했던 맥OS(개발을 배운 후 현업에서 일하기 전까진 관심도 없었다. 하드웨어성능에 비해 악랄한 아이폰의 가격때문에!)가 그렇게 안정적인 OS라서 전문가분들이 이용을 많이한다는것을 알게되었고, 오픈소스진영의 자유라는것이 상업과 비상업의 경계에서 애매하게 줄타기하는 실로 자본과는 멀어질 수 없다는것. 그리고 빌형 역시 천재이지만 실지로는 일정부분이상부터는 OS개발보다는 사업확장(부의 축적 경외감)을 위해 노력했다는것. 그리고 토형도 역시 노력에 대한 대가를 바라지 않는 발룬티어가 아니라 자신이 사용하기 위해 투사의 개념보다는 "아 야 이런 완성도 안된걸 내가 돈을 내고 써야되냐?"라는 개념으로 "그럴바엔 내가 만들어서 쓸건데 이정도는 만들어줄테니까 니네가 필요하면 더 만들어봐" 라는 느낌으로 현재의 리눅스 생태가 형성된것. 그리고 지금은 고인이되신 스티브잡스(이후 잡형)님은 이전이나 지금이나 마소조차 오픈화한것에도 끝까지 소스공개를 하지않는걸 원칙으로하는 현재까지 나온 OS중에 가장 완벽하다는 MacOS까지..

역시 생각은 생각에 꼬리를 물고 의식의 흐름은 뇌내의 어딘가에서 강물처럼흘러 바다처럼 가지만 이것역시 내가 긁고 듣고 이해하려다 생긴 무언가의 정확한 팩트가아닌 변조된 기억이므로 잡설일 것이지만, 계속적으로 전문가가 되려고하는 지금의 입장에서는 너무 궁금한게 많다.

나는 굉장히 경험에 기반한걸 중요하시하는 성향이 있는만큼 존경하는 빌형, 멋지게 살다간 잡형, 아직도 신이라 생각하는 토형까지 그들의 OS를 다 사용해보고싶은 욕심을 codestates에서 채워주었다.

가보자.

# Linux!!!!!
아직은 쪼렙이기 때문에 Ubuntu를 사용하여 GUI환경으로 접한다.

## 터미널 사용
- `ctrl` + `alt` + `t`를 이용하여 터미널을 실행시킬 수 있다. 
- GUI를 통해 실행시킬 수 도 있는데, `cmd`(윈도우키) + `a`를 이용하여 현재 시스템에 연결되어있는 패키지를 아이콘으로 보고 클릭하여 실행할 수 있다.
> 단축키는 몰라도 우분투 환경에서는 사용하는데 무리는 없지만, 알고있으면 마우스를 휴대할 필요가없다.

## Prompt
윈도우에서는 윈도우10 이후로 나도모르는 문제가 발생했을 때 능력자들이 해결할 수 있는 커맨드를 올려놔서 사용해본 파워쉘이나, 윈도우 자체 내 Dos라고 생각했던 영화에서 해킹할때 나오던 그 검은화면 CLI(Command-Line Interface).

### 명령어
- pwd(print working directory): 현재 위치 확인하기(폴더 구조내 나의 위치)
- mkdir(make directories)

```bash
$mkdir helloWord
```
- ls(list): 특정 폴더에 포함된 파일이나 하위 폴더 리스트 출력
  - -l: 파일포멧 전부 표현
  - -a: all
  - -al 또는 -la

> > 리스트에서 제일 앞이 d인것은 폴더, l인것은 파일이다.(다 정해진 약속이 있다.)

- nautilus: 현재 위치를 파일탐색기를 통해 연다.
- cd(change directory): 폴더 이동
- touch: 파일 생성

```bash
$touch any-file-name.extention_word #exe, text etc
```

- cat: 파일내용 터미널에 출력

```bash
$cat any-file-name.extention_word
```

- rm: 휴지통을 거치치 않고 삭제한다.

```bash
# 확장자를 점점 줄이고싶어 ex-wd 이후 e-d
$rm file-dont-want.extnt-wrd
$rm -rf folder-dont-want.ex-wd
```
  - -rf: 폴더를 지울때 옵션. 안넣으면 동작안하며 경고날림
  - -r(recursive): 폴더 지울때 사용
  - -f: 질문을 받지 않을 때 사용

- mv(move): 폴더나 파일의 이름을 변경 또는 이동
  - GUI 드래그앤 드롭으로 이용, cli는 mv를 이용
- cp(copy): 폴더나 파일의 이름을 복사

```bash
# cp 원본파일 복사할파일
$cp original.e-d copied.e-d

# 폴더의 경우 -rf옵션 추가
$cp -rf original copied

# 상위로 복사
$cp original.e-d ../
$cp -rf original ~/UpperDirectory/
```

- whoami: 현재 사용자가 누군지 확인할 수 있다.
```bash
$whoami
# 결과
# [username]
```

- sudo: rootAuth를 획득하는 명령어
- apt: 패키지 매니저
  - apt update: 패키지 목록 갱신(rootAuth)
    - 패키지를 다운로드 할 수 있는 지정된 저장소의 최신 정보를 업데이트함. 새로운 저장소를 추가하거나, 패키지를 설치하기전 최신정보를 갱신함.(설치 후 저장소(mirror server)를 변경하면 빨라진다.)
  - apt list --upgradable: 업그레이드 가능한 패키지 목록을 출력
  - apt upgrade: 전체 패키지 업그레이드 - (rootAuth)
  - apt --only-upgrade install packageName: 특정패키지 업그레이드(rootAuth)
  - apt install packageName : (rootAuth)
  - apt list --installed: 설치된 패키지 보기
  - apt search searchKeyword: 패키지 검색
  - apt show packageName: 패키지 정보 확인
  - apt remove packageName: 패키지 이름(권한)

---
우분투는 dos와는 다르다. 윈도우의 파워쉘역시 사용법이 특이하다고 생각했었는데, 익숙해 진다면 여느 매체에서 보던 전문가처럼 "다라라ㅏ라라다라랄라다ㅏ랃 (컴퓨터 연산소리 지이이지이이이) 다라닫라라라라다라라다"하는 것처럼 키보드만으로 멋있는 척(남이하면 우와아아 전문가다, 내가하면 나 좀 쩌는듯)할 수있는 뭔가 있어보이는 그런 무언가 생길거 같다.
> ## 참고
> [W3Schools:CLI](https://www.w3schools.com/whatis/whatis_cli.asp)   
> [Ubuntu:Command Line for Beginner](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)   
> [CSCS&Info:Doc/Linux shell commands](https://docs.cs.cf.ac.uk/notes/linux-shell-commands/)