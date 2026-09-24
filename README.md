# Starbucks Customer Segmentation & Promotion Analysis

스타벅스 고객 행동 및 프로모션 로그를 분석하여  
**고객 세그먼트별 프로모션 성과를 비교하고 맞춤형 프로모션 전략을 제안한 팀 프로젝트**입니다.

---

## Project Context

스파르타 내일배움캠프 데이터분석 10기 과정에서 진행한  
**팀 기반 교육 프로젝트**입니다.

모든 고객에게 동일한 프로모션을 제공하는 방식보다  
고객의 구매 빈도, 최근 구매 시점, 구매 규모와 프로모션 반응을 함께 고려해  
**고객군별로 다른 프로모션 전략을 설계하는 것**을 목표로 했습니다.

---

## Business Question

> 고객 특성과 구매 행동에 따라  
> **어떤 프로모션을 누구에게 제공해야 더 효과적인 성과를 낼 수 있을까?**

이를 위해 다음 흐름으로 분석했습니다.

1. 프로모션 유형과 조건별 성과 분석
2. 고객 구매 행동 기반 RFM 세그먼트 설계
3. 세그먼트별 매출 기여도 및 프로모션 효율 비교
4. Tableau 대시보드 구성
5. 고객군별 맞춤 프로모션 전략 제안

---

## My Contribution

저는 프로젝트에서 **데이터 전처리 및 프로모션 거래 매칭 로직 구현, Tableau 시각화 작업**에 참여했습니다.

### 1. Data Preprocessing

개인 전처리 노트북에서 다음 작업을 수행했습니다.

- `portfolio`, `profile`, `transcript` 데이터 구조 확인 및 컬럼명 정리
- 고객 데이터의 결측치 및 중복 데이터 처리
- `value` 컬럼의 딕셔너리 구조를 파싱하여 `amount`, `offer_id`, `reward` 변수 생성
- 프로모션 채널을 web / email / mobile / social 이진 변수로 변환
- 거래 금액 로그 변환 후 IQR과 Z-score를 함께 활용한 이상치 처리
- 거래(transaction)에 프로모션 `offer_id`를 연결하는 매칭 로직 구현
- 프로모션 완료 시점과 유효기간을 고려하여 구매를  
  **direct / indirect / organic** 유형으로 구분
- 고객 정보와 프로모션·거래 데이터를 결합하여 분석용 데이터셋 생성

> 개인 작업 과정은 `notebooks/jaehee_preprocessing.ipynb`에서 확인할 수 있습니다.

### 2. Tableau Visualization

프로모션 성과와 RFM 고객 세그먼트를 비교할 수 있도록  
Tableau 기반 시각화 작업에 참여했습니다.

프로젝트에서는 다음 세 가지 관점의 대시보드를 구성했습니다.

- 프로모션 현황
- RFM 매출 분석
- RFM 상세 현황 및 퍼널

---

## Data

프로젝트에서는 세 가지 데이터셋을 활용했습니다.

### `portfolio.csv`
프로모션 정보

- Reward
- Channel
- Difficulty
- Duration
- Offer Type

### `profile.csv`
고객 인구통계 정보

- Gender
- Age
- Income
- Membership Date

### `transcript.csv`
고객의 프로모션 및 구매 이벤트 로그

- Person
- Event
- Value
- Time

원본 데이터 규모:

- Portfolio: **10 rows**
- Profile: **17,000 rows**
- Transcript: **306,534 rows**

전처리 과정에서 결측치, 중복값, 이상치 등을 정리하여  
이벤트 로그는 최종 **293,041건**을 분석에 활용했습니다.

---

## Analysis Workflow

1. 데이터 구조 및 품질 확인
2. 결측치·중복값·이상치 처리
3. 프로모션 및 거래 이벤트 구조화
4. Transaction–Offer 매칭
5. 프로모션 영향 매출 분류
6. 프로모션 유형 및 조건별 성과 분석
7. RFM 고객 세그먼트 생성
8. 고객군별 매출 기여도 및 ROI 비교
9. Tableau 대시보드 제작
10. 고객군별 맞춤 프로모션 전략 제안

---

## Key Analysis

### 1. Promotion Performance

프로모션이 실제 구매에 어느 정도 영향을 주는지 확인하기 위해  
매출을 직접기여, 간접기여, 비프로모션 매출로 구분했습니다.

주요 결과:

- **간접기여 매출: 48.3%**
- **직접기여 매출: 36.5%**
- **비프로모션 매출: 15.1%**
- 전체 매출의 약 **85%가 프로모션의 영향을 받은 매출**로 나타남
- Discount 프로모션이 BOGO보다 높은 매출 비중을 기록

---

### 2. Promotion Difficulty & Duration

프로모션의 최소 구매 조건과 유효기간에 따라  
고객 반응이 어떻게 달라지는지 비교했습니다.

주요 결과:

