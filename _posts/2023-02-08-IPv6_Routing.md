---
layout: single
title:  "Private 클라우드를 활용한 네트워크&서버 보안 운영 관리 - IPv6_Routing"
categories: "Education"
tag: [네트워크, 국비교육과정(Private 클라우드를 활용한 네트워크&서버 보안 운영 관리), IPv6_Routing]
---

# IPv6_Routing
## 일정
  - 2023.02.08(수) ~ 2023.2.10

### IPv6 Address

#### 📝 이론
  
  **IPv4** \
  = x.x.x.x \
  = 8bit.8bit.8bit.8bit \
  = 32bit \
  = 10진수.10진수.10진수.10진수 \
  = 192.168.10.1 \
  = broadcast 주소 = 255.255.255.0 \
  = loopback 주소 = 127.0.0.1 \
  = 주소없음 = 0.0.0.0 \
  = 192.168.10.1 = 네트워크 자리(192.168.10.0) + 호스트 자리(1)

  A Class(1-126), B Class(128-191), C Class(192-223) // D Class(224-239), E Class(240-255)

  통신방법 : Unicast(1:1), Multicast(1:Group), Broadcast(1:N)

  **IPv6** \
  = x : x : x : x : x : x : x : x \
  = 16bit.16bit.16bit.16bit.16bit.16bit.16bit.16bit \
  = 128bit \
  = 16진수 : 16진수 : 16진수 : 16진수 : 16진수 : 16진수 : 16진수 : 16진수 \
  = 2011 : 2022 : 2033 : 2044 : 2055 : 2066 : 2077 : 2088 \
  = broadcast 주소 = FFFF.FFFF.FFFF.FFFF.FFFF.FFFF.FFFF.FFFF \
  = loopback 주소 = ::1 \
  = 주소없음 = ::
  = 2011 : 2022 : 2033 : 2044 : 2055 : 2066 : 2077 : 2088/64 = 네트워크 자리(2011 : 2022 : 2033 : 2044) + 호스트 자리(2055 : 2066 : 2077 : 2088)

  글로벌 주소 = 2000 ~ 3FFF:: \
  사이트 로컬 주소 = FEC0 ~ FEFF:: \
  링크 로컬 주소 = FE80 ~ FEBF::   // 같은 물리적인 네트워크 내에서만 유일하면 됩니다.

  통신방법 : Unicast(1:1), Multicast(1:Group), Anycast(1:Nearest 1 = 주소 중복 가능) <주의> broadcast 없음
  
### IPv6 Routing Protocol

  - 실습

  ![image](https://user-images.githubusercontent.com/84834776/221114214-8e65d261-04f4-4af3-87d3-d11f873e1919.png)

  - 풀이

  ![image](https://user-images.githubusercontent.com/84834776/221114278-9d1a0ad4-f98b-417e-a4ed-b66ac115ccf8.png)

### IPv6 BGP

  - 실습

  ![image](https://user-images.githubusercontent.com/84834776/221456634-7a65717e-4c15-4d36-8826-4beacac93c4e.png)

  - 풀이

  ![image](https://user-images.githubusercontent.com/84834776/221456945-eccbeaa7-45ea-4464-941b-e1e0a4e7cb34.png)
  
  ![image](https://user-images.githubusercontent.com/84834776/221456976-6957a3d9-f8c7-4a65-9915-83e521eaf9c6.png)

  ![image](https://user-images.githubusercontent.com/84834776/221457011-4ee7de62-e41c-436d-be56-3bbe398eb01a.png)



### Router 패스워드 설정, 라우팅 정보 확인 및 저장, console 패스워드 구성, enable 패스워드 구성, TFTP nvram에 저장, 
  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/217982780-733b9f9d-ebb2-4348-b636-b3914a3c36a3.png)

  - 풀이

    ![image](https://user-images.githubusercontent.com/84834776/217985054-47a7d538-27cb-4900-afc8-e7b55a6c11bb.png)

  - 결과 확인

    1. ping 연결 확인
    2. 다운받은 라우터 구성요소 워드패드로 확인
    3. TFTP 서버에서 내용 변경 후 라우터 RAM에 다시 저장하기
    4. 변경한 내용이 라우터에 반영이 되었다면 ok


### Router 패스워드 복구
  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/217999652-923ab228-252a-4fdb-a865-26a44fb6a280.png)

  - 풀이

    ![image](https://user-images.githubusercontent.com/84834776/217999686-b295e238-9301-4300-b3eb-14b43562059f.png)

  - 결과 확인

    1. Router의 전원을 껐다 다시 켰을 때, enable 시 수정한 패스워드로 진입 가능하면 ok

### Router IOS 복구 절차
  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/218006034-0cd31480-0949-4da8-aefb-769e25d5f79d.png)

  - 풀이 

    ![image](https://user-images.githubusercontent.com/84834776/218006080-c6eeedfb-f2c9-4a0e-b152-3a06f365253f.png)

  - 결과 확인

    1. 라우터 장비의 전원을 껐다 켰을 때, os 로드되면 ok

### Router 패스워드 복구, Router IOS 복구 절차
  - 실습

    ![image](https://user-images.githubusercontent.com/84834776/218016255-282842ed-676c-4517-b39c-e4af1feb4697.png)

  - 풀이

    ![image](https://user-images.githubusercontent.com/84834776/218016338-2506551d-633c-415a-92fd-fe2fdafbf602.png)

  - 결과 확인

    1. R1에서 TFTP 서버까지 ping 확인

### Cable
  - 황띠  황  초띠  파  파띠, 초, 갈띠, 갈
  - Route=PC, HUB=SWITCH
  - Straight-Through Cable (Direct) : 타입이 다른 경우(실선)
  - Crossover Cable (Cross) : 타입이 같은 경우(점선)
  - Rollover Cable (console) : Router/Switch 셋팅

  
