# ✈️ 항공사 추천 프로젝트

## **클라이언트에게 추천해줄 TOP5 항공사 선정**

---

## 📌 프로젝트 개요

본 프로젝트는 **뉴욕 지역 항공편 데이터를 활용하여**,

* 자사(위치: 뉴욕)를 방문한 클라이언트들에게 **각자의 공항으로 돌아가는 최적의 항공사 추천**
* 운영 규모와 신뢰성을 기준으로 한 **5대 항공사 선정**
* **주중/주말별 맞춤형 항공사 추천 시스템** 구축
* 4가지 핵심 지표를 통한 **데이터 기반 의사결정 지원**

분석 내용을 담고 있습니다. 참고로 최종 파일은 cd 폴더안의 cd.qmd 입니다.

---

## 🚀 주요 분석 과정

| 분석 단계 | 설명 |
| ----------- | ------------------------------------- |
| 🏢 **5대 항공사 선정** | 운영 규모와 안정성 기준 대형 항공사 선별 |
| 📊 **규모 분석** | 운영 횟수, 비행거리, 보유 항공기, 좌석 수 분석 |
| 📅 **주중/주말 분석** | 시기별 맞춤형 추천을 위한 세분화 분석 |
| 🎯 **종합 점수 산정** | 4가지 지표 정규화 후 종합 순위 산출 |

---

## 🧰 기술 스택

| 분야 | 사용 기술 |
| ----- | ------------------------------------------------------------ |
| 언어 | Python |
| 프레임워크 | Quarto (RevealJS 발표) |
| 데이터 소스 | nycflights13 패키지 |
| 시각화 | Matplotlib, Seaborn |
| 데이터 처리 | Pandas, NumPy |
| 분석 기법 | 최댓값 정규화, 레이더 차트, 스택 막대 그래프 |

---

## 📈 데이터 설명

### 🗂️ 데이터 출처
**nycflights13 패키지**: 2013년 뉴욕 3개 공항 출발 항공편 데이터

### 📊 주요 데이터셋

#### 1. Flights 데이터셋
| 변수명 | 유형 | 설명 |
| ------ | ---- | ---- |
| **year, month, day** | 수치형 | 항공기 출발 날짜 |
| **dep_delay** | 수치형 | 출발 지연 시간 (분) |
| **carrier** | 범주형 | 항공사 코드 |
| **tailnum** | 범주형 | 항공기 등록 코드 |
| **origin** | 범주형 | 출발 공항 (LGA, JFK, EWR) |
| **dest** | 범주형 | 도착 공항 |
| **distance** | 수치형 | 비행 거리 (마일) |

#### 2. Planes 데이터셋
| 변수명 | 유형 | 설명 |
| ------ | ---- | ---- |
| **tailnum** | 범주형 | 항공기 등록 코드 |
| **year** | 수치형 | 제조 연도 |
| **manufacturer** | 범주형 | 제조사 |
| **model** | 범주형 | 항공기 모델 |
| **seats** | 수치형 | 좌석 수 |
| **engines** | 수치형 | 엔진 수 |

### 🛫 분석 대상 공항
- **LGA** (LaGuardia Airport)
- **JFK** (John F. Kennedy International Airport)  
- **EWR** (Newark Liberty International Airport)

---

## 🔧 분석 방법론

### 📍 1단계: 5대 항공사 선정 기준

**선정 조건:**
1. **뉴욕 3개 공항 모두에서 운영** (접근성 보장)
2. **운영 규모가 큰 항공사** (안정성 및 신뢰도)

**평가 지표:**
- 총 운영 횟수
- 총 비행 거리
- 보유 항공기 수
- 총 좌석 수

**점수 산정:**
```
각 지표별 정규화 점수 = 항공사 값 / 최댓값
종합 점수 = 4개 지표 정규화 점수의 합
```

### 📍 2단계: 주중/주말별 맞춤 분석

**분석 기준:**
- **주중**: 월요일 ~ 목요일
- **주말**: 금요일 ~ 일요일

**4가지 핵심 지표:**
1. **총 운항 수**: 선택 옵션의 다양성
2. **평균 지연 시간**: 정시성 및 신뢰성
3. **정시 운항 비율**: ±5분 이내 출발 비율
4. **경로 다양성**: 도착지 수 (네트워크 범위)

### 📍 3단계: 최댓값 정규화 방식

| 지표 | 계산 방식 | 예시 |
|------|-----------|------|
| 운항 횟수 | 항공사 운항 수 / 최대 운항 수 | 25,000 / 25,000 = 1.0 |
| 지연 시간 | 1 / (평균 지연 시간 + 1) 후 정규화 | 낮을수록 높은 점수 |
| 정시 비율 | 정시 비율 / 최대 정시 비율 | 85% / 90% = 0.94 |
| 경로 다양성 | 도착지 수 / 최대 도착지 수 | 80 / 100 = 0.8 |

