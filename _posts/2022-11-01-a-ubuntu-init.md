---
layout: post
title: "Ubuntu init"
date: 2022-11-01
categories:
- OS
tags:
- Unix
- Linux
- Ubuntu
- Linus Benedict Torvalds
- Windows11
- Windosw10
- wsl
- wsl2
- git
- gh
- sudo
- su
- passwd
- nvm
- node version manager
- nodeJS
- npm
---

Os는 경이롭다. Dos, Win 3.1, Win95, Win98, WinNT, Win2000, WinXP, Win7, Win10, Win11까지 자본주의에 이념에 맞게 계속하여 새로운 시도와 새로운 사용자경험을 할 수 있게 해준다. 중간중간 실패한 버전들도 있었지만, Cpu나 메인보드 인터페이스에 맞는 지원을 위해 아낌없이 R&D에 투자하는 마소는 역시 미워할수없다.

하지만 이건 리눅스란걸 모를때 이야기고, 사실 개발자가 아니라면 사용할까싶은 CLI환경 역시 사용처에 따라서는 불필요한 리소스를 사용하지 않게 하므로 상당히 매력적인 OS이다.

MacOS와는 다르게 어느정도 Windows 운영체제와 단축키나 키세팅이 비슷하여 사실 Unix기반으로 비슷하다고 볼 수 있는 MacOS와는 다르게 Windows를 평생 써왔던 일반 유저의 경우에는 MacOS보다는 Unix기반의 Linux가 더 편할지도 모른다.(CLI환경만 아니라 다른 커널을 올려서 쓴다는 걸 가정하에)

하지만 GUI환경까지 올린 Ubuntu의 경우에는 Package별로 관리해야되고, 관리를 위해 여러가지 프로그램을 설치해야 Windows와 비슷한 환경에서 사용할 수 있었고, 지원하지않는.. 그러니까 정확하게는 누군가가 만들어주지 않는다면, 아니면 내가 현재처럼 직접 필요한걸 만들지 못한다면, Linux는 CLI환경을 벗어나 GUI환경으로 가기에는 너무 불편한 펭귄(별로안좋아함)이다.

그리하여 MacOS에서 잘라내기 조차 못하는 내 입장에서는 효율적인 Windows가 최적이었고, 어떤 환경이라도 생산성이 떨어지지 않는건 역시 선택권이 없었다. 다행이도 Window하위시스템으로 WSL이 출시되고, distro를 통한 virtual환경의 linux를 사용할 수 있다는 것을 알게된 뒤로는 전혀 선택을 할 필요가 없었다.

다른말로 시간을 낭비하지 않아도 되었다.

Windows11의 출시소식을 듣고, TPM2.0을 지원하지 못하는, 1세대 amd였기에 설치를 꺼리고 있다, 마침 팔려고 놔뒀던 씽크패드L15에 Windows11을 설치했다. 새로나온 Windows 새로나온 기능, 미려한 디자인, 최적화된 성능 등 매우 매력적인 OS라 생각한다. 일반적 평은 8.1의 망작을 보는것같다 하지만, 실제적으로는 매우 가볍고, windows10보다는 성능적으로도 우월하다는것은 하드웨어 성능테스트가 입증한다.

하지만 무슨문제였는지, 지금 진행하는 일들이 뻗어버렸다. windows10에서는 문제가 없었던 wsl이 windows11에서 문제가 발생했다. 다행히 다운그레이드는 1분도 걸리지 않았으나, 협업중에 이런일이 있었다면 정말 난감했을 것이다. Android에 Linux Gui를 설치하여 돌아다니면서 만질 수 있는 900g도 채 되지않는 vscode를 돌릴 수 있는 포터블 데스크탑을 만들때 계속 하던, Ubuntu설치 후 했었던 CLI기본세팅.

다음에 또 비슷한 일이 생겼을 때 여러사이트를 찾아다니지 않기위해 남긴다.

---

## 0. before init

본 글은 부연설명은 하지 않는다. 각 필요한 정보의 경우는 하위 참조에서 직접 확인하시길 바라며, 단순히 복사 붙이기를 하기위한 문서이다. 관련 설정의 경우에도 필자가 사용하기 편하게 기재하니, 단순하게 복사붙이기가 아닌, 변경해야될 부분은 변경하여야 한다.

## 1. WSL

### 1-1. [Wsl install & init](https://wslhub.com/wsl-firststep/firststep/install/)

