# S3 — Filter & Score (수렴, 듀얼 페르소나)

**PURPOSE**: 약한 아이디어를 명시적 근거로 kill, 생존자를 루브릭 채점, 상위 2–3개 선정.

**INPUT**: `20-idea-candidates.md` (+ 사용자 제출 idea card 있으면 합류), `10-research-digest.md`, `templates/30-scoring-rubric.md`, 페르소나 파일 2개
**OUTPUT**: `runs/<run-id>/30-scoring.md`
**AGENT**: `opus-architect` ×2 병렬 (P1/P2 페르소나 각각) → orchestrator 합의표

**DELEGATION PROMPT** (×2, `{persona}` = 페르소나 파일 전문):

> 너는 다음 인물이다: {persona 파일 전문}. 이 인물의 렌즈·질문·kill 신호·채점 성향을 완전히 체화하고 채점하라.
> 첨부한 아이디어 카드들을 `templates/30-scoring-rubric.md`로 평가하라:
> 1. 하드 게이트 G1/G2 먼저 — 실패는 즉시 kill, 이유 1줄
> 2. 생존자에 6개 기준 각 1–5점 + 가중합
> 3. 데이터 의존성 체크 — cold-start NO면 "2주 MVP 데모성" 최대 2점
> 4. 아이디어당 이 페르소나의 전형적 질문 중 가장 아픈 질문 1개와 그 답 가능 여부
> DECISION/RATIONALE/RISKS 형식. 캘리브레이션 앵커(`runs/round1-retrospective/`)가 있으면 참조해 점수 인플레이션 방지.

**합의표** (orchestrator): 루브릭의 점수표 형식. 두 페르소나 모두 3.0 미만 → kill. 1.0 이상 갈림 → 이유 명시. `review_shortlist: yes`면 여기서 인간 확인.

**QUALITY BAR**: 모든 kill에 1줄 근거. advance 2–3개, 3.0 미만 advance 금지 (쿼터 채우기 금지).
**FAILURE MODES**: P1/P2 점수 사실상 동일 → 페르소나 주입 실패, 재실행. advance 0개 → 시드 약함, S4 강행 금지.
