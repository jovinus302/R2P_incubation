# S2 — Idea Generation (발산)

**PURPOSE**: 시드+다이제스트에서 서로 다른 제품 아이디어 10–12개. 다양성·수량 > 완성도.

**INPUT**: `00-seed.md`, `10-research-digest.md`, `process/reference/generation-lenses.md`
**OUTPUT**: `runs/<run-id>/20-idea-candidates.md` (idea card 10–12개)
**AGENT**: `sonnet-analyst`

**DELEGATION PROMPT**:
> 첨부한 시드와 리서치 다이제스트를 기반으로 제품 아이디어 10–12개를 생성하라. 각 아이디어는 `templates/20-idea-card.md` 형식 (문제/타깃 유저/제품 컨셉/why this tech/근접 제품과 차별점, 8줄 이내). generation-lenses.md의 렌즈를 최소 6개 이상 커버하라. 자기 검열 금지 — 과감한 아이디어는 버리지 말고 [WILD] 태그. 각 카드에 SAFE/STRETCH/WILD 태그. 아이디어끼리 타깃 유저나 코어 루프가 겹치면 하나로 합치고 새로 발산하라. cold-start 데모 가능 여부를 카드마다 1줄로 표기하라 (round 1 교훈).

**QUALITY BAR**: 12개 중 최소 3개는 서로 완전히 다른 유저 세그먼트. WILD 최소 2개.
**FAILURE MODES**: 전부 같은 아이디어의 변형 → 렌즈 커버리지 재확인 후 재실행. 기술 데모 위장 (anti-patterns.md 냄새) → 해당 카드에 플래그.
