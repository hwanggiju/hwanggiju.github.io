---
layout: single
title:  "Private 클라우드를 활용한 네트워크&서버 보안 운영 관리 - 네트워크 기초"
categories: "Education"
tag: [네트워크, 국비교육과정(Private 클라우드를 활용한 네트워크&서버 보안 운영 관리)]
---

# L3.IPv4.Routing 분야 복습 

## 일정

- 2022.12.05(월) ~ 

## 목차

1. [네트워크 기초](#네트워크-기초)
2. [Static Route](#static-route)
3. [Subnetting](#subnetting)
4. [Supernetting](#supernetting)
5. [DHCP Server](#dhcp-server)
6. [ACL](#acl)
7. [NAT](#nat)
8. [DHCP ACL NAT 최종 실습](#dhcp-acl-nat-최종-실습)
9. [Dynamic Routing](#dynamic-routing)
10. [괸리자 거리값](#괸리자-거리값)
11. [RIP EIGRP OSPF 축약 재분배 NAT 종합 실습](#rip-eigrp-ospf-축약-재분배-nat-종합-실습)
12. [Frame-Relay](#frame-relay)
13. [Filtering](#filtering)
14. [BGP](#bgp)

--------------------------------

### 네트워크 기초

- ip주소(집주소) = x.x.x.x = 10진수.10진수.10진수.10진수 = 8bit.8bit.8bit.8bit = 32bit = Network 주소자리(동) + Host 주소자리(번지)

- 8bit = 0000 0000
- 8bit = 1111 1111 = 128(2^7) 64(2^6) 32(2^5) 16(2^4) 8(2^3) 4(2^2) 2(2^1) 1(2^0) = 255
- [Classful Address] : 초창기 계층별 주소     

  |IPv4 = (?).10진수.10진수.10진수|Subnet Mask(1 = Network 주소 자리, 0 = Host 주소 자리)|
  |------------------------------|----------------------------------------------------|
  |A Class : 1 ~ 126|255.0.0.0 = /8|
  |B Class : 128 ~ 191|255.255.0.0 = /16|
  |C Class : 192 ~ 223|255.255.255.0 = /24|
  |D Class : 224 ~ 239(Multicast 주소)|<예> 224.0.0.0 = 인사부, 224.1.1.100 = 총무부|
  |E Class : 240 ~ 255(연구용)||
  
  --------------------------
  
  - _예1_
        
    - IP 주소 = 192.168.10.1
    - Subnet Mask = 255.255.255.0
    - Network 주소 = 192.168.10.0 (Host 주소 자리가 전부 0) <예> 청학동
    - Broadcast 주소 = 192.168.10.255 (Host 주소 자리가 전부 1) <예> 청학동에 있는 모든 집주소
    - 할당 가능한 주소 = 192.168.10.1 ~ 192.168.10.254
    - 주소 개수 = 2^8 - 2
             
  - _예2_
      
    - IP 주소 = 126.255.0.1
    - Subnet Mask = 255.0.0.0
    - Network 주소 = 126.0.0.0 (Host 주소 자리가 전부 0) <예> 청학동
    - Broadcast 주소 = 126.255.255.255 (Host 주소 자리가 전부 1) <예> 청학동에 있는 모든 집주소
    - 할당 가능한 주소 = 126.0.0.1 ~ 126.255.255.254
    - 주소 개수 = 2^24 - 2
               
  - _예3_
              
    - IP 주소 = 191.255.0.1
    - Subnet Mask = 255.255.0.0
    - Network 주소 = 191.255.0.0 (Host 주소 자리가 전부 0) <예> 청학동
    - Broadcast 주소 = 191.255.255.255 (Host 주소 자리가 전부 1) <예> 청학동에 있는 모든 집주소
    - 할당 가능한 주소 = 191.255.1.1 ~ 191.255.254.254
    - 주소 개수 = 2^16 - 2 
           
  - _예4_
                
    - IP 주소 = 223.0.255.254
    - Subnet Mask = 255.255.255.0
    - Network 주소 = 223.0.255.0 (Host 주소 자리가 전부 0) <예> 청학동
    - Broadcast 주소 = 223.0.255.255 (Host 주소 자리가 전부 1) <예> 청학동에 있는 모든 집주소
    - 할당 가능한 주소 = 223.0.255.1 ~ 223.0.255.254
    - 주소 개수 = 2^8 - 2
            
  - _예5_
                         
    - IP 주소 = 128.0.0.1
    - Subnet Mask = 255.255.0.0
    - Network 주소 = 128.0.0.0 (Host 주소 자리가 전부 0) <예> 청학동
    - Broadcast 주소 = 128.0.255.255 (Host 주소 자리가 전부 1) <예> 청학동에 있는 모든 집주소
    - 할당 가능한 주소 = 128.0.1.1 ~ 128.0.254.254
    - 주소 개수 = 2^16 - 2

  ※ __0.x.x.x (x) / 127.0.0.1(Loopback주소 = 자기자신)__ 
  
- IPv4 통신 방법 : unicast(1:1), multicast(1:Group), broadcast(1:다)
- Network 주소가 같은 경우

  - PC to PC, PC-HUB-PC, PC-SWITCH-PC, Router to Router
  
    |PC1|PC2|통신 유무|
    |---|---|--------|
    |192.168.10.1/24|192.168.20.1/24|x|
    |126.255.0.1/8|126.0.255.1/8|o|
    |191.0.255.1/16|191.255.0.1/16|x|
    |223.0.0.1/24|223.0.1.2/24|x|
    |192.168.10.1/24|192.168.10.2/24|o|

- Network 주소가 다른 경우

  - PC-Router-PC
  
    |PC1|(Router)|PC2|통신 유무|
    |---|--------|---|---------|
    |1.1.1.1|1.1.1.2 <--> 1.1.1.3|1.1.1.4|x|
    |1.1.1.1|1.1.1.2 <--> 2.1.1.2|2.1.1.1|o|

- Network 연결 실습 (윈도우)

![image](https://user-images.githubusercontent.com/84834776/205583931-f30870b8-a50d-4c67-a870-fdb16b530f2b.png)

1. 윈도우 pc 서버 on
2. 라우터 on
3. 라우터 게이트웨이와 서브넷 마스크 지정
4. 윈도우 pc 서버 설치
5. 윈도우 pc 서버 ip 지정(실행 -> ncpa.cpl -> 속성 -> 인터넷 프로토콜(TCP/IP) -> ip 주소 기입)
6. 각 pc 서버에서 ping 확인

- Network 연결 실습 (리눅스)

![image](https://user-images.githubusercontent.com/84834776/205790488-833ac666-f2bd-430f-876b-a3a6a7525411.png)

1. 리눅스 pc 서버 on
2. 라우터 on
3. 라우터 게이트웨이와 서브넷 마스크 지정
4. 리눅스 pc ip 지정 (노랑색 박스 순서와 같이 명령어 실행)
5. 각 pc 서버에서 ping 확인

----------------------------------

### Static Route

![image](https://user-images.githubusercontent.com/84834776/205839433-6baa3dc1-ecfd-4b03-b611-9fafd9e86431.png)

- Router 장비 : 다른 Network 주소 연결 + 지도 관리
- Static Routing : ip route 명령어 (유형 1 : 이웃 주소 지정, 유형 2 : 자신의 Local interface 지정 )

  - 실습 1 (유형 1)
  
  ![image](https://user-images.githubusercontent.com/84834776/205849493-1f4b905f-5f61-4d81-b6ef-d8b4306f4fbd.png)
  
  - 실습 2 (유형 1)

  ![image](https://user-images.githubusercontent.com/84834776/206059996-1f92ebdc-e020-4b96-8b8e-f9a5891741b0.png)

  - 실습 3 (no ip route 명령어)

  ![image](https://user-images.githubusercontent.com/84834776/206070274-152dc5c9-4360-48fd-b18f-2f0f103b8f79.png)

- no ip route 명령어 : 라우터 ip 삭제 명령어

- 루핑(Looping) ; 모르는 주소일 때 default 경로 지정, 잘못된 주소 지정

  ![image](https://user-images.githubusercontent.com/84834776/206090249-37fc1dc9-670c-47e7-bd05-0861e90f8607.png)
  
- 실습 4 (유형 2)

  ![image](https://user-images.githubusercontent.com/84834776/206098797-27389c4a-bc15-4a3a-abea-60569fdcd22e.png)

- Dynamic Routing : RIP, EIGRP, OSPF, BGP

----------------------------------

### Subnetting

- 장점
  1. 비용(IP 주소 임대) 절감
  2. 공인주소 절약
  3. 보안

- 1개의 Network 주소를 여러개의 Network 주소로 만들기
- <예1> 
  - 192.168.10.1 255.255.255.0 -> 192.168.10.0
  - 126.1.1.1 255.0.0.0 -> 126.0.0.0
  - 126.1.1.1 255.255.0.0 -> 126.1.0.0
  - 126.1.1.1 255.255.255.0 -> 126.1.1.0
- <예2>
  - 126.1.1.1/8 - 126.2.2.2/8 = 통신 o
  - 126.1.1.1/16 - 126.2.2.2/16 = 통신 x

- Subnetting 방법 1 : Network 주소 개수 선정
  - 2^0 = 1개, 2^1 = 2개, 2^2 = 4개, 2^3 = 8개, ...
  - 255.255.255./0000 0000/ -> 네트워크 개수에 맞춰 Subnet mask 왼쪽 0부터 차례로 1 up 
  - 실습
  
    ![image](https://user-images.githubusercontent.com/84834776/206351815-c61e12e5-d0f8-4bcb-91e7-44929801889c.png)

- Subnetting 방법 2 : Host 주소 개수 선정
  - 주소 개수가 가장 많은 것 선정

    > 120개
    - 2^7 = 128 / 255.255.255./1000 0000/ (128)
    - 192.168.10.0 ~ 192.168.10.127

    > 60개 
    - 2 ^ 6 = 64 / 255.255.255./1100 0000 (192)
    - 192.168.10.128 ~ 192.168.10.191

    > 6개 
    - 2 ^ 3 = 8 / 255.255.255./ 1111 1000 (248)
    - 192.168.10.192 ~ 192.168.10.199

    > 6개 
    - 192.168.10.200 ~ 192.168.10.207

  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/206367458-b485bd87-933e-4ca5-98a9-fdcc99b4af82.png)
    
----------------------------------

### Supernetting

- 여러 개의 Network 주소를 1개의 Network 주소로 만들기
- <예1>
  - 126.1.0.0/16, 126.2.0.0/16 , 126.3.0.0/16 => 126.0.0.0/8
- Supernetting 방법

  ![image](https://user-images.githubusercontent.com/84834776/206966572-f2371142-05b8-445f-8610-a48faf0bb6a4.png)

  - 축약 x
  
  ![image](https://user-images.githubusercontent.com/84834776/206967113-db7fd054-e1aa-4ffd-9bff-12133c5b304a.png)

  - 하나의 라우터 인터페이스에 여러 주소 넣어주는 방법
    - ip route (ip 주소) (Subnet Mask) secondary 입력

  - 축약 o
 
  ![image](https://user-images.githubusercontent.com/84834776/206967381-4cb9e534-49a7-46c6-bc86-9199beca42ae.png)
  
  - 실습
  
  ![image](https://user-images.githubusercontent.com/84834776/206974552-97d95104-69e3-4c42-8f2e-ef553c99af57.png)
  
  
----------------------------------
  
### DHCP Server

- 서버(Sever) : 서비스 제공 <예> DHCP Server(IP 주소 제공)
- 클라이언트(Client) : 서비스 요청 <예> DHCP 클라이언트(IP 주소)

- 윈도우 [HTTP 서버 환경 구축, DNS 서버 환경 구축]
  - step 1. 제어판 > 프로그램 추가/제거 > windows 구성 요소 추가/제거 > 네트워킹 서비스 > DNS(도메인 이름 시스템) 체크 : DNS 설치

    ![image](https://user-images.githubusercontent.com/84834776/207238757-8331182b-eadb-43ea-bb23-03b82f1bf84f.png)

  - step 2. 제어판 > 프로그램 추가/제거 > windows 구성 요소 추가/제거 > 응용 프로그램 서버 > 인터넷 정보 서비스(IIS) 체크 : HTTP 설치
  
    ![image](https://user-images.githubusercontent.com/84834776/207238918-238665e9-f8d7-44d1-9ec2-035963b80b84.png)

  - step 3. 관리도구 > DNS 서버 > 정방향 조회 영역 > 새 영역 > 영역 이름 지정 > 새 호스트 www, IP 주소 연결
  
    ![image](https://user-images.githubusercontent.com/84834776/207240033-49ee923a-643f-4368-9c8e-f402c78b3061.png)

  - step 4. 관리도구 > 인터넷 정보 서비스(IIS) 관리 > 로컬 컴퓨터 > 웹 사이트 > 기본 웹 사이트 > 속성 > 문서(기본 콘텐트 페이지 사용) > 웹 페이지 파일 생성 및 홈 디렉터리에 저장
  
    ![image](https://user-images.githubusercontent.com/84834776/207240964-68fb9577-b3e1-4815-9d6f-cad786f3c5a5.png)

- 실습

  ![image](https://user-images.githubusercontent.com/84834776/207249369-c003198b-906f-40e7-b613-09a2dae33a39.png)

- 각 PC MAC 주소를 L2 기반으로 IP 주소를 Router에 요청하고, L3를 기반으로 Router에서 IP 주소를 자동으로 할당해준다.
- DHCP Relay Agent

  ![image](https://user-images.githubusercontent.com/84834776/207257236-c12358aa-2a3b-454b-a4f0-14bee8d86d7b.png)
  
- 실습 2

  ![image](https://user-images.githubusercontent.com/84834776/207491110-2f5c4907-4937-42f7-ac1a-88e237b25c64.png)

  - Switch 전원 켜도 열어서 부팅할 것 !!!!!! (되는 것도 있고 안되는 스위치도 있음...)

- 예약 Host 주소 지정
  - Router 자동 할당된 주소 확인 명령어 : show ip dhcp binding
  - Router 자동 할당된 주소 해제 명령어 : clear ip dhcp binding *
  - Router 주소 충돌 확인 명령어 : show ip dhcp conflict
  - 리눅스 : hardware-address (MAC 주소)
  - 윈도우 : client-identifier (MAC 주소)
  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/207537479-eea5ea08-fdfa-4881-ba79-71e8935ab34d.png)

- DHCP Server : Broadcast 통신 (L2 주소 : FFFF.FFFF.FFFF, L3 주소 : 255.255.255.255) 
- DHCP Server - DHCP Relay Agent : Unicast 통신(일대일 통신 방식)

  - step 1. DHCP Discover : 출발지(MAC1/0.0.0.0) - 목적지(FFFF.FFFF.FFFF/255.255.255.255)

    ![image](https://user-images.githubusercontent.com/84834776/207523700-b47e4d9e-9253-40af-b936-9cf8815e5a30.png)

  - step 2. DHCP Offer : 출발지(MAC2/192.168.10.254) - 목적지(MAC1/255.255.255.255), Payload(IP,S/M,G/W,DNS,임대)

    ![image](https://user-images.githubusercontent.com/84834776/207523800-68602dd3-dfe1-448b-a739-62409e40f570.png)
    
    - Payload에서 제안한 IP 주소룰 목적지(클라이언트) IP 주소로 출력 (※ 실제로는 255.255.255.255로 보내짐.)
    
  - step 3. DHCP Request : 출발지(MAC1/0.0.0.0) - 목적지(MAC2/255.255.255.255), Payload(위와 같음)

    ![image](https://user-images.githubusercontent.com/84834776/207523847-cceb2644-9e10-40bc-a6b1-1080361d4a64.png)
    
  - step 4. DHCP ACK : 출발지(MAC2/192.168.10.254) - 목적지(MAC1/255.255.255.255), Payload(위와 같음)

    ![image](https://user-images.githubusercontent.com/84834776/207523951-cc1d3215-c82b-4a73-bfa7-00be19527c71.png)
    
    - Payload에서 제안한 IP 주소룰 목적지(클라이언트) IP 주소로 출력
    
- TCP / UDP
  - 포트 간 통신 : DHCP UDP 디폴트 포트 67번 / DHCP Client UDP 디폴트 포트 68번 / HTTP 서버 TCP 디폴트 포트 80번 
  - 포트 번호는 변경 가능

- ARP (IP -> MAC)
  - 목적지 간의 IP(L3) 주소를 MAC(L2) 주소로 매핑 시켜주는 프로토콜
  - arp -a 명령어 : pc의 ip와 mac 주소 매핑 정보 확인

- RARP (MAC -> IP)
  - 목적지 간의 MAC(L2) 주소를 IP(L3) 주소로 역으로 매핑 시켜주는 프로토콜
    1. 처음 목적지 IP는 알고있지만, MAC 주소를 모르는 상태에서 FFFF.FFFF.FFFF 전송
    2. 목적지에서 출발지의 IP주소와 MAC 주소 정보를 확인하고, 목적지의 IP주소와 MAC 주소를 다시 출발지에게 전송
    3. 출발지와 목적지의 ARP 매핑, 이후 ping 전송 시 목적지 MAC 주소를 정확한 주소로 전송하게 됨.

- Wireshark를 사용하여 DHCP 서버와 클라이언트 사이 기본 통신 과정 실습
  
  ![image](https://user-images.githubusercontent.com/84834776/207772387-6212f72c-dce7-464d-ac90-11c3184e415c.png)


----------------------------------

### ACL

- Access Control List(ACL)
- 라우터의 방화벽
- 엑세스 리스트 제어방법에 따른 분류
  - Standard Access List : 출발지 주소만 참고 (숫자 1 - 99)
  - Extended Access List : 출발지, 목적지, 프로토콜, 사용 포트 번호 참고 (숫자 100 - 199)

- Standard Access List
  - 실습 1 (Standard Access List)

    ![image](https://user-images.githubusercontent.com/84834776/207785774-f38c6284-9579-46b0-adf1-83a3c970522b.png)

  - 실습 2 (Standard Access List)

    ![image](https://user-images.githubusercontent.com/84834776/207802709-3ebf109b-1cda-48a1-90e0-328e58c289f0.png)
  
- Extended Access List
  - 실습 1 (Extended Access List)
    
    ![image](https://user-images.githubusercontent.com/84834776/208335973-7cd8494f-9fcc-4eb4-a928-c4da505fa619.png)
  
  - 실습 2 (Extended Access List)

    ![image](https://user-images.githubusercontent.com/84834776/208336026-d51da6ac-ecf9-4101-b0ec-c3cd4096e4c4.png)

  - 실습 3 (Extended Access List)
  
    ![image](https://user-images.githubusercontent.com/84834776/208336645-bdf0c2aa-2bea-405b-9eaa-6607cc39ab3b.png)
    

----------------------------------

### NAT

- Network Address Translation(NAT)
- IP주소 변환
  - 사설 주소 돈 x, 공인 주소 돈 o
  - 사설 주소를 공인 주소로 변환 : 내부 -> 외부 
  - 공인 주소를 사설 주소로 변환 : 외부 -> 내부

- 실습 1
  
  ![image](https://user-images.githubusercontent.com/84834776/208359834-ecc37093-ad0e-4350-981c-02677eff5dde.png)
  
  > PAT(Port Address Translation), Static NAT
    - 단계 1. 할당 받은 공인 주소 라우터에 연결 (ip nat pool cisco (할당받은 주소 범위) netmask (SubnetMask))
    - 단계 2. 내부 사설 주소 ACL
    - 단계 3. 외부 주소와 내부 주소 연결 (ip nat inside source list (ACL 번호) pool (cisco) overload)
           
  > Static NAT 
    - 단계 1. 내부 IP 변환할 IP 주소 정적으로 입력
          
  - 최종. 라우터 인터페이스 내부 외부 설정
  
- 실습 2

  ![image](https://user-images.githubusercontent.com/84834776/208370676-23c4814e-4edd-4eff-9279-74d6af7a69d8.png)
  
- 실습 3

  ![image](https://user-images.githubusercontent.com/84834776/208601659-14b0d5d7-d4b4-4d2d-b7ed-0454cc52a0f9.png)
  
  - 목표 : HTTP-B로 오는 외부 주소 1.1.34.10, 웹 통신 가능, HTTP-A로 오는 외부 주소 10.1.1.1
  - R3 라우터 2중 NAT 설정
  - 가상 IP 주소 생성 (loopback)
    - interface loopback 0
    - ip address 10.1.1.1 255.255.255.0

----------------------------------

### DHCP ACL NAT 최종 실습

  ![image](https://user-images.githubusercontent.com/84834776/208798455-a8b40c5c-26c4-4be5-8a20-68cd09a154ce.png)


----------------------------------

### Dynamic Routing
- 라우터의 지도를 교환
- RIP(R), EIGRP(D, D EX), OSPF(O, OIA, E1/E2, N1/N2) : 내부 라우터들을 연결시켜 주는 역할   =>  BGP (B) : 내부 라우터를 하나로 통합시켜 주는 역할
> RIP Protocol : Classful Network 주소까지만 인식, 소규모 네트워크에서 활용
  - RIPv2 Protocol [120/3]
    - 관리자 거리값(Administrative Distance) : 120
    - Metrix : 15 Hop, 16 Hop(목적지 도달 x)
    - Code : R
    - Update : 30초 <예> clear ip route *

    ![image](https://user-images.githubusercontent.com/84834776/208831018-234fad91-f016-46b7-839c-6a9538fa7cc0.png)

  - auto-summary : 자동 축약 / no auto-summary : 축약 x

    ![image](https://user-images.githubusercontent.com/84834776/208838285-b4de1300-97a0-4079-8964-2c2643efb07e.png)

  - 원하는 RIP 버전으로 주고 받기 실습

    ![image](https://user-images.githubusercontent.com/84834776/209598102-65986cdf-95bc-4f96-bd5a-e878146c2946.png)

  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/209036150-f9c3ac6a-8f54-4ed1-90d5-09130d9e361b.png)

> EIGRP Protocol
  - 관리자 거리값(Administrative Distance) : 90(D), 170(D EX)
  - Metrix : B, D, R, L, M
  - Code : D(같은 AS), D EX(재분배)
  - Update : 순간 
  - FD(Feasible Distance) : 자신을 중심으로 목적지까지의 Metric
  - AD(Advertised Distance) : 자신의 다음 라우터(next hop)로부터 목적지까지의 Metric
  - Sucessor
  - Feasible Sucessor

  ![image](https://user-images.githubusercontent.com/84834776/209040581-ac7a482f-7085-4f68-b8c6-ea4f5423f142.png)

  - EIGRP unequal loadbalancing 실습

    ![EIGRP unequal loadbalancing](https://user-images.githubusercontent.com/84834776/209616085-d1b0b445-89bd-40d9-8b33-88aa1d58d867.jpg)
    
  - EIGRP에서 0.0.0.0 전달 방법

    ![EIGRP에서 0 0 0 0 전달 방법](https://user-images.githubusercontent.com/84834776/209627091-f7944873-36b0-4e00-b1cf-0f41a3bce5fb.jpg)
    
  - EIGRP에서 축약을 이용한 0.0.0.0 전달(복습)

    ![EIGRP에서 축약을 이용한 0 0 0 0 전달(복습)](https://user-images.githubusercontent.com/84834776/209746640-2033c09d-73ff-413b-bb4d-2ecf22faad9b.jpg)

  - no ip domain-lookup : 명령어 잘못 입력 시 도메인에게 물어보지 않고 바로 처리
  
> OSPF Protocol
  - AREA가 하나 이상인 경우 AREA 0 (Back-Born Network)가 있어야 함.
  - 모든 AREA가 AREA 0에 물리적으로 붙어있어야 함.
  - OSPF는 기본 구성시 Loopback 주소를 /32로 넘김
  - OSPF 구성 시 Loopback 주소를 /24로 넘김
    - interface lo 0
    - ip ospf network point-to-point

  - 관리자 거리값(Administrative Distance) : 110
  - Metrix : Cost
  - Code : O(같은 AS), OIA(다른 Area), E1/E2/N1/N2(재분배)
  - Update : 순간

    ![image](https://user-images.githubusercontent.com/84834776/209053348-7646f667-d2d3-4a53-bc1c-667cbc6b9056.png)
    
  - OSPF DR/BDR/DROther
  
    - LSA 중계 역할을 하는 라우터를 DR(Designated Router) 이라고 하며, DR에 장애가 발생하면 대신 DR 역할을 하는 라우터를 BDR(Backup DR) 이라고 한다.

    - DROther 간에는 라우팅 교환 x

  - OSPF DR/BDR/DROther 선출 순서
    
    - 스템 1. OSPF 우선순위가 가장 높은 라우터가 DR이 된다. 다음 순위의 라우터가 BDR이 된다.

    - 스텝 2. OSPF 우선순위가 모두 동일하면(기본값 1), 라우터 ID가 높은 것이 DR, 그 다음이 BDR이 된다.

    - 스텝 3. 한 번 DR/BDR이 선출되면 더 높은 우선순위의 라우터가 추가되어도 라우터를 재부팅하거나 clear ip ospf process
명령어를 사용하기 전에는 DR/BDR을 다시 선출하지 않는다.

    - 스텝 4. DR이 다운되면 BDR이 DR이 되고, BDR을 새로 선출한다. BDR이 다운되면 BDR을 새로 선출한다.
    
    ![image](https://user-images.githubusercontent.com/84834776/209773192-09c6bfb9-80fa-4514-92e1-6f9a4d65d38e.png)
    
  - OSPF 축약

    ![image](https://user-images.githubusercontent.com/84834776/209902843-b54ee647-c412-4b77-9a99-f89f6384e0a8.png)
    
    > ASBR 축약
      - router [protocol]
      - summary-address 축약 네트워크 서브넷마스크

    > ABR 축약
      - router [protocol]
      - area * range 축약 네트워크 서브넷마스크

  - OSPF Default Route 생성 하기

    1. default-information originate always 입력
    2. static 라우터 연결 후 default-information originate 입력

  - OSPF Virtual-link

    ![image](https://user-images.githubusercontent.com/84834776/210036939-1b5b1880-e4b7-48e0-a9b8-ec6432494807.png)
    
    - router-id x.x.x.x
    - area [number] virtual-link x.x.x.x
    - 주의 : router-id를 먼저 지정해주어야 함.

  - OSPF LSA 종류
    
    ![image](https://user-images.githubusercontent.com/84834776/210044565-6ea3d117-a7fd-4b12-bcc4-34228322b997.png)
    
    - 링크 상태 데이터베이스는 에어리어별로 관리되며, 동일한 에어리어에 소속된 내부 라우터들의 링크 상태 정보 데이터베이스 내용은 모두 동일
    - LSA 들은 30 분마다 LSA 전체 정보를 전송하는 LSA Refresh 를 한다 무결성
    
- AD 값 (Administrative Distance)
  - RIPv2(120) < OSPF(110) < EIGRP(90, 170, 5) < Static route(1) < Connected(0)

- 재분배
  
  > RIP
    - router rip
    - redistribute [프로토콜] metric [1 ~ 15]

  > EIGRP
    - router eigrp 100
    - redistribute [프로토콜] metric [bandwidth] [delay] [ 신뢰도 ] [load] [MTU]

  > OSPF
    - router ospf 1
    - redistribute [프로토콜] { subnets(defaul 값 ) metric 20(defaul 값 ) } <- 생략가능

  ![image](https://user-images.githubusercontent.com/84834776/209276028-20f7479c-eb91-44f0-b8b3-1e1ce81bf7df.png)

- 실습 1

  ![image](https://user-images.githubusercontent.com/84834776/209286221-41309c71-fa6c-4771-be7b-d90aeebcb7b3.png)
  - 방법 1. 네트워크 주소 할당 (기존 방식)
  - 방법 2. 라우터에 물리적으로 연결된 주소 연결 (redistribute connected metric *)
  - 방법 3. 정적 할당 후 연결 (redistribute static metric *)

- 실습 2

  ![image](https://user-images.githubusercontent.com/84834776/209488689-61df59dc-a767-4426-9491-e68e002df09d.png)

----------------------------------


### 괸리자 거리값

- Administrative Distance(AD)
- 특정 라우터에서 AD값을 조정하면 해당 라우터에서만 영향을 미치며, 다른 라우터로 조정한 AD값이 전달되지 않는다.
- 관리자 거리값 조정
- clear ip eigrp neighbor * : 모든 이웃된 라우터 해제하고 재연결
  
  ![image](https://user-images.githubusercontent.com/84834776/209507230-0ed3df97-153c-4b1c-b311-2a9649b24877.png)

  > RIP
    - router rip
    - distance rip 220

  > EIGRP
    - router eigrp 100
    - distance eigrp 80 120

  > OSPF
    - router ospf 1
    - distance ospf 150

----------------------------------

### RIP EIGRP OSPF 축약 재분배 NAT 종합 실습
  ![image](https://user-images.githubusercontent.com/84834776/210472174-405b21f0-6ffa-44c7-ac8f-5e592aee81d0.png)
  
  
----------------------------------

### Frame-Relay

  - Point-to-Point Frame-Relay
    - show frame-relay map : frame-relay 지도 확인 명령어
    - Frame-Relay 2계층 전송 역할 뿐 (frame-relay에서 지도 확인 명령어 : show frame-relay route)

      ![image](https://user-images.githubusercontent.com/84834776/210493333-4135438c-c53d-4e4f-9317-8833c7fab70f.png)

    - DCE : 클럭 신호를 보내는 곳 (FR interface s1/0, s1/1, s1/2)
    - DTE : 클럭 신호를 받는 곳 (R1 interface s1/0, R3 interface s1/1, R4 interface s1/2)

  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/210685796-300d7e39-ef94-4f2b-90d7-848eacab83b2.png)

  - Multipoint Frame-Relay
    
    ![image](https://user-images.githubusercontent.com/84834776/210687417-93144a8b-af05-4dc2-92ec-b08354037f8f.png)

  - ip split-horizon : 루핑 방지 명령어

    - hub and spoke topology (부분메시)
    - ip split-horizon 상태일 때, 부분 메시에서 dhcp로 라우팅 교환이 인터페이스에서 전달되지 못함 -> no ip split-horizon 명령어로 해제
    - RIP / EIGRP

      ![image](https://user-images.githubusercontent.com/84834776/210717821-65bbbdac-3d72-489a-8c74-508c0400ee16.png)
    
    - OSPF

      1. 논브로드캐스트 네트워크에서의 OSPF 설정

        ![image](https://user-images.githubusercontent.com/84834776/210719645-4042221c-9080-4c6f-b2bd-9de34863768c.png)
        
        - 네트워크 타입 일치
        - 네이버 수동 지정
      
      2. 브로드캐스트 네트워크에서의 OSPF 설정

        ![image](https://user-images.githubusercontent.com/84834776/210723514-a2757565-8112-4697-a241-997bf5d06300.png)

        - 네트워크 타입 일치
        - 네이버 자동 지정

      3. 포인트 투 멀티포인트 네트워크에서의 OSPF 설정 (가장 빠름.)

        ![image](https://user-images.githubusercontent.com/84834776/210723802-bcd5c712-0f9b-47c3-8570-b7cc8fb9a492.png)

         - 네트워크 타입 일치
  
  - Frame-Relay / DHCP(OSPF, EIGRP) / 재분배 / NAT / DNS 실습

    ![image](https://user-images.githubusercontent.com/84834776/210918399-83b3f26f-f760-40ae-8111-198c81fc6f82.png)

    - 실습하면서 까먹었던 부분 : 리눅스 웹 서버 구축 명령어(service httpd restart), 리눅스 DNS 주소 설정할 때 주소 입력 변수가 뭐였는지 까먹어서 찾아보았다.
    - 실습하면서 몰랐던 부분 : PAT 공인주소 loopback으로 설정 후 라우팅하면 된다.

----------------------------------

### Filtering

  - 이론

    1. prefix-list 는 대소문자 구분한다.
    2. 명령어 구조 : ip prefix-list NETS (seq 7) deny x.x.x.x/(subnetmask 길이)
    3. prefix-list 확인 명령어 : show ip prefix-list
    4. ge(greater or equal) - 같거나 클 때 (서브넷 마스크 길이), le(less or equal) - 같거나 작을 때 (서브넷 마스크 길이)
    5. RIP, EIGRP 등과 달리 OSPF 에서는 라우팅 정보를 인터페이스에서 송신할 때에는 차단할 수 없다.
    6. 필터링 명령어 : distribute-list 명령어
    7. route-map 필터 순서는 ACL에서 필터되면 permit만 넘어가고, deny는 버려진 후 route-map에서 필터가 되는 구조이다.  

  - 실습
    
    * prefix로 조건 지정
    
      ![image](https://user-images.githubusercontent.com/84834776/210937799-9ed8b26b-f9ce-480f-aaa6-ba536444256a.png)
    
    * Numbered-ACL로 조건 지정
      
      ![image](https://user-images.githubusercontent.com/84834776/210937413-4fa0a84e-873a-41f3-8db3-b04da76b4603.png)
      
      - Numbered-ACL 지정하는 방식 한번 더 복습하기.
      
    * Named-ACL로 조건 지정

      ![image](https://user-images.githubusercontent.com/84834776/210947725-bbbf5c33-084c-4037-8b50-be942066af55.png)
      
      - Named-ACL 지정하는 방식 한번 더 복습하기.
      
    * route-map 필터링

      ![image](https://user-images.githubusercontent.com/84834776/210947321-95606eff-f304-4f12-b045-b34b254b2075.png)

    * prefix-list 조건을 사용하여 route-map으로 필터링 실습

      ![image](https://user-images.githubusercontent.com/84834776/211227186-9cc4426f-9afe-4d50-b6bc-338c1e454db0.png)
      
      - 조건

      1. R1에서 route-map 2개의 명령어를 통해 192.168.10.0/24 만 거부하고 나머지는 전부 허용하게 설정한다.
      2. 단, prefix-list 조건 지정은 전부 permit만 사용한다.    
      <br/>
      
      - 문제 해결

      1. 먼저, 각 라우터의 인터페이스에 주소를 넣어준다.
      2. OSPF AREA 0 으로 DHCP 라우팅 연결을 시켜준 후 ping으로 연결 상태를 확인해준다.
      3. prefix-list 명령어로 192.168.10.0/24를 permit한 후, route-map cisco deny 10을 설정하고 prefix-list로 지정한 조건과 match 시켜준다.
      4. <span style='background-color:#F7DDBE'><*이 문제의 핵심*></span> route-map cisco [permit] 20을 설정한 후, 아무런 match와 set이 없다면 '나머지 모든 네트워크는 별도의 수정없이 그대로 허용'하라는 의미로 조건을 지정해준다.
      5. 결과적으로 첫번째 조건으로 192.168.10.0 네트워크는 거부되어지고, 두번째 조건으로 모든 네트워크가 허용된다.
      <br/>
      
      - 결과 (show ip route)
        
        ![image](https://user-images.githubusercontent.com/84834776/211228420-5e2f1f9a-cd4b-41d1-ad34-97aa3e0f7b92.png)
  
    * 라우팅 프로세스 간 네트워크 필터하기 
      
      - Route-map 이용해 필터하기
      
        ![image](https://user-images.githubusercontent.com/84834776/211233666-00f9ab63-67b8-49ee-8259-11090a3ab225.png)
  
      1. 이전에 아무 조건없이 기본 재분배를 하게되면, 모든 네트워크 정보를 교환할 수 있었다.
      2. 여기서는 원하는 네트워크만 넘겨주기 위해 prefix-list로 조건을 설정하고 route-map으로 필터링하여 재분배하게 된다면, 조건에 해당하는 네트워크만 허용하거나 거부하게 할 수 있다.
  
      - Route-map Tag 이용해 필터하기
  
        ![image](https://user-images.githubusercontent.com/84834776/211243145-813ff744-8fc8-44cd-9848-608d71c493b1.png)

      1. OSPF에서 set 명령어로 태그를 달아 네트워크를 넘겨주고, R3에서 show ip eigrp topology [네트워크 주소] 태그가 달린 것을 확인해본다.
      2. 여기서 주의해야 할 점은 ospf에서 1.1.12.0 네트워크를 태그 달아서 보내줄 때, eigrp에서 와일드 마스크 없이 1.0.0.0으로 보내주면 1.1.12.0 네트워크도 1.0.0.0 네트워크에 속하기 때문에 eigrp로 다시 재분배되어 태그없이 전달하게 되고, R4에 1.1.12.0 네트워크 정보가 전달된다.
      3. 따라서 ospf에 태그가 달린 정보를 정확히 전달하기 위해서 eigrp에서 와일드 마스크를 지정해 정확한 네트워크만 정보 전달할 수 있게 지정해야한다.
  
----------------------------------

### BGP
  


        
        
      
    
    







