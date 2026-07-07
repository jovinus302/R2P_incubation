# S2 — Idea Generation (발산)

**PURPOSE**: 시드+다이제스트에서 서로 다른 제품 아이디어 10–12개. 다양성·수량 > 완성도. 단, 발산 시점부터 CTO급 앵커를 인지 — 하류가 시드에 없던 파급력을 만들 수 없듯, S3가 발산에 없던 moat를 만들 수 없다.

**INPUT**: `00-seed.md`, `10-research-digest.md`, `process/reference/generation-lenses.md`, `templates/30-scoring-rubric.md`의 "CTO급 정의" 섹션
**OUTPUT**: `runs/<run-id>/20-idea-candidates.md` (idea card 10–12개)
**AGENT**: `sonnet-analyst` (기본). 시드가 테제·frontier 필수성 중심이거나 파급력 요구가 명시된 run은 opus 격상 가능 — 격상 사유를 run-log에 기록.

**DELEGATION PROMPT**:
> 첨부한 시드와 리서치 다이제스트를 기반으로 제품 아이디어 10–12개를 생성하라. 각 아이디어는 `templates/20-idea-card.md` 형식. 채점 앵커: **CTO급 = 유통 너머의 moat, 재정의하는 테제, 복제 어려운 기술 깊이 중 하나 이상** — "구글/애플이 이미 파는 기능을 잘 만든 것"은 CTO급이 아니다 (단 SAFE 대조군으로는 유지).
> 렌즈 규칙: generation-lenses.md의 렌즈를 최소 6개 커버하되, **렌즈 13(테제 우선)·14(wedge 설계)는 필수**, 16(복리 데이터 모트)·17(시스템 레이어 베팅) 중 최소 1개 커버.
> 카드 필수 필드: moat 가설(유통 제외), 경쟁 킬 테스트("구글/애플이 6개월 내 뻔한 버전 출시 → 남는 것"), 트랙 제안(D/S), cold-start 데모 여부.
> 구성 쿼터: 전략 베팅(S트랙 제안) 후보 최소 2개, SAFE 유틸 대조군 최소 2개 (단일 패스 안에서 대조 확보). WILD 최소 2개 — 자기 검열 금지, 과감한 아이디어는 버리지 말고 [WILD] 태그.
> 아이디어끼리 타깃 유저나 코어 루프가 겹치면 하나로 합치고 새로 발산하라.

**QUALITY BAR**: 12개 중 최소 3개는 서로 완전히 다른 유저 세그먼트. WILD 최소 2개. S트랙 제안 최소 2개 + SAFE 대조군 최소 2개. 경쟁 킬 테스트에 "남는 것 없음"이라 답하는 카드가 절반 초과면 발산 실패.
**FAILURE MODES**: 전부 같은 아이디어의 변형 → 렌즈 커버리지 재확인 후 재실행. 전 후보가 "빅테크 기존 기능 + 탑재 해자" 형태 → 렌즈 13/16/17 강조해 재실행. 기술 데모 위장 (anti-patterns.md 냄새) → 해당 카드에 플래그.