---

## 📊 주요 분석 결과

### 🏆 5대 항공사 선정 결과

| 순위 | 항공사 코드 | 항공사명 | 종합 점수 | 특징 |
|------|-------------|----------|-----------|------|
| 1 | **UA** | United Airlines | 최고점 | 운영 규모 1위 |
| 2 | **AA** | American Airlines | 고득점 | 네트워크 광범위 |
| 3 | **B6** | JetBlue Airways | 상위권 | 서비스 품질 우수 |
| 4 | **DL** | Delta Air Lines | 상위권 | 안정적 운영 |
| 5 | **EV** | ExpressJet Airlines | 상위권 | 경로 다양성 우수 |

### 📅 주중 추천 순위

| 순위 | 항공사 | 종합 점수 | 강점 |
|------|--------|-----------|------|
| 🥇 | **UA** | 최고점 | 모든 지표에서 균형잡힌 성능 |
| 🥈 | **DL** | 고득점 | 정시성과 안정성 우수 |
| 🥉 | **B6** | 상위권 | 서비스 품질과 고객 만족도 |
| 4 | **EV** | 중상위 | 경로 다양성 특화 |
| 5 | **AA** | 중위권 | 네트워크 광범위하나 지연 다소 |

### 🎉 주말 추천 순위

| 순위 | 항공사 | 종합 점수 | 강점 |
|------|--------|-----------|------|
| 🥇 | **DL** | 최고점 | 주말 운영 효율성 1위 |
| 🥈 | **UA** | 고득점 | 안정적인 주말 서비스 |
| 🥉 | **B6** | 상위권 | 주말 여행객 특화 서비스 |
| 4 | **EV** | 중상위 | 다양한 주말 노선 |
| 5 | **AA** | 중위권 | 대형 항공사 안정성 |

---

## 💡 핵심 인사이트

### 🎯 **종합 추천: UA & DL**

**선정 근거:**
- ✅ **UA**: 주중/주말 모두 상위권, 종합적 우수성
- ✅ **DL**: 주말 1위, 정시성과 안정성 특화
- ✅ **B6**: 서비스 품질 우수, 중단거리 특화
- ⚖️ **EV**: 경로 다양성 우수하나 규모 제한
- ⚠️ **AA**: 네트워크 광범위하나 지연 시간 이슈

### 🌟 클라이언트별 맞춤 추천

**비즈니스 출장객**: 
- 주중 → **UA** (균형잡힌 성능)
- 주말 → **DL** (정시성 우수)

**여가 여행객**:
- 서비스 중시 → **B6** (고객 만족도)
- 경로 다양성 → **EV** (다양한 목적지)

**대형 그룹 여행**:
- 안정성 우선 → **AA** (대형 항공사 신뢰도)

### 📈 시기별 특징

**주중 vs 주말 차이점:**
- 주중: 비즈니스 수요로 정시성 중요
- 주말: 여가 수요로 서비스 품질 중요
- DL은 주말 운영에서 특히 강점 보유

---

## 📊 시각화 특징

### 🕸️ 레이더 차트
- **극좌표(polar) 그래프** 활용
- 4개 지표를 방사형으로 배치
- 항공사별 강점/약점 한눈에 비교
- 투명도 조절로 겹치는 영역 시각화

### 📊 스택 막대 그래프
- 4개 지표별 기여도 시각화
- 색상별 구분으로 지표 식별 용이
- 총점 표시로 순위 명확화

---

## 🔧 시스템 구성

### ① 데이터 전처리
* nycflights13 패키지에서 flights, planes 데이터 로드
* 날짜 기반 주중/주말 분류
* 항공사별 데이터 집계 및 정리

### ② 항공사 선정
* 3개 공항 운영 항공사 필터링
* 4가지 규모 지표 계산
* 정규화 점수 및 종합 순위 산출

### ③ 추천 분석
* 주중/주말별 4가지 지표 계산
* 최댓값 정규화 및 종합 점수 산정
* 항공사별 순위 및 특징 분석

### ④ 시각화
* 레이더 차트 생성 (극좌표 활용)
* 스택 막대 그래프 구현
* 항공사별 색상 매핑 및 범례 설정

### ⑤ 발표자료
* Quarto RevealJS 기반 프레젠테이션
* 단계별 분석 과정 시각화
* 항공사 추천 결과 및 근거 제시

---

## 👥 프로젝트 구성원
* 홍주형, 신지원, 이주연, 한규민
