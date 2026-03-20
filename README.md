# 📊 HolySheet

> 금융 API 자동 연동과 AI 분석으로 소비 습관을 개선하는 청년 타겟 모바일 앱

![Status](https://img.shields.io/badge/status-in--development-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 💡 개요

간편결제(카카오페이, 네이버페이, 토스 등) 확산으로 소액 결제가 반복·누적되며 월말에 예상치 못한 지출로 이어지는 현상이 빈번하다. 기존 가계부 앱은 수동 입력 부담과 단순 기록에 그쳐 실질적인 소비 습관 개선까지 연결되지 않는다.

HolySheet는 금융 API 자동 연동으로 입력 부담을 없애고, AI 챗봇이 소비 패턴을 분석해 맞춤형 피드백을 제공한다. 친구와의 비교·공유 기능과 목표 달성 시각화로 지속적인 습관 개선을 유도한다.

**타겟 사용자**

| 페르소나 | 특징 | 주요 니즈 |
|---|---|---|
| 대학생 (20대 초반) | 용돈·아르바이트 생활, 충동 소비 잦음 | 소비 패턴 파악 |
| 취준생 (20대 중반) | 고정 수입 없이 지출 관리 필요 | 예산 목표 설정, 절약 피드백 |
| 사회초년생 (20대 후반) | 첫 월급 후 소비 관리 시작 | 카테고리 분류, 소비 예측 |

---

## 🚀 주요 기능

| 우선순위 | 기능 | 설명 |
|---|---|---|
| 🔴 P0 | 소셜 로그인 | 카카오 / 구글 또는 이메일 가입 |
| 🔴 P0 | 소비 내역 자동 조회 | 금융 API 기반 카드 내역 자동 수집 |
| 🔴 P0 | AI 카테고리 자동 분류 | 지출 항목 자동 태깅 (식비, 쇼핑, 교통 등) |
| 🔴 P0 | 소비 그래프 대시보드 | 카테고리별 지출 시각화 |
| 🔴 P0 | 소비 목표 설정 | 월별·카테고리별 예산 설정 및 달성 현황 |
| 🟡 P1 | 소비 패턴 Q&A 챗봇 | "이번 달 어디서 제일 많이 썼어?" 등 자연어 질의 |
| 🟡 P1 | 챗봇 피드백 | 소비 분석 기반 개선 제안 메시지 |
| 🟡 P1 | 친구·연령대 비교 분석 | 동일 연령대 소비 동향 비교 그래프 |
| 🟡 P1 | 소비 예측 모델 | 현재 패턴 기반 이번 달 예상 지출 계산 |
| 🟡 P1 | 소비 점수 및 순위 | 소비 습관 점수화 및 또래 내 순위 제공 |
| 🟢 P2 | 맞춤 알림 | 사용자 성향 기반 소비 목표 알림 |
| 🟢 P2 | 소비 만족도 평가 | 지출 후 자기 평가 기능 |
| 🟢 P2 | 친구 기능 | 친구 추가·삭제·소비 현황 공유 |

---

## 📦 아키텍처
```
┌─────────────────────────────┐
│        Android App          │
│     (Kotlin + Compose)      │
└─────────────┬───────────────┘
              │
┌─────────────▼───────────────┐
│         API Gateway         │
│     (FastAPI / Spring)      │
└──────┬──────────────┬───────┘
       │              │
┌──────▼──────┐  ┌────▼────────────┐
│  FastAPI    │  │  Spring Boot    │
│ (AI · 분석) │  │ (금융 API · 비즈니스 로직) │
└──────┬──────┘  └────┬────────────┘
       │              │
       └──────┬───────┘
              │
┌─────────────▼───────────────┐
│            DB               │
│          (TBD)              │
└─────────────────────────────┘
```

---

## 🛠 기술 스택

**Android**
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?logo=kotlin&logoColor=white)
![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-4285F4?logo=jetpackcompose&logoColor=white)

**AI / 분석 서버**
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?logo=langchain&logoColor=white)

**비즈니스 서버**
![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?logo=springboot&logoColor=white)

**DB**
![TBD](https://img.shields.io/badge/DB-TBD-lightgrey)

**인프라**
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)

---

## 📁 레포지토리 구조
```
holysheet/
├── android/              # Kotlin Android 앱
├── fastapi/              # Python FastAPI 서버 (AI·ML·분석)
├── spring/               # Spring 서버 (금융 API 연동·비즈니스 로직)
├── docs/                 # API 스펙, ERD, 공통 문서
│   ├── api-spec.yaml     # OpenAPI 3.0
│   └── erd.md
└── .github/
    └── workflows/
        ├── android.yml   # paths: android/**
        ├── fastapi.yml   # paths: fastapi/**
        └── spring.yml    # paths: spring/**
```

---

## 🚀 시작하기

### 사전 요구사항

- Android Studio (Hedgehog 이상)
- Python 3.11+
- Java 17+

### 로컬 실행
```bash
# 레포 클론
git clone https://github.com/your-org/holysheet.git
cd holysheet

# FastAPI 서버
cd fastapi
pip install -r requirements.txt
uvicorn main:app --reload

# Spring 서버
cd spring
./gradlew bootRun

# Android 앱
# Android Studio에서 android/ 디렉토리 열기
```

---

## 🌿 브랜칭 전략
```
main
└── develop
    ├── feature/android-*
    ├── feature/fastapi-*
    └── feature/spring-*
```

- `main` : 배포 브랜치 — 직접 push 금지
- `develop` : 통합 브랜치
- `feature/*` : 기능 단위 개발 → PR → develop 머지

---

## 👥 팀 역할

| 이름 | 담당 |
|---|---|
| 유승환 | 데이터 분석, 시각화, ML, 백엔드, DevOps |
| 윤민재 | 백엔드 금융 API 연동, 브랜칭 전략, GitHub 협업 관리, DevOps |
| 정찬영 | DB, 풀스택, Git 외 협업 관리 |
| 김현진 | 챗봇, 프론트, 문서화 |

---

## 📅 개발 일정

| 단계 | 기간 |
|---|---|
| 기획 및 설계 | 3월 2주 ~ 3월 4주 |
| 개발 | 4월 ~ 6월 |
| 출시 목표 | 6월 말 |

---

## ⚠️ 제약 사항

- **금융 API** : 오픈뱅킹·카드사 API 승인 일정 고려 필요. 불가 시 SMS 파싱 또는 CSV 업로드 방식으로 대체 검토
- **데이터 보안** : 개인 금융 정보 포함 → 개인정보보호법 준수 필수
- **서버 비용** : 무료 티어 우선 사용

---

## 📄 라이선스

MIT