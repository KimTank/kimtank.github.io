---
layout: post
title: "소프트웨어 개발 프로세스"
date: 2020-07-27T00:00:00-00:00
categories:
 - 소프트웨어 공학
tags:
 - 소프트웨어 개발 프로세스
 - 성공 프로젝트 관점 개발
 - 개발 생명주기
 - SDLC와 개발방법론
 - 애자일 프로세스와 방법론
 - 김희영
---
# 4장 소프트웨어 개발 프로세스

## 4.1 소프트웨어 개발 프로세스란?

> SEI(SW Engineering Institute), "소프트웨어 생산에 사용되는 활동, 방법 및 실무작업들의 집합"
>
> IEEE, "주어진 목적을 달성하기 위한 순서적인 절차 틀"
>
> CMMi(Capability Maturity Model integration)의 창시자 와츠 험프리, "소프트웨어 제품의 품질은 그 제품을 만들기 위해 사동된 프로세스의 품질에 의해 결정된다."



## 4.2 성공한 프로젝트 관점의 개발

- 수행 프로세스의 관점 : 수행하기로 한 업무를 모두 수행하였는지
- 프로덕트의 관점 : 완성된 소프트웨어가 요구한 모든 기능을 구현하고 있는지
- 결론적 고객의 입장에서 만족스러워야함.



## 4.3 개발 생명주기(SDLC)

Software Development LifeCycle : 어떻게 개발할것인가 추상적 표현, 개발 업무를 단계적으로 나타내주는 기본체계

1. ### 폭포수 모형(waterfall model)

   - 정의

   단계의 완료를 문서로 명확하게 확정한 후 다음 단계로 넘어가는 체계적 순차적 접근방법

   - 특징
     1. 가장 많이 사용됨
     2. 프로젝트 검증 용이
     3. 순차적 진행
     4. 계약상 명확한 단계별 완수여부 확인 가능
     5. 앞 단계 수정 어려움

   - 장점
     1. 이해쉬움
     2. 정형적 접근법 제공
     3. 진행 명확하게 알 수 있음
     4. 체계적 문서화 가능
   - 단점
     1. 이전 단계의 완료 및 승인이 없이 다음 단계로 이행 불가
     2. 소프트웨어 가시화가 대단히 어려움
     3. 요구사항 시스템반영됬는지 확인하는데 많은 시간 경과해야됨.

   

2. ### 프로토타입 모형(prototype model)

   - 형상이나 설계, 적합성을 평가하기 위해 완성된 소프트웨어와 비슷함.

   - 미리 모형을 개발하고 사용자의 평가 후 본격적으로 구현하는 방법을 제시

   - 특징

     1. 사용자 요구사항 반영 위해 반복적인 설계/개발과정 거치는 점증적 방법
     2. 이전 단계의 완료 및 승인 없이 다음 단계 이행안됨.

   - 장점

     1. 요구사항 도출 용이, 변경 자유로움
     2. 가시화된 요구사항으ㅏ로 이해하기 쉬움.

   - 단점

     1. 결과물 최종산출물이 아니라, 구현과정 추가 필요함.
     2. 자원의 낭비가 심함.
     3. 변경 많아 중간산출물의 문서화 어려움.

     

3. ### 나선형 모형(spiral model)

   - 정의

   폭포수 모형의 체계적, 프로토타입 모형의 반복 특성 결합, 위험분석 추가하여 점진적 소프트웨어 완성하는 접근법

   - 목적

     프로젝트의 위험을 최소화

   - 장점

     1. 사전의 다양한 위험 대처가능
     2. 비용과다 혹은 납기지연 문제 조기에 해결

   - 단점

     1. 위험분석 잘못될때 심각한 문제 야기
     2. 다른 모형에 비해 복잡함.
     3. 프로젝트 관리 어려움.

     

## 4.4 SDLC와 개발방법론

SDLC의 개념을 활용하여 구체적 방법을 제시한 것이 개발방법론.

- 신속애플리케이션 개발(RAD: Rapid Application Development)
- 유피(UP: Unified Process)
- 마르미(MaRMI: Magic and Robust Methodology Integrated)

