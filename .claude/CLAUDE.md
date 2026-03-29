# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

HolySheet is a mobile-first financial management platform targeting young adults (20s). It uses financial APIs and AI to automatically categorize expenses and provide personalized spending analysis.

## Repository Structure

```
holysheet/
├── android/        # Kotlin + Jetpack Compose Android app
├── fastapi/        # Python FastAPI server (AI, ML, analytics)
├── spring/         # Java Spring Boot server (financial API, business logic)
├── docs/           # API specs (OpenAPI 3.0), ERD
└── .github/workflows/  # CI per service (android.yml, fastapi.yml, spring.yml)
```

> Note: As of early development, `android/`, `fastapi/`, and `spring/` are placeholder directories pending implementation.

## Architecture

The system uses two backend services behind an API Gateway:

- **FastAPI** (Python): AI/ML features — LangChain-powered expense categorization, chatbot Q&A, spending analysis
- **Spring Boot** (Java): Business logic — financial API integration, user/account management
- **Android** (Kotlin + Compose): Mobile client, only platform targeted

Both servers share a single database (TBD).

## Commands

### FastAPI server

```bash
cd fastapi
pip install -r requirements.txt
uvicorn main:app --reload
```

### Spring server

```bash
cd spring
./gradlew bootRun
```

### Android app

Open the `android/` directory in Android Studio (Hedgehog or later).

## Requirements

- Python 3.11+
- Java 17+
- Android Studio Hedgehog+

## Branching Strategy

- `main`: production — no direct push
- `develop`: integration branch
- `feature/android-*`, `feature/fastapi-*`, `feature/spring-*`: feature branches → PR → merge to `develop`

## Constraints

- **Financial APIs**: Open banking / card company API approvals may delay integration. Fallback: SMS parsing or CSV upload.
- **Data security**: Personal financial data is involved — must comply with 개인정보보호법 (Korean Personal Information Protection Act).
- **Server costs**: Free-tier services preferred.

