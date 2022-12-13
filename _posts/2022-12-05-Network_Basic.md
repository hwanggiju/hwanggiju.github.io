---
layout: single
title:  "Private 클라우드를 활용한 네트워크&서버 보안 운영 관리 - 네트워크 기초"
categories: "Network"
tag: [네트워크, Subnetting, Supernetting, 국비교육과정(Private 클라우드를 활용한 네트워크&서버 보안 운영 관리)]
---

# L3.IPv4.Routing 분야 복습 

## 일정

- 2022.12.05(월) ~ 

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
  
### DHCP Server

- 서버(Sever) : 서비스 제공 <예> DHCP Server(IP 주소 제공)
- 클라이언트(Client) : 서비스 요청 <예> DHCP 클라이언트(IP 주소)

- 윈도우 [HTTP 서버 환경 구축, DNS 서버 환경 구축]
  1. 제어판 > 프로그램 추가/제거 > windows 구성 요소 추가/제거 > 네트워킹 서비스 > DNS(도메인 이름 시스템) 체크 : DNS 설치

    ![image](https://user-images.githubusercontent.com/84834776/207238757-8331182b-eadb-43ea-bb23-03b82f1bf84f.png)

  2. 제어판 > 프로그램 추가/제거 > windows 구성 요소 추가/제거 > 응용 프로그램 서버 > 인터넷 정보 서비스(IIS) 체크 : HTTP 설치
  
    ![image](https://user-images.githubusercontent.com/84834776/207238918-238665e9-f8d7-44d1-9ec2-035963b80b84.png)

  3. 관리도구 > DNS 서버 > 정방향 조회 영역 > 새 영역 > 영역 이름 지정 > 새 호스트 www, IP 주소 연결
  
    ![image](https://user-images.githubusercontent.com/84834776/207240033-49ee923a-643f-4368-9c8e-f402c78b3061.png)

  4. 관리도구 > 인터넷 정보 서비스(IIS) 관리 > 로컬 컴퓨터 > 웹 사이트 > 기본 웹 사이트 > 속성 > 문서(기본 콘텐트 페이지 사용) > 웹 페이지 파일 생성 및 홈 디렉터리에 저장
  
    ![image](https://user-images.githubusercontent.com/84834776/207240964-68fb9577-b3e1-4815-9d6f-cad786f3c5a5.png)

    
