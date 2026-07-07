# S3 — Filter & Score (수렴, 트리플 페르소나)

**PURPOSE**: 약한 아이디어를 명시적 근거로 kill, 생존자를 루브릭 채점, 상위 2–3개 선정.

**INPUT**: `20-idea-candidates.md` (+ 사용자 제출 idea card 있으면 합류), `10-research-digest.md`, `templates/30-scoring-rubric.md`, 페르소나 파일 3개
**OUTPUT**: `runs/<run-id>/30-scoring.md`
**AGENT**: `opus-architect` ×3 병렬 (P1/P2/P3 페르소나 각각) → orchestrator 합의표

**트랙 부여** (채점 전, orchestrator): 각 후보에 D(데모) 또는 S(전략 베팅) 트랙 부여. S 배정은 "왜 D로 못 하나" 근거 필수 — S트랙은 데모 실패의 탈출구가 아님. 페르소나는 채점 중 트랙 배정에 이의 가능.

**DELEGATION PROMPT** (×3, `{persona}` = 페르소나 파일 전문):

> 너는 다음 인물이다: {persona 파일 전문}. 이 인물의 렌즈·질문·kill 신호·채점 성향을 완전히 체화하고 채점하라.
> 첨부한 아이디어 카드들을 `templates/30-scoring-rubric.md` (v3)로 평가하라:
> 1. 하드 게이트 먼저 — G1, 그리고 트랙별 G2-D 또는 G2-S. 실패는 즉시 kill, 이유 1줄
> 2. 생존자에 8개 기준 각 1–5점 + 가중합. 전략 자산(활용 필요성)과 moat(방어 지속성)에 같은 근거 이중 계상 금지
> 3. 데이터 의존성 체크 — cold-start NO여도 즉시 캡 아님. 신뢰 가능한 wedge 설계가 있으면 캡 없음, wedge가 없거나 허구적일 때만 "2주 MVP 데모성" 최대 2점
> 4. 아이디어당 이 페르소나의 전형적 질문 중 가장 아픈 질문 1개와 그 답 가능 여부
> DECISION/RATIONALE/RISKS 형식. 캘리브레이션 앵커(`runs/round1-retrospective/`)가 있으면 참조하되 v3 점수와 액면 비교 금지 — 인플레이션 방지 목적으로만.

**합의표** (orchestrator): 루브릭 v3의 점수표 형식(트랙·P3 열 포함). 3인 중 2인 이상 3.0 미만 → kill. **moat 하한**: 2인 이상 moat ≤2 → 전략 advance 불가(재프레이밍 또는 "데모-only" 라벨). 1.0 이상 갈림 → 이유 명시(P3 vs P1/P2 갈림은 CTO 보고 신호). `review_shortlist: yes`면 여기서 인간 확인. **S트랙 advance는 review_shortlist 여부와 무관하게 인간 체크포인트 강제** (v3 첫 run들은 S트랙 앵커 부재).

**QUALITY BAR**: 모든 kill에 1줄 근거. advance 2–3개(트랙 무관 merit), 3.0 미만 advance 금지 (쿼터 채우기 금지). S트랙을 "데모성 낮음"만으로 kill 금지.
**FAILURE MODES**: 페르소나 점수 사실상 동일(특히 P3가 P1/P2와 동일) → 페르소나 주입 실패, 재실행. advance 0개 → 시드 약함, S4 강행 금지.
