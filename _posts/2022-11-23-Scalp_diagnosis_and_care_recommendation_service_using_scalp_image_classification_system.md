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

    관리를 하지 않응 이유  why?

    1. 증상이 바로 눈에 보이지 않아 관리의 심각성 x

    2. 관리 정보 부족과 비용 부담

- 키워드 분석 플랫폼 (썸트렌드)

    <img width="471" alt="image" src="https://user-images.githubusercontent.com/84834776/204461792-596aaff2-17d8-4eef-9b58-f5e5dff34b33.png">

    <썸트렌드 두피 키워드 검색 결과>

    1. 전체순위에서 샴푸, 관리, 상태와 같은 단어에서 두피 관리를 연상케 하는 것을 볼 수 있음.

    2. 검색 건수가 가장 많은 탈모의 경우, 탈모를 예방하기 위한 프로젝트를 한다면, 사람들의 수요가 어느정도 있을 것이라 판단.

- 토픽 모델링 LDA / 워드클라우드 진행
    
    <img width="463" alt="image" src="https://user-images.githubusercontent.com/84834776/204461833-3771c916-9328-4568-acd6-58fa3aa11aaf.png">

    1. 첫번째 결과, '두피 증상'이라는 주제 추측

    <img width="463" alt="image" src="https://user-images.githubusercontent.com/84834776/204461870-189af50f-3013-43c8-870b-f98e90aa848e.png">

    2. 두번째 결과, '두피 케어'라는 주제 추측

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


#### ※ 기능 구현


### 6. 트러블슈팅


### 7. 프로젝트 후기


### 8. 프로젝트(Google Drive) 코드 링크

[Code Link](https://drive.google.com/drive/folders/16w_G1dtGKbUNC5J1ic9c66D3OmZU2dHR?usp=share_link)