- **$10 지출 미션**이 전체 매출에서 가장 큰 비중을 차지
- **7일 유효기간** 프로모션이 높은 매출 성과를 기록
- 고객은 리워드 규모보다 **미션 달성 난이도**에 더 민감하게 반응
- 많은 고객군에서 **$7를 초과하는 조건부터 완료율이 감소**

---

### 3. RFM Customer Segmentation

고객 행동을 다음 세 가지 기준으로 점수화했습니다.

- **Recency**: 마지막 구매 후 경과일
- **Frequency**: 기간 내 구매 횟수
- **Monetary**: 평균 구매 금액

RFM 점수에 따라 고객을 다섯 그룹으로 분류했습니다.

- VVIP
- VIP
- 충성고객
- 잠재고객
- 우려고객

VIP와 충성고객이 전체 고객의 핵심 비중을 차지하며,  
두 그룹이 전체 매출의 약 **78%**를 만들어냈습니다.

---

### 4. Segment Performance

고객군별 프로모션 성과에는 큰 차이가 나타났습니다.

- VVIP의 프로모션 ROI: **1,103%**
- 우려고객의 ROI는 VVIP 대비 크게 낮게 나타남
- VIP와 충성고객은 프로젝트의 핵심 매출 기여 그룹
- 잠재·우려고객은 프로모션 도달률과 완료율 개선 필요

따라서 모든 고객에게 동일한 프로모션을 제공하기보다  
**고객 세그먼트별로 다른 난이도와 혜택을 적용할 필요**가 있음을 확인했습니다.

---

## Dashboard

프로젝트에서는 Tableau를 활용해 세 가지 대시보드를 구성했습니다.

### Dashboard 1 — Promotion Overview

프로모션 유형, 최소 구매 조건, 유효기간 등에 따른  
성과 및 완료율을 비교합니다.

### Dashboard 2 — RFM Revenue Analysis

RFM 고객군별 매출 기여도와  
효율이 높은 프로모션을 비교합니다.

### Dashboard 3 — RFM Detail & Funnel

프로모션 수신부터 완료까지의 퍼널을 통해  
고객군별 전환율과 이탈률을 확인합니다.

> 대시보드 이미지는 `images/` 폴더에 추가할 예정입니다.

---

## Strategy Recommendations

분석 결과를 기반으로 고객군별 차별화된 프로모션을 제안했습니다.

### VVIP / VIP

높은 구매 빈도와 구매 규모를 유지하는 고객군으로  
차별화된 경험과 충성도 유지에 초점을 맞췄습니다.

예시:

- 신메뉴 및 커스텀 메뉴 추천
- VIP 전용 굿즈
- 리저브 원두 체험 등 프리미엄 혜택

### Loyal Customers

전체 고객에서 큰 비중을 차지하는 핵심 그룹으로  
VIP 등급으로의 상향과 방문 습관 형성을 목표로 했습니다.

예시:

- 자주 구매하는 메뉴 기반 간편 주문
- 등급 상향 리워드

### Potential / At-Risk Customers

구매 빈도와 프로모션 효율이 상대적으로 낮은 고객군에는  
진입 장벽을 낮춘 혜택을 제안했습니다.

예시:

- 소액 할인 쿠폰
- BOGO 프로모션
- 재방문 유도 프로모션

---

## Repository Files

### `notebooks/data_preprocessing.ipynb`

팀 프로젝트에서 사용한 최종 데이터 전처리 및 분석용 데이터 생성 과정입니다.

### `notebooks/jaehee_preprocessing.ipynb`

제가 수행한 전처리 작업을 정리한 개인 노트북입니다.

주요 내용:

- 이상치 처리
- 프로모션 이벤트 구조화
- Transaction–Offer 매칭
- 구매 유형 분류
- 분석용 데이터셋 병합

### `tableau/starbucks_promotion.twb`

프로모션 및 RFM 분석을 위한 Tableau workbook 파일입니다.

### `images/`

README에 사용할 Tableau 대시보드 이미지를 저장하는 폴더입니다.

---

## Tools

### Data Analysis
- Python
- Pandas
- NumPy

### Preprocessing & Analysis
- Scikit-learn
- IQR
- Z-score
- RFM Analysis

### Visualization
- Matplotlib
- Seaborn
- Tableau

---

## Repository Structure

```text
starbucks-customer-promotion-analysis/
│
├── README.md
│
├── notebooks/
│   ├── data_preprocessing.ipynb
│   └── jaehee_preprocessing.ipynb
│
├── tableau/
│   └── starbucks_promotion.twb
│
└── images/
    └── .gitkeep
```

---

## Project Type

- **Educational Team Project**
- Sparta Data Analysis Bootcamp
- Data Analysis 10th Cohort

> This repository contains the analysis files used in the team project.  
> My primary work in the repository includes data preprocessing, transaction–offer matching,  
> promotion purchase classification, and Tableau visualization.