1. ### RAD

   - 목적

     개발도구 활용 대신 문서화를 대폭적으로 줄여, 짧은 시간에 소프트웨어 개발함.

     고객에게 시스템을 빠르게 인도

   - 특징

     1. 기능과 UI에 대한 요구사항에 더 비중둠.

     2. 문서산출물 생략 혹은 추후 작성함.
     3. 전통적 폭포수 모형의 단계 중 분석과 설계 단계를 결합, 단순화시킴.

   - 장점

     1. 단계 축하여 문서산출물 부담 줄임.
     2. 프로토타입을 활용하여 빠른 고객의 요구사항 파악
     3. 간결한 개발기법 활용

   - 단점

     1. 시스템 성능에 문제가 발생할 수 있음.
     2. 문서작성을 추후에 하므로 의사소통 문제 발생
     3. 시간 단축위해 작업 병행하여 진행하면 혼선 발생할 수 있음.
     4. 기존 시스템과 인터페이스 고려 않을 위험

     

2. ### UP

   - 정의

     객체지향 분석설기법 적용하여 개발하는 방법론

   - 특징

     1. 반복적
     2. 점진적
     3. 유스케이스(usecase)기반 분석과 설계 진행
     4. 아키텍처 중심 개발 지향
     5. 위험관리 중시

   - 도입(inception)

     전체 요구사항 이해, 프로젝트 개발여부 결정

   - 상세(elaboration)

     요구사항 분석 및 아키텍처 확정, 위험요소 해결

   - 구축(construction)

     사용자의 환경에서 실행 가능한 시스템을 구축, 평가 중점

   - 이행(transition)

     개발 완료하고 품질 보장하며, 사용자에게 인도

   - 장점

     1. 위험요소 초기에 완화 가능
     2. 요구사항에 보다 근접한 시스템 개발 가능
     3. 반복이 거듭되면 피드백 작용, 교훈(Lessons Learned)이 반영

   - 단점

     1. 반복은 일정지연의 원인
     2. 끊임없는 변경으로 개발자의 피폐화 발생
     3. 전체 프로세스를 개발자 이해 어려움.

     

3. ### 마르미

   - 한국전자통신연구원(ETRI) 개발한 한국형 소프트웨어 개발방법론, 한국실정에 맞추도록 체계화에 목적

     1. 마르미  : 구조적 방법론(마르미-1)
     2. 마르미-2 : 객체지향 개발방법론
     3. 마르미-3 : 컴포넌트 기반의 개발방법론, CBD방법론
     4. 재활용을 위한 모듈화 개발기법
     5. 초기부터 재활용 가능한 컴포넌트 개발
     6. 마르미-4 : 재공학 지침을 제공하는 방법론

     

## 4.5 애자일 프로세스와 방법론(Agile Process and Methodology)

- Agile : 민첩한
- 등장 이유 : 전통적 방법 소프트웨어는 개발에 시간이 너무 많이 걸림.
- 애자일 선언문("Manifesto for Agile Software Development") ≒ 애자일 가치(Agile software development values)
  1. 프로세스와 도구보다 사람들과 소통이 중요(Individuals and Interactions over processes and tools)
  2. 상세한 문서보다 작동하는 소프트웨어가 중요(Working Software over comprehensive documentation)
  3. 계약협상보다 고객과의 협업이 중요(Customer Collaboration over contract negotiation)
  4. 계획대로 진행하는 것보다 변경에 대응하는 것이 중요(Responding to Change over following a plan)

1. ### 애자일 선언문

   애자일 엽합(Agile Alliance) "애자일실행 가이드(The Guide to Agile Practices)", "애자일 용어사전(Agile glossary)"
   1. Customer satisfaction by early and continuous delivery of valuable software 고객은 좋은 소프트웨어 빠르고 계속 좋아함.
   2. Welcome changing requirements, even in late development 변경된 요구사항은 아무리 늦어도 환영
   3. Working software is delivered frequently(weeks rather than months) 동작하는 소프트웨어 자주 줌
   4. Close, daily cooperation between business people and developers 사업가와 개발자의 긴밀한 협력
   5. Projects are built around motivated individuals, who should be trusted 프로젝트 동기부여된 개인으로 부터 구축, 신뢰할수 있어야됨.
   6. Face to face converstion is the best form of communication(co-location) 평등한 위치의 대화가 최고
   7. Working software is the primary measure of progress 동작하는 소프트웨어는 진행의 중요한 척도
   8. Sustainable development, able to maintain a constant pace 지속가능한 개발, 일정한 속도 유지
   9. Continuous attention to technical excellence and good design 우수한 기술, 좋은 디자인에 대한 지속적 관심
   10. Simplicity- the art of maximizing the amount of work not done- is essential 단순성(수행되지 않은 작업량을 최대화 하는 기술) 필수
   11. Best architectures, requirements, and designs emerge from self-organizing teams 자체구성팀에서 최고의 아키텍처, 요구사항, 디자인이 나옴.
   12. Regularly, the team reflects on how to become more effective, and adjusts accordingly 팀은 정기적으로 효과적 방법 반영, 그에 따라 조정

