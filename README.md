# 🎓 대학생 맞춤형 장학금 추천 서비스 (UNI-DTHON 금상 수상작)
> **Personalized Scholarship Recommendation App for University Students**

![Mobile Application](https://img.shields.io/badge/Moblile_Application-Flutter-150458) ![Backend Server](https://img.shields.io/badge/Backend_Server-Node.js-blue)
![Data Analysis & Processing](https://img.shields.io/badge/Data_Analysis_&_Processing-Python-yellow)

## 📌 1. Project Overview (프로젝트 개요)
수많은 장학금 정보가 산재해 있어 몰라서 못 받는 장학금이 많다는 문제에서 출발했습니다.
본 프로젝트는 **전국 장학금 데이터를 수집 및 DB화**하고, 사용자의 개인 정보(학점, 소득분위, 거주지 등)를 기반으로 **신청 가능한 장학금을 자동으로 필터링하여 추천**해주는 모바일 애플리케이션 프로토타입입니다.

* **기간:** 20XX.XX ~ 20XX.XX (UNI-DTHON 해커톤 프로젝트)
* **성과:** **UNI-DTHON 해커톤 금상 (2등)** 수상
* **역할:** 장학금 데이터 크롤링 및 전처리, 추천 알고리즘(Rule-based Filtering) 설계, 앱 기획

---

## 🧐 2. Problem & Solution (문제 해결)
### ❌ Problem: 정보의 비대칭성
* 장학금 정보가 학교 홈페이지, 지자체, 재단별로 흩어져 있음.
* 자격 요건(학점 3.5 이상, 경기도 거주 등)이 복잡하여 일일이 확인하기 어려움.

### ⭕ Solution: 맞춤형 추천 알고리즘
* **Data Aggregation:** 흩어진 공고를 하나의 포맷(CSV/DB)으로 통합.
* **Smart Filtering:** 사용자 프로필(User Profile)과 공고의 자격 요건(Requirements)을 매칭하여 '지원 가능' 리스트만 도출.

---

## 💾 3. Data Pipeline & Processing (데이터 처리)
**(이 섹션이 핵심입니다. 전처리된 CSV 파일의 일부를 스크린샷으로 찍거나 테이블로 표현하세요.)**

장학금 공고마다 제각각인 데이터 형식을 통일하기 위해 전처리 파이프라인을 구축했습니다.

### 3.1. Data Structure
수집된 비정형 텍스트 데이터를 분석 가능한 정형 데이터(Structured Data)로 변환했습니다.

| Scholarship ID | Organization | Min GPA | Income Level | Residence | Deadline |
| :--- | :--- | :---: | :---: | :--- | :--- |
| S_001 | OO장학재단 | 3.5 | 8구간 이하 | 서울 | 2025-12-31 |
| S_002 | XX기업장학금 | - | 무관 | 전국 | 2025-01-15 |

### 3.2. Preprocessing Logic
* **결측치 처리:** 학점 기준이 없는 경우 `0.0` 또는 `None`으로 표준화하여 필터링 로직에서 제외되지 않도록 처리.
* **자격 요건 파싱(Parsing):** "평점 3.0 이상, 4.0 만점 기준" 등의 자연어 텍스트를 `min_gpa: 3.0`, `scale: 4.0` 수치형 데이터로 변환.
* **카테고리화:** 소득 분위, 지역 조건 등을 범주형 데이터(Categorical Data)로 매핑.

---

## 📱 4. Key Features & UI (주요 기능)
**(앱 구동 화면이나 와이어프레임 이미지를 여기에 넣어주세요. ex: `![App Screenshot](./assets/app_flow.png)`)**

1.  **전체 장학금 리스트:** DB에 적재된 모든 장학금을 마감일 순으로 조회.
2.  **마이 페이지 (프로필 설정):** 내 학교, 학점, 거주지, 소득분위 입력.
3.  **맞춤 추천 (Smart Match):** 입력된 정보를 바탕으로 **지원 가능한 공고**만 필터링하여 노출.
    > *Logic: (User.GPA >= Scholarship.Min_GPA) AND (User.Loc IN Scholarship.Target_Loc)*

---

## 🛠 5. Retrospective (회고)
*(본인이 데이터를 다루며 느낀 점을 강조하세요)*

* **데이터 구조화의 중요성:** 제각각인 공고문을 하나의 스키마(Schema)로 정의하는 과정에서 데이터 모델링의 중요성을 배웠습니다.
* **알고리즘 최적화:** 초기에는 단순 `if-else`문이 많아지며 속도 저하가 우려되었으나, Pandas DataFrame의 벡터 연산을 활용해 필터링 속도를 개선했습니다. (코드 부재로 로직 설명으로 대체)
* **사용자 관점:** 단순히 리스트만 보여주는 것이 아니라, '왜 추천되었는지' 이유를 함께 보여주는 UI를 기획하여 UX를 개선했습니다.

---

## 📂 Repository Structure
* `/data` : 전처리된 장학금 데이터 샘플 (Sample CSV)
* `/assets` : 앱 구동 화면 및 시연 영상, 발표 자료 (PPT)
* `/docs` : 해커톤 기획서 및 알고리즘 흐름도
