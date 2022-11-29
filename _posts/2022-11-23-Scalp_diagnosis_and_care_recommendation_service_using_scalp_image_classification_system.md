---
layout: single
title:  "디지털 스마트 부산 아카데미 최종 프로젝트"
categories: "FinalProject"
tag: [python, 소프트웨어 교육 프로그램, 최종 프로젝트, YOLO, EfficientNet B0, 팀 프로젝트, 수상작]
---

# 두피 이미지 분류 시스템을 활용한 두피 진단 및 케어 추천 서비스 (수상작)

## Scalp diagnosis and care recommendation service using scalp image classification system


### 1. 프로젝트 주제

> 필요성

- 설문 조사 결과

    <img width="451" alt="image" src="https://user-images.githubusercontent.com/84834776/204461669-e2ca3d01-9ce0-4353-a9f3-8c4d1e2c593c.png">

    <한국암웨이 기업과 모바일 리서치 기관인 오픈서베이 성인 400명을 대상으로 한 성인 두피 관리 실태 조사 결과>

1. 첫번째 그래프, 젊은 층에서도 두피 고민이 많은 것을 볼 수 있음.

2. 두번째 그래프, 고민은 많은 반면 두피 관리는 소극적

    <img width="200" alt="image" src="https://user-images.githubusercontent.com/84834776/204461735-f8df1c5d-6da1-41f4-8ba5-9bf429c1bc69.png">

    <건강보험공단에서 발표한 탈모증 환자 증가 추세 그래프> 

1. 젊은 층 외모에 대한 관심 증가 -> 병원을 찾는 빈도 수 증가

2. 사회적 스트레스로 인한 우리나라의 탈모 인구 증가

    > 관리를 하지 않응 이유  why?

    1. 증상이 바로 눈에 보이지 않아 관리의 심각성 x

    2. 관리 정보 부족과 비용 부담

- 키워드 분석 플랫폼 (썸트렌드)

    <img width="471" alt="image" src="https://user-images.githubusercontent.com/84834776/204461792-596aaff2-17d8-4eef-9b58-f5e5dff34b33.png">

    <썸트렌드 두피 키워드 검색 결과>

1. 전체순위에서 샴푸, 관리, 상태와 같은 단어에서 두피 관리를 연상케 하는 것을 볼 수 있음.

2. 검색 건수가 가장 많은 탈모의 경우, 탈모를 예방하기 위한 프로젝트를 한다면, 사람들의 수요가 어느정도 있을 것이라 판단.

- 토픽 모델링 LDA / 워드클라우드 진행

1. 첫번째 결과, '두피 증상'이라는 주제 추측

    <img width="463" alt="image" src="https://user-images.githubusercontent.com/84834776/204461833-3771c916-9328-4568-acd6-58fa3aa11aaf.png">

2. 두번째 결과, '두피 케어'라는 주제 추측

    <img width="463" alt="image" src="https://user-images.githubusercontent.com/84834776/204461870-189af50f-3013-43c8-870b-f98e90aa848e.png">

3. 주제 1과 주제 2에 대한 워드클라우드

    <img width="464" alt="image" src="https://user-images.githubusercontent.com/84834776/204461906-9390c915-5b41-4289-9789-44e36e8f15fe.png">

> 목표

1. 집에서 스마트 폰으로 자신의 두피를 촬영하고 두피 유형을 진단한 후 맞춤형 두피 제품을 추천 받을 수 있음.

2. 실시간으로 촬영하여 자신의 두피 증상 확인.

### 2. 참여기간 / 참여인원

- 2022-10-17 ~ 2022-11-23 / 전자공학 1명, 경영정보학 3명, 체육학과 1명

### 3. 사용한 기술 스택

> 언어 및 프레임워크

- Python - Flask
- YOLOv5, YOLOv7
- EfficientNet
- AIhub
- labelImg; Labeling Program

> 개발환경

- Google Colab
- Jupyter Notebook
- GPU

