---
layout: single
title: "디지털 스마트 부산 아카데미 예비 프로젝트"
categories: "예비프로젝트"
tag: [python, 예비 프로젝트, 소프트웨어 교육 프로그램, YOLO, FaceNet, 팀 프로젝트]
---

# YOLO와 FaceNet 모델을 이용한 초상권 보호 모자이크 처리 시스템

## Portrait rights protection mosaic processing system using YOLO and FaceNet model

### 1. 프로젝트 주제

> 필요성

<img width="473" alt="image" src="https://user-images.githubusercontent.com/84834776/204127877-174dc0c4-2c63-41ce-a245-becaa6f17f8a.png">

- 1인 크리에이터, 케이블/공중파 방송국, SNS 인플루언서 등 공개적 사진 또는 영상 게시물 인기
- 보행자 입장 : 원치 않은 노출이 갈수록 늘어나고 있는 추세
- 크리에이터 입장 : 초상권으로 인한 영상 삭제 요청 시 금전적 피해

> 목표

- 특정 인물을 제외한 나머지 사람들에 있어 자동 모자이크 처리 시스템 개발

### 2. 참여기간 / 참여인원

- 2022-09-23 ~ 2022-10-14 / 전자공학 1명, 경영정보학 3명, 운동정보학 1명

### 3. 사용한 기술 스택

> 언어 및 프레임워크

- Python
- YOLOv5, YOLOv7
- FaceNet
- labelImg; Labeling Program

> 개발환경

- Google Colab
- Jupyter Notebook

### 4. 나의 역할

- 데이터 수집 및 라벨링
- 객체 모자이크 처리 코드 작성
- YOLO 모델과 FaceNet 모자이크 코드 결합
- 학습 모델 테스트 

### 5. 핵심기능

<img width="501" alt="image" src="https://user-images.githubusercontent.com/84834776/204193379-c88ae3a1-315b-43eb-9644-24308ae69b86.png">

- YOLO 모델로 구현한 특정 인물을 제외한 나머지 인물 모자이크 처리 플로우차트

<img width="493" alt="image" src="https://user-images.githubusercontent.com/84834776/204193449-9fec1d41-66eb-44bc-9e16-6c03cfca119a.png">

- FaceNet 모델로 구현한 특정 인물을 제외한 나머지 인물 모자이크 처리 플로우차트

#### ※ 기능 구현

> 데이터 수집 및 라벨링

 <img width="494" alt="image" src="https://user-images.githubusercontent.com/84834776/204195410-b62ad5f8-a180-4dcf-94de-1b7566c64c3c.png">

- YOLO 모델 특정 인물 데이터 수집 및 클래스 분류 : 김용명 이미지 크롤링 및 영상 프레임 추출 / 라벨링
- 약 1 만개의 이미지 데이터

<img width="473" alt="image" src="https://user-images.githubusercontent.com/84834776/204195637-6f3f0b13-b6b8-4091-b582-223beef4bbd0.png">

- FaceNet 모델 특정 인물 데이터 수집 및 클래스 분류 : 김용명 이미지 크롤링 및 영상 프레임 추출 / 라벨링
- 194개의 이미지 데이터

> 결과

<img width="432" alt="image" src="https://user-images.githubusercontent.com/84834776/204195961-198ce23f-1c85-4adb-b611-d5ed17dfde26.png">

- YOLOv5s 모델 - 약 mAP 77% (에포크 200번)
- YOLOv5m 모델 - 약 mAP 32% (에포크 17번)
- YOLOv7 모델 - 약 mAP 65% (에포크 30번)

※ 결과적으로 YOLO 모델과 FaceNet 모델의 정확도 성능 비교를 하기엔 동일한 학습 환경이 되지 못해서, 사용자의 결과 분석 경험을 통해 YOLOv7 모델이 가장 좋을 것이라고 판단하였음.

### 6. 트러블슈팅

> Problem 1

YOLO 모델에서 연예인 또는 여성의 경우 크게 화장법이 달라지는 경우 인식률이 떨어짐.

> Solution 1

YOLO 모델에서 근본적인 해결방법을 찾지 못했지만, FaceNet을 통해 한계점 보완

> Problem 2

FaceNet 모델에서 특정 인물을 2명 이상 학습해주어야 해서 한 명일 때 모자이크 처리 기능 구현의 어려움.

> Solution 2

학습된 사람 얼굴을 분류하는 코드에서 특정 인물 라벨이 아닐 때, 모자이크 처리 실행 코드 추가.

한 명의 사람만 인식하고 싶을 때도 모자이크 처리 가능.

> Problem 3

YOLO 모델의 경우 코랩 GPU 할당 문제로 동일한 학습을 적용시키기 어려움.

> Solution 3

제한적인 상황에서 팀원들끼리 최대한 GPU 자원을 모아 다양한 모델을 돌려볼 수 있게 함.

### 7. 프로젝트(Google Drive) 코드 링크

[Code Link](https://drive.google.com/drive/folders/10BtvndKGUIEfBFq66WxDkwASNDcVvRGN?usp=share_link)
