---
layout: single
title: "디지털 스마트 부산 아카데미 미니 프로젝트"
categories: "미니프로젝트"
tag: [python, 미니 프로젝트, 소프트웨어 교육 프로그램, 데이터 수집 및 분석, YOLO, 팀 프로젝트]
---

# YOLOv5를 활용한 야생동물 로드킬 방지 모델

## Wildlife roadkill prevention model using YOLOv5

### 1. 프로젝트 주제

- YOLOv5를 활용하여 야생동물 로드킬 방지 모델 생성

> 필요성
  
  <img width="481" alt="image" src="https://user-images.githubusercontent.com/84834776/194847259-e976fe17-c626-479f-91d8-2802f85552e7.png">
 
  - 해마다 증가하는 야생동물 로드킬 문제
  - 동물 뿐만 아니라 운전자에게도 큰 위협
  - 고라니, 너구리, 맷돼지, 맷토끼, 고양이, 오소리 - 가장 사고가 많이 일어나는 동물 6가지 선정
  - 야생동물 탐지 시 해결방안 제시 (초음파 스피커)

### 2. 참여기간 / 참여인원

  - 2022-09-19 ~ 2022-09-22 / 전자공학 1명, 경영정보학 2명

### 3. 사용한 기술 스택
  
#### 언어 및 프레임워크
  
  - Python
  - YOLOv5
  - labelImg ; Labeling Program

#### 개발환경

  - Google Colab
  - Jupyter Notebook
  - Window
  
### 4. 나의 역할

  - 데이터 수집 및 라벨링
  - YOLOv5 모델 적용
  - Team Code Error 해결
  - 학습 모델 테스트

### 5. 핵심기능

  <img width="229" alt="image" src="https://user-images.githubusercontent.com/84834776/194854152-16f36ef5-ef7b-4985-974a-47ca765efabb.png">

  1. YOLOv5를 활용한 야생동물 탐지 후 주파수 스피커를 설치하여, 동물이 들을 수 있는 가청주파수 대역으로 설정.
  2. 로드킬이 많이 발생하는 동물 고라니, 맷돼지, 너구리, 오소리, 토끼, 고양이 객체 크롤링 + 영상 프레임 추출
  3. 학습결과 mAP 0.95 : 약 94%

#### ※ 기능 구현

- 데이터 수집 (크롤링 + 영상 이미지 프레임 추출)
- 각 동물에 대한 구글 이미지 크롤링과 산 속 야간 촬영 동물 영상 이미지 프레임 추출하여 데이터 수집
  
  > 수집과정
  
   - 영상 프레임 추출
    
     <img width="624" alt="image" src="https://user-images.githubusercontent.com/84834776/194855274-4135c749-055b-4942-b385-b0174c9277aa.png">
    
   - 크롤링
    
     <img width="624" alt="image" src="https://user-images.githubusercontent.com/84834776/194855415-35e52bda-55e0-4be9-858c-222b3491d16e.png">

- 데이터 라벨링
- labelImg program 사용

  > 라벨링 과정

  - 클래스 구성

  <img width="138" alt="image" src="https://user-images.githubusercontent.com/84834776/194856257-3ececc16-e478-4428-927d-5eb8a5675430.png">

  - 라벨링 진행

  <img width="428" alt="image" src="https://user-images.githubusercontent.com/84834776/194856312-4de4ba6c-625e-48a5-bb75-c7d6a00a13c8.png">

- YOLOv5 모델 학습

  > 선정이유
  
  <img width="627" alt="image" src="https://user-images.githubusercontent.com/84834776/194856727-f26b2def-99b8-4e21-ab83-62c2c5b266ed.png">
  
  - 이미지 전체를 보는 특성 -> 맥락적 이해도가 다른 모델에 비해 우수
  - 실시간 이미지 객체 인식에 있어 준수한 성능
  - 간단하고 빠른 처리 속도
  
  > 학습과정

  <img width="468" alt="image" src="https://user-images.githubusercontent.com/84834776/194857042-371e5916-8dfc-4fa1-87ee-b4c6af7b291d.png">
  
  - mAP 0.95 : 약 94%
  
- 테스트 결과 시각화

  <img width="581" alt="image" src="https://user-images.githubusercontent.com/84834776/194857515-336bc532-b2c9-4e3e-bb07-a40693cccf0c.png">

  <img width="595" alt="image" src="https://user-images.githubusercontent.com/84834776/194857574-bc2e8cba-57c1-4c2f-a79f-7b25405fc75a.png">

### 6. 트러블슈팅

  - 데이터 라벨링 인덱스 번호 불일치

  > Problem
  
  데이터 라벨링 중 동물 라벨링 인덱스 번호가 다르게 지정되어 학습 결과에 오류
  
  > Solution

  데이터를 한 사람 당 800개 이상 수집, 직접 찾아서 하기보다 코드로 반복하여 파일을 열어 인덱스 번호 변경하여 문제 해결

  - 코드 오류 문제

  > Problem

  팀원들의 코드 오류에 대한 어려움
  
  태풍으로 인해 비대면 소통
  
  > Solution

  짧은 프로젝트 기간이다보니 편한 분위기 조성이 다소 어려웠기 때문에, 코드 오류 발생 시 혼자 고민하는 경향
  
  더욱이 태풍으로 인해 비대면 환경에서 어색함을 느끼게 되었지만, 최대한 풀어나가기 위해 잠깐의 가벼운 이야기로 편한 분위기 조성
  
  이후 혼자 고민하기 보단 함께 고민하면서 문제 해결 

### 7. 깃허브 링크

  [Code Link](https://github.com/hwanggiju/Detect_WildAnimals.git)