### 4. 나의 역할

- 프로젝트 발표
- LDA
- 메타데이터 EDA
- 웹 어플리케이션 구현
- EfficientNet, YOLO 모델 적용

### 5. 핵심기능

- EfficientNet B0 모델을 활용한 두피 이미지 유형 분류

- YOLOv5m 모델을 활용한 실시간 두피 증상 탐지

#### ※ 기능 구현

- AIhub 유형별 두피 이미지 활용

    1. 6가지 증상에 대한 이미지 데이터와 라벨링 데이터
    2. 증상에 대한 8가지 유형 분류 기준 표
    3. 약 10만명의 사람들 두피 정보 메타데이터

- 모델별 클래스 선정 기준

    > YOLO
    - 비듬과 홍반 클래스 분류
    - 증상이 비슷한 것들끼리 하나로 통합
    - 미세각질과 피지과다 : 비듬의 주 요인 (비듬)
    - 모낭사이홍반과 모낭홍반농포 : 비슷한 홍반 증상 (홍반)
    - 탈모 : 탈모를 예방하기 위한 프로젝트로써 적합하지 않다고 판단.

    > EfficientNet B0
    - 탈모 : 탈모를 예방하기 위한 프로젝트로써 적합하지 않다고 판단.
    - 탈모를 제외한 5가지 증상 클래스 선정
    - 탈모성을 제외한 7가지 유형 이용 
    
    <img width="453" alt="image" src="https://user-images.githubusercontent.com/84834776/204467901-1c614b61-73b8-441f-82d1-5922530b9e27.png">
    
    - 두피 이미지 삽입 -> 각 증상마다의 중증도 단계 분류 -> 기준 표를 기반으로 최종 두피 유형 분류

    <img width="442" alt="image" src="https://user-images.githubusercontent.com/84834776/204467977-5f014518-d261-4e96-b4e3-f655c607e332.png">

- 메타데이터 EDA

    <img width="422" alt="image" src="https://user-images.githubusercontent.com/84834776/204468023-a11b2be0-24a2-40e2-ae32-44ae613c6a92.png">
    
    <img width="422" alt="image" src="https://user-images.githubusercontent.com/84834776/204468069-58833778-3981-4ecc-8678-1cb208bd7d5f.png">

    각종 EDA 과정을 거쳐 사람들의 두피 정보 인사이트 정보 획득

- 모델 구축

> YOLO 모델 정확도 비교 및 결과

<img width="330" alt="image" src="https://user-images.githubusercontent.com/84834776/204468106-f0b8cd0a-d877-42cf-997f-6e0118a802bb.png">

> EfficientNet B0 정확도 결과

<img width="426" alt="image" src="https://user-images.githubusercontent.com/84834776/204468141-f6a5334b-d708-401f-8c19-26f21182ea8d.png">

- 웹과 어플 구현

    ***프로젝트 코드 링크 참조***

### 6. 트러블슈팅

> Problem 1



> Solution 1



> Problem 2



> Solution 2



### 7. 프로젝트 후기

약 5주간의 교육 최종 프로젝트 기간이었다. 처음에는 4개월 동안 같이 교육 듣는 사람들과 어느정도 친해져서 서로 소통이 원활했다.

아이디어 기획부터해서 프로젝트 최종 발표 때까지 이전에 배웠던 것들을 활용해 완벽한 결과물을 만들고자 목표를 세웠고, 좋은 결과물을 만들어 낼 수 있었던 것 같다. 

결과적으로 최종 프로젝트 발표에서 금상을 받을 수 있었다.

<img width="275" alt="image" src="https://user-images.githubusercontent.com/84834776/204469037-8655412c-a88d-4fa4-8df9-a2523f78ca19.png">

### 8. 프로젝트(Google Drive) 코드 링크

[Code Link](https://drive.google.com/drive/folders/16w_G1dtGKbUNC5J1ic9c66D3OmZU2dHR?usp=share_link)










