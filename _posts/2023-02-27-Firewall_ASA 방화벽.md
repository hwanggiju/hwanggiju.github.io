---
layout: single
title:  "Private 클라우드를 활용한 네트워크&서버 보안 운영 관리 - 방화벽"
categories: "Education"
tag: [네트워크, 국비교육과정(Private 클라우드를 활용한 네트워크&서버 보안 운영 관리), ASA]
---

# 방화벽
## 일정
  - 2023.03.06 ~ 2023.

### ASA.Firewall. Security-Level 구성

  ![image](https://user-images.githubusercontent.com/84834776/223028736-8fbd923b-7210-4815-a5db-4d285c751280.png)

### ASA.Firewall. ACL & MPF 구성

  ![image](https://user-images.githubusercontent.com/84834776/223034668-299931ad-845f-44c6-bb14-c892f229b64e.png)

### ASA.Firewall. 기본정책 global_policy 구성

  ![image](https://user-images.githubusercontent.com/84834776/223042119-67eac8df-7519-4e7d-866b-f25a1eaaa120.png)

### ASA.Firewall. ACL과 MPF 혼합 구성 1

  ![image](https://user-images.githubusercontent.com/84834776/223043281-b6315a7e-4a88-4fab-8c9b-9b9443cd062c.png)

### ASA.Firewall. ACL과 MPF 혼합 구성 2

  ![image](https://user-images.githubusercontent.com/84834776/223043804-23b09bf2-6476-4f78-8a3c-649d93a393fd.png)

### ASA.Firewall.라우팅 : STATIC ROUTE

  ![image](https://user-images.githubusercontent.com/84834776/223588230-2ee7f0d5-83fc-48ab-8262-0e69dc397b02.png)

### ASA.Firewall.라우팅 : RIPv2

  ![image](https://user-images.githubusercontent.com/84834776/223594279-e74b730b-2adf-4a26-a81c-984fdeec4410.png)

### ASA.Firewall.라우팅 : EIGRP

  ![image](https://user-images.githubusercontent.com/84834776/223596016-9a0fb080-a25d-4385-ad10-1523f92b9e0b.png)

### ASA.Firewall.라우팅 : OSPF

  ![image](https://user-images.githubusercontent.com/84834776/223597137-1ae19f9a-e7a3-4eea-b300-973538a6321b.png)

### ASA ACL

  - 연습 1 : outside 에서 dmz 에 위치한 다음 서비스들에 대해 접근을 허용하시오

    - 조건

    ![image](https://user-images.githubusercontent.com/84834776/223620883-344ed63e-d191-4e52-a5ae-f303c85233aa.png)
  
  - 풀이

    ![image](https://user-images.githubusercontent.com/84834776/223620769-e5936d1c-ed41-4f7d-9565-24850ed65cbd.png)

  - 연습 2 : outside 에서 dmz 으로 전송되는 ICMP 가 차단되는 Log 메시지 확인하기
    
    ![image](https://user-images.githubusercontent.com/84834776/223625964-4344899d-4391-4c00-b75f-979b40db611c.png)
    
  - 결과

    ![image](https://user-images.githubusercontent.com/84834776/223625776-8e34d04f-3f71-400a-8146-4fb1e37cb264.png)

  - 연습 3 : outside 에서 dmz 으로 전송되는 ICMP 가 차단되는 Log 메시지 통계치 출력하기

    ![image](https://user-images.githubusercontent.com/84834776/223626531-6e100a19-8d9a-4d74-a6ae-13c680db1538.png)

  - 결과 

    ![image](https://user-images.githubusercontent.com/84834776/223626741-1ae74809-d626-48eb-8f10-4ec7f7861c3a.png)

  - 연습 4 : Object를 사용한 Access list 구성

    - 조건 

    ![image](https://user-images.githubusercontent.com/84834776/223632534-9b04c838-eb3a-4c09-8ee9-c8493f51a658.png)
    
    - 풀이


    ![image](https://user-images.githubusercontent.com/84834776/223632456-56df94f1-496c-453c-b682-455bb22180ac.png)

  - 연습 5 : Object group을 사용한 Access list 구성

    - 조건 

    ![image](https://user-images.githubusercontent.com/84834776/223632840-25a5d2e3-f43a-46da-8d75-94d70a7490b6.png)

    - 풀이

    ![image](https://user-images.githubusercontent.com/84834776/223634633-fa86eda1-a309-40d2-b045-b01ff22c41fb.png)

  - 연습 6 : Object 와 Object Group 을 사용한 Access list 구성 - 시간 설정

    ![image](https://user-images.githubusercontent.com/84834776/223638235-b2498ffe-a73a-41ef-b91b-b6bad0de0b8d.png)
    
### MTF

  - Application Layer Control(DPI) STEP 1 : Telnet서버

  ![image](https://user-images.githubusercontent.com/84834776/223889448-015bd162-0278-4f3d-b4be-0a0bcb360ea3.png)

  - Application Layer Control(DPI) STEP 2 : HTTP
  
  ![image](https://user-images.githubusercontent.com/84834776/223897610-da75cfd2-147c-405a-bc31-5216f13ce4ad.png)

  - Application Layer Control(DPI) STEP 3 : FTP
  
  ![image](https://user-images.githubusercontent.com/84834776/223901963-41afd773-e008-44ad-8d53-f27abe5460fd.png)

### ASA.Firewall.NAT

  - Section 2 : Object NAT (Auto NAT)

  ![image](https://user-images.githubusercontent.com/84834776/223927653-dbf66887-8e73-49f8-bfe7-7c47be9949c3.png)

  ![image](https://user-images.githubusercontent.com/84834776/223929529-a46bbe0f-c5d3-4ed2-9372-b057de51fb3b.png)
    
  ![image](https://user-images.githubusercontent.com/84834776/223931481-65ccbd83-d524-4ba1-ae11-e00e1037132b.png)
  
  ![image](https://user-images.githubusercontent.com/84834776/223937055-ae2e5e11-b544-4abd-95d9-71d300ea053c.png)
  
  - Section 3 : After-auto manual NAT(Manual NAT)

  ![image](https://user-images.githubusercontent.com/84834776/223942377-de35aa12-2493-4f01-98fb-e9d43e5aaf3a.png)

  - Section 1 : Manual NAT(Twice NAT)
  
  ![image](https://user-images.githubusercontent.com/84834776/223948493-9b557721-6749-4f3f-888b-13a11924703f.png)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