Window PowerShell 관리자 모드 실행

- Gui 설치

```bash
Start-Process 'https://aka.ms/termianl`
```

#### 1-1-1. 자동설치

- Cli 설치

```bash
wsl.exe --install
```

재시작

- 설치할 수 있는 버전 확인

```bash
wsl.exe --list --online
```

- 원하는 버전 설치

```bash
wsl.exe --install -d Ubuntu-20.04
```

#### 1-1-2. 수동설치

- WSL, HCS 설치(PowerShell 관리자모드)

```bash
If ((Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform, Microsoft-Windows-Subsystem-Linux).RestartNeeded) { Restart-Computer -Force }
```

- 재부팅 후 파워셀 관리자모드

```bash
wsl --set-default-version 2
```

- 일반 x64

```bash
Set-Location -Path $env:USERPROFILE\Downloads
$TargetUri = "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi"
Invoke-WebRequest -Uri $TargetUri -OutFile .\wsl_update_x64.msi
.\wsl_update_x64.msi
```

- 주의 arm은 상기 x64가 아닌 아래 arm용

```bash
Set-Location -Path $env:USERPROFILE\Downloads
$TargetUri = "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi"
Invoke-WebRequest -Uri $TargetUri -OutFile .\wsl_update_arm64.msi
.\wsl_update_arm64.msi
```

- ubuntu 20.04

```bash
Set-Location -Path $env:USERPROFILE\Downloads
$TargetUri = "https://aka.ms/wslubuntu2004"
Invoke-WebRequest -Uri $TargetUri -OutFile .\ubuntu.zip
New-Item -Type Container -Path $env:SYSTEMDRIVE\Distro\Ubuntu2004
Expand-Archive -Path .\ubuntu.zip -DestinationPath $env:SYSTEMDRIVE\Distro\Ubuntu2004
Remove-Item -Path .\ubuntu.zip
Set-Location -Path $env:SYSTEMDRIVE\Distro\Ubuntu2004
.\ubuntu2004.exe
```

### 1-2. [Ubuntu init](https://wslhub.com/wsl-firststep/firststep/ubuntu/)

- 패키지 미러 주소 변경

```bash
sudo sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list
```

- 패키지 업데이트, 업그레이드, autoremove

```bash
sudo apt update && sudo apt -y upgrade && sudo apt -y autoremove
```

- zsh설치(선택)

```bash
sudo apt -y install zsh
```

- Oh-My-ZSH(선택)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- 설치시 기본셸 사용선택안했을때

```bash
chsh -s $(which zsh)
```

- 한국어 언어팩(선택)

```bash
sudo apt -y install language-pack-ko

sudo locale-gen ko_KR.EUC-KR
sudo update-locale LANG=ko_KR.UTF-8 LC_MESSAGES=POSIX

sudo apt -y install fonts-unfonts-core fonts-unfonts-extra fonts-nanum fonts-nanum-coding fonts-nanum-eco fonts-nanum-extra fonts-noto-cjk
```

- Fuzzy Search(선택)

```bash
bash sudo apt -y install git

