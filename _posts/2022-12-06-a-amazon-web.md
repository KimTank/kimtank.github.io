---
layout: post
title: "Cloud Computing"
date: 2022-12-06
categories:
  - Network
tags:
  - Network
  - JavaScript
  - React
  - Web
  - Cloud Computing
  - Deploy
---

GCP, Oracle 가상컴퓨터, 돈이되는 사업, Amazon이 쏘아올린 작은 리소스

---

## 1. Cloud Computing

온프레미스라는 데이터센터를 구축하여 서버와 자원, 공간 및 네트워크 환경을 제공한다.

1. SaaS: Software as a Service, 클라우드 제공자가 당장 사용 가능한 소프트웨어를 제공
2. PaaS: Platform as a Service, 클라우드 제공자가 데이터베이스, 개발 플랫폼까지 제공
3. IaaS: Infrastructure as a Service, 클라우드 제공자가 가상 컴퓨터까지 제공

|      | network | H/W | OS  | platform/DB | Application |
| :--: | :-----: | :-: | :-: | :---------: | :---------: |
| SaaS |    ■    |  ■  |  ■  |      ■      |      ■      |
| PaaS |    ■    |  ■  |  ■  |      ■      |             |
| IaaS |    ■    |  ■  |     |             |             |

## 2. Deploy

Deployment: 개발한 서비스를 사용자가 이용가능하게 하는 과정이다.

- Development: 각자 컴퓨터에서 코드를 작성하고 테스트하는 개발 단계, 더미데이터로 테스트
  - Local 컴퓨터 환경에서 개발 및 테스트
  - Smaple Data 이용
  - 변경사항 있어도 문제안됨
  - 모든 구성원이 각자 환경 진행
- Integration: 각자의 컴퓨터에서 작성한 코드를 합치는 과정이다. 
  - 각자의 환경에서 개발된 부분을 취합
  - 코드간 Conflict가 없는지 확인
  - 작성한 코드가 다른 코드에 문제를 발생시키지 않는지 확인
- Staging: 실제 출시 단계인 Production단계와 가장 유사한 환경에서 테스트를 진행한다. 실데이터를 복사해 문제가 있는지와 관련 부서와 확인을 거친다.
  - Production단계와 가장 유사한 환경에서 테스트
  - 복제된 실제 데이터를 이용해서 테스트
  - 모든 관계자들에게 검증하는 단계
- Production: 개발된 서비스를 출시하는 단계, 코드를 구동하고 서비스를 제공한다.
  - 개발환경과는 구분 된 환경
  - 실제 데이터를 이용
  - 실제 서비스가 제공되는 단계

배포에서는 환경의 차이를 이해하고 환경 설정을 코드와 분리하는 것이 중요하다.

- 절대경로 대신 상대경로를 사용한다.
- 환경에 따라 포트를 분기할 수 있도록 환경변수를 설정한다.
- Docker와 같은 개발 환경 자체를 통일시키는 솔루션을 사용한다.

## 참조

> []()
