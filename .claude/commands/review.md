/project:review — PR 코드 리뷰
사용법
/project:review          → 최근 커밋 1개 리뷰
/project:review branch   → 현재 브랜치 전체 리뷰 (main 대비)
/project:review 3        → 최근 N개 커밋 리뷰

실행 지시
Step 1. 리뷰 대상 결정
아래 로직으로 $ARGUMENTS 값을 판단한다.
$ARGUMENTS 없음        → git diff HEAD~1 HEAD
$ARGUMENTS = "branch"  → git diff main...HEAD
$ARGUMENTS = 숫자 N    → git diff HEAD~N HEAD
Step 2. diff 수집
결정된 명령어를 실행해서 변경된 코드를 가져온다.
함께 실행할 보조 명령어:
bashgit log --oneline -5          # 최근 커밋 맥락 파악
git diff --stat HEAD~1 HEAD   # 변경된 파일 목록 overview
Step 3. 에이전트 병렬 실행
수집한 diff를 기반으로 아래 4개 에이전트를 병렬로 실행한다.
.claude/agents/readability-agent.md
.claude/agents/logic-agent.md
.claude/agents/bestpractice-agent.md
.claude/agents/growth-agent.md
각 에이전트는 동일한 diff를 독립적으로 분석한다.
Step 4. 결과 통합 출력
아래 형식으로 리뷰 결과를 출력한다.

출력 형식
## 👋 코드 리뷰 결과

**리뷰 대상:** [실행된 git 명령어]
**변경 파일:** [git diff --stat 결과]
**커밋:** [git log 결과]

---

### ✨ 잘하신 점
[반드시 1개 이상, 구체적 파일명/라인 언급]

---

### 🎯 이번 핵심 학습 포인트
> 한 번에 다 고치려 하지 말고, 이 3가지만 집중해보세요.

1. 
2. 
3. 

---

### 📚 상세 피드백

<details>
<summary>🔍 가독성 리뷰 (readability-agent)</summary>

[readability-agent 결과]

</details>

<details>
<summary>⚙️ 로직 리뷰 (logic-agent)</summary>

[logic-agent 결과]

</details>

<details>
<summary>📐 Best Practice 리뷰 (bestpractice-agent)</summary>

[bestpractice-agent 결과]

</details>

<details>
<summary>🌱 성장 리포트 (growth-agent)</summary>

[growth-agent 결과]

</details>

---

### 🚀 다음 단계 추천
[growth-agent의 다음 학습 추천 내용]

심각도 기준
심각도기준🔴 반드시 수정보안 취약점, 명백한 버그🟡 수정 권장나쁜 습관, 로직 불안정🟢 개선 제안더 나은 방법 존재
🔴 1개 이상 → 커밋 전 반드시 수정
🟡 3개 이상 → 수정 권장
🟢 이하만 → 다음 단계로 진행 가능