git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
```

### 1-3. [VScode init](https://wslhub.com/wsl-firststep/firststep/vscode/)

- [VScode WSL 확장 설치](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

![https://microsoft.github.io/vscode-remote-release/images/wsl-readme.gif](https://microsoft.github.io/vscode-remote-release/images/wsl-readme.gif)

- CLI에서 프로젝트 열기(해당 프로젝트 폴더 내)

```bash
code .
```

![https://docs.microsoft.com/ko-kr/windows/wsl/media/wsl-open-vs-code.gif](https://docs.microsoft.com/ko-kr/windows/wsl/media/wsl-open-vs-code.gif)


- VScode Gui 좌측하단 >< 탭 클릭 후 `새 WSL 창`

### 1-4. [SSH 키 생성](https://wslhub.com/wsl-firststep/firststep/sshkey/)

- 새키 생성

```bash
ssh-keygen -t rsa
```

- 만들어진 ssh-key 공개 키 값 확인(선택)

```bash
cat ~/.ssh/id_rsa.pub
```

#### 1-4-1. [비밀번호 묻지 않기](https://medium.com/@pscheit/use-an-ssh-agent-in-wsl-with-your-ssh-setup-in-windows-10-41756755993e)

- keychain 설치

```bash
sudo apt -y install keychain
```

- 키체인에 키 등록

```bash
/usr/bin/keychain --nogui $HOME/.ssh/id_rsa
```

- 생성던 스크립트 파일 확인(선택)

```bash
cat ~/.keychain/$(hostname)-sh
```

- vim(에디터)로 아래구문 추가
  - 사용자 설정파일
    - `~/.bashrc`
    - `~/.zshrc`

```bash
source ~/.keychain/$(hostname)-sh
```

### 1-5. [xdg-open의 wsl버전 설치(선택)](https://wslhub.com/wsl-firststep/firststep/bridge/)

```bash
pip3 install --user git+https://github.com/cpbotha/xdg-open-wsl.git
```

### 1-6. [Windows 네트워크 드라이버 추가하기](https://wslhub.com/wsl-firststep/firststep/networkdrive/)

1. 파일탐색기에서 주소창에 `\\wsl$` 보유한 WSL 배포판 확인
2. 네트워크 드라이버 추가할 배포판 우측클릭, `네트워크 드라이브 연결`
3. 원하는 A~Z 드라이버로 추가

### 1-7. [WSL 배포판 복사하기](https://wslhub.com/wsl-firststep/advanced/copy-distro/)

상기 링크의 방법도 있지만, NTFS파일 시스템으로인한 메타데이터 손상이 있을 시 실행에 분명히 문제가 있을 것이므로, 재설치 후 Github나 개인 아카이브와같은 저장소를 통해 다시 작업환경 구축한는걸 권장한다.

### 1-8. [wsl trouble shooting](https://wslhub.com/wsl-firststep/troubleshoot/timesync/)

- 하드웨어 시간과 동기화

```bash
sudo hwclock --htosys
# sudo hwclock -s
```

#### 1-8-1. 사용중 만났던 오류와 해결법

- [공식문서](https://learn.microsoft.com/ko-kr/windows/wsl/troubleshooting)
- [wsl 멈추는 문제 - 가상화메모리 설정](https://chp747.tistory.com/222)
- [넷마블 wsl2 트러블슈팅](https://netmarble.engineering/journey-to-wsl2-and-trouble-shooting/)
- [Vmmem 메모리 누수](https://eight20.tistory.com/18)
  - [메모리 누수 이슈 진행중](https://github.com/microsoft/WSL/issues/4166)

## 2. Git

### 2-1. [Git 설치](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

[GitBook](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)

- Ubuntu

```bash
sudo apt install git-all
```

- RPM 기반 Fedora, RHEL, CentOS

```bash
sudo dnf install git-all
```

- [이외 배포판](http://git-scm.com/download/linux)

### 2-2. [Git 설정](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%B5%9C%EC%B4%88-%EC%84%A4%EC%A0%95)

- 내정보(없으면 동작안함)

```bash
git config --global user.name "너의이름"
git config --global user.email 너의아이디@남의페이지.com
```

- 편집기 설정

```bash
git config --global core.editor vim
```

### 2-3. [도움말](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%8F%84%EC%9B%80%EB%A7%90-%EB%B3%B4%EA%B8%B0)

다른사람의 블로그를 참고하기보다는 최신화가 이루어지는 공식 문서를 확인하는것이 마음이 편하다.

## 3. [Node Version Manager](https://github.com/nvm-sh/nvm)

- 설치 스크립트

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

or

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

- 설정추가

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

리눅스 설치관련이니, [문서](https://github.com/nvm-sh/nvm#table-of-contents)를 확인하자.

### 3-1. NodeJS 설치

상기 [문서](https://github.com/nvm-sh/nvm#long-term-support)를 읽어보면 되지만, 일반적으로는 `명령어 -h || --help`등과 같이 검색할 시 cli에서 각종 실행할 수 있는 명령어가 나오니, 막히면 [문서](https://github.com/nvm-sh/nvm#long-term-support)를 보자.

### 4. [Git cli gh(선택)](https://cli.github.com/)

auth를 위한 설치

- [OS별 설치법](https://github.com/cli/cli#installation)
- [Linux](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)
  - Ubuntu 설치

```bash
type -p curl >/dev/null || sudo apt install curl -y
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```

- upgrade

```bash
sudo apt update
sudo apt install gh
```

---

## 참조

> [WSL한국포럼: first-step](https://wslhub.com/wsl-firststep/)   
> [git:main](https://git-scm.com/)   
> [nvm:main](https://github.com/nvm-sh/nvm)   
> [git cli:main](https://cli.github.com/)