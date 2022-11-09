---
layout: post
title: "Network deep vol.1"
date: 2022-11-09
categories:
- Network
tags:
- Network
- ARPANE
- Internet Protocol
- IP
- Packet
- Transmission Control Protocol
- TCP
- User Datagram Protocol
- UDP
- International Organization for Standardization
- ISO
- Open Systems Interconnection Reference Model
- OSI
---

블로그 정리의 시기가 다가왔다. ruby도 알아야하는 상황 미루면 크게 오는구나

---

## 1. 역사

IP 기반 네트워크는 1969년 ARPANE에서 시작되었다. 핵전쟁을 대비하기 위해 기존 회선교환방식에서 패킷교환방식으로 구축하였다.

1. 회선교환방식: 중간자인 Operator가 있어 전용선을 미리 할당하여야하고, 동시에 다른통신을 할 수 없다.
2. 패킷교환방식: 데이터를 잘게 나누어 전송하여, 특정 회선이 전용선으로 할당되지 않아 효율적이다.

Internet Protocol, IP는 출발지와 목적지의 정보를 IP주소라는 특정한 숫자값으로 표기하고, 패킷단위로 데이터를 전송한다.

## 2. Packet

Pack + Bucket -> Packet, 소포

출발지 IP, 목적지 IP와 같은 정보가 포함된다.

### 2-1. IP Protocol 한계

- 비연결성: 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
- 비신뢰성
  - 중간에 패킷 손실이 있을 수 있음.
  - 패킷 순서 보장 못함.

## 3. TCP/UDP

네티워크 프로토콜 계층은 OSI 7계층과 TCP/IP 4계층으로 나눈다.
IP Protocol보다 더 높은 계층에 TCP Protocol이 존재하며, IP Protocol의 한계를 보완할 수 있다.

> 개발순서: TCP/IP 4계층 -> OSI 7계층
> 두 모델은 정확하게 일치하지 않는다. 실제 네트워크 업계 표준은 TCP/IP 4계층에 가깝다.

Http msg create -> Socket(TCP(msg)) Transport -> TCP info create(include msg data) -> IP(Packet create(TCP info(msg data))) -> Ethernet Frame(IP(TCP(msg)))

