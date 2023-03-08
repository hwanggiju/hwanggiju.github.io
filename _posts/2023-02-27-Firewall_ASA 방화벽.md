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