- 실행가능 방법론 XP(eXtreme Programming), 스크럼(Scrum) 대표적



2. ### XP 방법론

   켄트 벡이 창안

   - 특징

     1. 고객과 개발팀이 상주하며, 서로간의 의사소통 중요시함.

     2. 개발범위 우선순위화함.

     3. 초기에 고객으로부터 피드백 받음.

     4. 개발자에게 변경 두려워하지말라 강조

        - 단순성(simplicity) : 시스템 구조 고객과 합의 바탕의 설계 단순성 유지
        - 의사소통(communication) 문서보다 구두에 의한 소통 중시, 고객이 개발팀 상주(원활한 소통)
        - 피드백(feedback) 릴리즈를 위해 고객이 인수테스트 실시, 부적합사항에 대한 피드백
        - 용기(courage) 개발자 용기가져야함. 강조
        - 존중(respect) 서로 존중하고 배려해야됨.

        

3. ### 스크럼 방법론

   - 정의

     팀의 개선과 프로젝트관리를 위한 방법론, 개발 조직의 효율적 운영 방식 제공.

   - 특징

     개발 과정에서 발생하는 일과 위험을 예측, 곤리 할수 있는 반복적, 점증적 접근법

   - 프레임워크

     1. 제품 백로그(Product backlof)

        - 개발 위한 기능목록 해당함. 
        - 기능목록은 사용자의 요구사항에서 도출된 것. 사용자 측의 제품책임자(product owner)에 의해 개발 우선순위 매겨짐. 
        - 사용자와의 지속적 의사소통으로 수정 가능, 
        - 스프린트의 한주기(2~4주)가 끝나기 전 수정하지 않는 것 좋음. 
        - 제품 책임자 정한 우선순위 가지고 개발팀에 해당하는 스크럼팀과 작업에 대한 조율 진행. 
        - 조율결과, 합의된 제품 백로그는 스프린트로 구현을 진행하기 위한 초기 근거

     2. 스프린트 계획 회의

        - 제품 백로그 어떻게 구현할지 스크럼팀에서 스프린트 목표와 이를 달성하기 위한 필요작업 목록에 대한 계획 수립
        - 6~8명 스크럼팀 구성
        - 프로젝트 관리자와 거의 동일한 스크럼 마스터 팀의 책임
        - 스크럼 마스터 팀원 코칭, 문제해결하는 역할 수행
        - 스프린트 주기의 기간을 결정

     3. 스프린트 백로그(Sprint backlog)

        - 스프린트 회의결과 작업목록이 작성된 결과가 스프린트 백로그
        - 개발팀원들 각자 스프린트 목표 달성을 위한 작업 할당
        - 4~16시간 작업소요 업무
        - 개발팀내 자율적 정하며, 팀원간 협업체계에 따라 의사소통 진행 중요

     4. 스프린트 수행

        - 2~4주 정도 시간이 소요되는 수준으로 업무 진행
        - 스프린트 계획회의에서 제품리뷰회의 진행날까지 '1 스프린트 주기'
        - 스프린트 진행동안, 일일 스크럼 회의 매일 동일한 시간과 장소에서 진행

     5. 일일 스크럼 회의

        - 스크럼 마스터 주재하 개발 팀원 참여하여 어제 한일, 오늘 할일, 이슈사항 등 공유
        - 산출물 갱신하고, 진척상황 관리함.
        - 진척상황 소멸차트(Burndown chart)를 작성, 관리
        - 소멸차트 : 시간의 경과에 따라 남아있는 업무가 무엇인지 도식화함.

     6. 작동 가능한 SW제품(shipable product)

        - 스프린트 진행되는 동안 지속적으로 제품 갱신되며, 한 주기 끝나면 '작동 가능한 SW제품'도출됨.
        - SW제품 품질은 스프린트 계획회의에서 목표로 정한 수준을 만족하는 수준
        - "스프린트 검토회의(sprint review)"에서 목표를 달성했는지 결과를 확인, 점검
        - 확인 및 점검은 제품책임자와 사용자가 개발자의 시연과 도움을 받아서 진행

     7. 스프린트 회고(sprint retrospective)

        - 스크럼팀 내부에서 스프린트 활동과 개발한 내역을 되돌아보고 개선점을 찾는 것.
        - 부정적 부분보다 긍정적 부분 극대화하는 방안 찾는것 중요.
        - 계획과 실제 업무진행의 차이분석, 추후 계획 원활하게해야됨.
        - 회고이후 새 스프린트 주기 실행하여 다시 스프린트 계획회의를 진행함.

        