1. Transmission Control Protocol(TCP): 전송제어프로토콜 세그먼트는 IP패킷의 출발지 IP와 목적지IP정보를 보완할 수있는 출발지PORT, 목적지PORT, 전송제어, 순서, 검증 정보등을 포함하여
   - 연결지향: TCP 3way handshake(가상 연결)

      |---|---|---|---|
      |클라이언트|방향|서버|비고|
      |from|->SYN->|to|접속 요청 SYN packet 전송|
      |to|<-SYN+ACK<-|from|SYN요청 받아 요청수락 ACK+SYN 설정 packet 전송 후 litsen ACK응답|
      |from|->ACK->|to|ACK 전송(현재 최적화로 이단계에서 ACK+DATA|
      |to|<-ESTABLISHED<-|from| 이후 연결 성립 후 데이터 전송|

      > SYN: Synchroizie
      > ACK: Acknowledgment

   - 데이터 전달 보증
      -> f(clinet) request for data transport -> t(server)f response for data transport -> t(client)
      비연결성을 보완한다.
   - 순서 보장 & 신뢰할 수 있는 프로토콜
      -> c 1,2,3 -> s 1,3,2 -> s 2,3 -> c 2,3 -> s 1,2,3
     - 패킷이 순서대로 도착하지 않아도 TCP 세그먼트에 있는 정보로 다시 패킷 전송 요청
2. User Datagram Protocol(UPD): 사용자 데이터그램 프로토콜은 IP프로토콜에 PORT, Checksum field정보만 추가된 단순한 프로토콜이다.
   > checksum: 중복 검사, 오류 정정을 통해 공간이나 시간속에서 송신된 자료의 무결성을 보호하는 단순한 방법
   - 하얀 도화지(기능 거의 없음)
   - 비연결지향성
   - 데이터 전달 보증못함
   - 순서 보장못함
   - 신뢰성 낮지만 속도가 빠름 -> 실시간 스트리밍
3. 차이

   |---|---|
   |TCP|UDP|
   |연결지향|X|
   |전송순서보장|X|
   |데이터수신여부확인|X|
   |신뢰성높고 속도느림|신뢰성 낮고 속도빠름|

## 4. OSI 7계층 모델

출처: [effortDev: OSI 7 계층이란?, OSI 7 계층을 나눈 이유](https://shlee0882.tistory.com/110)
![https://shlee0882.tistory.com/110](/assets/img/221109-osi7.jpg)

1. OSI 7 layers
   |---|---|
   |Layer(계층)|ex|
   |Application(응용)|HTTP, DNS, SSL, SMTP, FTP|
   |Presentation(표현)|GIF, JPEG, MPEG, MIME, ZIP, ASCll|
   |Session(세션)|Sockets, RPC, SQL, NETBOIS|
   |Transport(전송)|TCP, UDP, NETBEUI|
   |Network(네트워크)|IP, ICMP|
   |Data Link(데이터 링크)|FDDI, Ethernet, PPP|
   |Physical(물리)|CDMA, GSM, NICs, CSMA/CD, Fiber|
2. TCP/IP 4 layers
   |---|---|
   |Layer(계층)|osi layer concern|
   |Application|Application, Presentation, Session|
   |Transport|Transport|
   |Internet|Network|
   |Network Interface|Data Link, Physical|

International Oranization for Standardization(ISO), 국제표주놔기구에서 1984년 제정된 표준 규격이다. Apple이 라이트닝을 버리고 usb-c type을 선택한 것과 같이, 제조사에 상관없이 공통으로 사용할 수 있는 네트워크 표준 규격을 정의했다.

OSI 7계층을 따르면 원인이 어디에 있는지 범위를 좁혀 문제를 쉽게 파악할 수 있다.

1. Physical: 시스템간의 물리적 연결과 전기 신호를 변환, 제어하는 계층이다. 전기신호를 전달하는데 초점을 둔다.
2. Data Link: 네트워크 기기간 데이터 전송 및 물리주소를 결정하는 계층이다. 물리계층의 전기신호를 모아 알아볼 수 있는 데이터 ㅕㅇ태로 처리한다. 주소 정보를 정의, 출발지와 도착지 주소를 확인하여 데이터 처리를 수행한다.
3. Network: 가장 복잡한 계층 중 하나로 실제 네트워크 간 데이터 라우팅을 담당한다.
   > 라우팅: 어떤 네트워크 안에서 통신 데이터를 짜여진 알고리즘에 의해 최대한 빠르게 보낼 최적의 경로를 선택하는 과정
4. Transport: 컴퓨터간 신뢰성 있는 데이터를 주고받을 수 있도록하는 서비스를 제공하는 계층이다. 하위계층에서 올바른 위치로 보내고 신호를 만든다면, 해당 데이터들이 정상적으로 보내지는지 확인한다. 네트웨크 계층에서 사용되는 패킷의 순서가 바뀐다던가 유실되면 이를 바로잡는 역할 도 한다.
5. Session: 세션 연결의 설정, ㅐ제, 메세지 전송 등의 기능을 수행한다. 컴퓨터간의 통신 방식을 결정한다. 작업을 마친 후 연력을 끊는 역할도 한다.
6. Presentantion: Application Layer로 전달하거나 받는 데이터를 인코딩 또는 디코딩한다. 컴파일러 같은 역할이다.
7. Application: 사용자와의 인터페이스를 제공한다.

### 4-1. 데이터 캡슐화

데이터를 상대방에게 보낼 때 각 계층에서 필요한 정보를 header(data link -> trailer)로 추가하는 것을 캡슐화라고 한다. 받을 때는 캡슐화의 반대인 역캡슐화를 하여 응용계층에서 원본을 받는 상대방에게 전달한다.

## 5. TCP/IP 4 Layer

OSI 모델을 기반으로 현실에 맞게 단순화된 모델이다.

1. Network Interface: OSI계층의 물리, 데이터 링크에 해당하며, 물리적 주소는 MAC을 사용한다.
2. Internet: Network에 해당하며, 통신 Node간 IP packet을 전송 기능 및 라우팅을 한다.
3. Transport: 전송계층, 통신 노드간의 연결을 제어, 신뢰성있는 데이터 전송을 담당한다.
4. Application: 세션, 표현, 응용 계층이 해당한다. TCP/UDP 기반 응용 그로그램 구현 시 사용한다.
   - 사용자에게 인터페이스를 제공하는 계층으로 서비스를 사용자에게 제공한다. 애플리케이션은 서비스를 요청하는측에서 사용하는 애플리케이션과 서비스를 제공하는 측의 애플리케이션으로 분류된다. Clinet, Server라고 명하고, 둘다 응용 계층에서 동작한다.

---

## 참조

> [effortDev: tistory](https://shlee0882.tistory.com/110)   
> [wiki: osi model](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)   
> [wiki: internet protocol suite](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C_%EC%8A%A4%EC%9C%84%ED%8A%B8)   
> [wiki: tcp](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)   
> [wiki: udp](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)