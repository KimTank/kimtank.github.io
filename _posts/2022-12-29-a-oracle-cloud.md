---
layout: post
title: "Oracle Cloud"
date: 2022-12-29
categories:
  - Web
tags:
  - Web
  - Oracle Cloud
  - instance
  - 가상네트워킹
  - VNIC
  - PuTTYgen
  - PuTTY
  - ssh 외부접속
---

pre-project 중 오라클 서버를 쓸일이 생겼다.

생성에서 설정까지 따라하면되는 서버만들기

---

## 1. 가입하기

오라클은 2022년 12월 29일 현재는 무료로 인스턴스 2개, 100GB의 무제한 free tier를 제공한다.

![무료 시작](/assets/img/221229-o1.png)

가입 시 신용카드가 있어야하니, 확인 후 시도하자.

## 2. 인스턴스 컴퓨트 생성

햄버거 -> 컴퓨트 -> 인스턴스

![인스턴스 컴퓨트](/assets/img/221229-o2.png)

![인스턴스 생성](/assets/img/221229-o3.png)

이미지 및 구성 -> 편집 -> 이미지 변경 -> 원하는 OS선택(유료말고 무료로)

![인스턴스 이미지 및 구성](/assets/img/221229-o4.png)

![인스턴스 이미지 및 구성1](/assets/img/221229-o5.png)

Shape(cpu)의 경우 무료로 제공되는 arm과 일반(VM.Standard.E2.1.Micro)이 있다.

네트워킹 -> 편집 -> 새 가상 클라우드 네트워크 생성, 새 공용 서브넷 생성

SSH키 추가(중요) -> 자동으로 키 쌍 생성 -> 전용 키 저장(중요) 없으면 접속못함

부트볼륨 -> 사용자정의 부트 볼륨 크기 지정 -> 부트 볼륨 크기 50GB(인스턴스 두개를 주니 50GB, 50GB 두개를 만들든 100GB 1개로 쓰든 자유)

생성

## 3. 예약된 주소(고정IP할당)

인스턴스 -> 목록 -> 생성한 인스턴스 -> 연결된 VNIC -> VINC목록 -> 생성된 VINC -> 리소스탭(IPv4주소) -> IPv4 햄버거 버튼 -> 전용 IP 주소 편집 -> 임시공용IP(선택됨) -> 공용IP없음(선택) 업데이트 -> IPv4 햄버거 버튼 -> 전용 IP 주소 편집 -> 공용IP없음(선택됨) -> 예약된 공용IP 선택 업데이트

![고정IP 할당](/assets/img/221229-o6.png)

![고정IP 할당1](/assets/img/221229-o8.png)

![고정IP 할당2](/assets/img/221229-o9.png)

## 4. PuTTY로 인스턴스로 접속

https://www.putty.org/ -> putty 다운로드

https://www.puttygen.com/ -> putty gen 다운로드

puttygen 실행 -> load -> 파일유형 all files -> 아까 2.에서 중요하다고한 SSH 전용키 YOUR_SSH_KEY_ssl.key 열기 -> Save private key

![PTg](/assets/img/221229-o13.png)

![PTg1](/assets/img/221229-o14.png)

![PTg2](/assets/img/221229-o10.png)

putty 실행 -> 생성한 Oracle Cloud 공용 IP 복사 -> Session -> host Name 붙여넣기 -> Connection -> SSH -> Auth -> Credentials => Private key file for authentication -> Brower -> PuTTYgen으로 저장한 pivate key 불러오기 -> Session -> Saved Sessions -> 저장할 이름 -> save -> Open -> ubuntu -> ubuntu, etc(centos, oracle linux) -> opc 입력하면 접속

![PTg](/assets/img/221229-o16.png)

![PTg1](/assets/img/221229-o11.png)

![PTg2](/assets/img/221229-o12.png)

[우분투 세팅](https://kimtank.github.io/os/2022/11/01/a-ubuntu-init.html)

---

다음번엔 오라클 클라우드 가상네트워킹 포트 열기 & 우분투 방화벽설정 및 포트열기

---

> ## 참조
>
> [OCI: free tier](https://www.oracle.com/kr/cloud/free/?source=CloudFree_CTA1_Default_kr&intcmp=CloudFree_CTA1_Default_kr)  
> [NES: 오라클 클라우드 인스턴스 생성하기](https://mungiyo.tistory.com/12)  
> [NES: 오라클 클라우드 인스턴스 외부 접속](https://mungiyo.tistory.com/13)
