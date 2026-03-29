# Claude Code 슬래시 커맨드 가이드

이 프로젝트에서 사용할 수 있는 커스텀 슬래시 커맨드 목록과 사용법입니다.

---

## 커맨드 목록

| 커맨드 | 설명 |
|---|---|
| `/project:review` | AI 에이전트 기반 자동 코드 리뷰 |
| `/project:rubberduck` | 대화형 러버덕 학습 모드 |

---

## `/project:review` — 코드 리뷰

커밋/브랜치의 diff를 4개 전문 에이전트가 병렬 분석합니다.

### 사용법

```
/project:review          → 최근 커밋 1개 리뷰
/project:review branch   → 현재 브랜치 전체 리뷰 (main 대비)
/project:review 3        → 최근 N개 커밋 리뷰
```

### 분석 에이전트

| 에이전트 | 역할 |
|---|---|
| `readability-agent` | 네이밍, 주석, 코드 구조, 보안(하드코딩 등) |
| `logic-agent` | 로직 정확성, 엣지 케이스, 알고리즘 |
| `bestpractice-agent` | 언어/프레임워크 Best Practice, 컨벤션 |
| `growth-agent` | 성장 패턴 분석, 성능 이슈, 다음 학습 추천 |

### 심각도 기준

| 심각도 | 기준 | 행동 기준 |
|---|---|---|
| 🔴 반드시 수정 | 보안 취약점, 명백한 버그 | 커밋 전 반드시 수정 |
| 🟡 수정 권장 | 나쁜 습관, 로직 불안정 | 🟡 3개 이상이면 수정 권장 |
| 🟢 개선 제안 | 더 나은 방법 존재 | 여유 있을 때 개선 |

---

## `/project:rubberduck` — 러버덕 학습 모드

답을 바로 주는 대신, 스스로 사고하고 설명하는 능력을 키우도록 유도하는 대화형 학습 모드입니다.

> **핵심 원칙:** 학습자가 말하는 시간 > AI가 말하는 시간

### 사용법

```
/project:rubberduck          → 러버덕 모드 시작 (상황은 대화로 파악)
/project:rubberduck debug    → 디버깅 모드로 바로 시작
/project:rubberduck concept  → 개념 학습 모드로 바로 시작
/project:rubberduck design   → 설계/아키텍처 모드로 바로 시작
/project:rubberduck review   → 코드 리뷰 러버덕 모드 (에이전트 자동 리뷰 X)
```

> 에이전트 자동 리뷰를 원하면 `/project:review`를 사용하세요.

### 상황별 모드

| 모드 | 트리거 예시 | 진행 방식 |
|---|---|---|
| `debug` | "이 코드 왜 안 돼?", "에러 나는데" | 현상 → 예상 원인 → 범위 좁히기 → 모순 발견 순서로 질문 |
| `concept` | "이게 뭔지 모르겠어", "이 개념 설명해줘" | 현재 이해 확인 → 설명하게 유도 → 모순으로 심화 |
| `design` | "이렇게 설계하면 돼?", "구조 어떻게 잡아?" | 설명 → 단점 끌어내기 → 대안 탐색 → 결정 유도 |
| `review` | "이 코드 봐줘", "이거 괜찮아?" | 학습자가 먼저 문제를 찾도록 질문 유도 |

### 힌트 정책

| 상황 | 동작 |
|---|---|
| 3회 이하 시도, 막힘 | 질문으로 유도 계속 |
| 3회 초과, 여전히 막힘 | 방향 힌트 제공 (코드 직접 제시 X) |
| "답 직접 줘" 요청 | 더 구체적인 힌트로 타협 |
| 강하게 재요청 | 힌트 수준 최대로 높이되 최종 답은 주지 않음 |

---

## 파일 구조

```
.claude/
├── CLAUDE.md                   # 프로젝트 전체 가이드 (Claude Code 자동 로드)
├── COMMANDS.md                 # 이 파일 — 커맨드 사용법
├── commands/
│   ├── review.md               # /project:review 프롬프트
│   └── rubberduck.md           # /project:rubberduck 프롬프트
└── agents/
    ├── readability-agent.md    # 가독성·보안 리뷰 에이전트
    ├── logic-agent.md          # 로직 리뷰 에이전트
    ├── bestpractice-agent.md   # Best Practice 리뷰 에이전트
    └── growth-agent.md         # 성장 리포트·성능 에이전트
```
