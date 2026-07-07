# S4 — Brief Writing + 레드팀/블루팀

**PURPOSE**: 상위 2–3개를 CTO-ready 브리프로 확장, 레드팀(결함 공격)과 블루팀(야망 복원)을 쌍으로 통과시킨 후 확정. 레드팀만 있으면 신선함이 단조 감소한다 — round 2 교훈.

**INPUT**: 선정된 idea cards, `10-research-digest.md`, `30-scoring.md`, `templates/40-idea-brief.md`, 페르소나 파일 3개
**OUTPUT**: `runs/<run-id>/briefs/brief-<n>-<slug>.md` ×2–3, `40-run-summary.md`
**AGENT**: sonnet-analyst 초안 (브리프당 1개, 병렬) → opus-architect 레드팀 1패스 (P1/P2/P3) → opus-architect 블루팀 1패스 → orchestrator 반영·확정

**DELEGATION PROMPT — 초안** (브리프당):
> 첨부한 idea card를 `templates/40-idea-brief.md` 템플릿의 전체 브리프로 확장하라. 근거는 첨부한 리서치 다이제스트에서 인용 (새 사실 지어내기 금지, 다이제스트에 없으면 "확인 필요" 표기). 2–3페이지 하드캡. 아키텍처 설명 금지 — 사용자가 보고 만지는 것 중심. 섹션 7(데이터 의존성)과 섹션 9(2주 MVP 스케치)는 특히 구체적으로. 카드의 moat 가설·경쟁 킬 테스트를 브리프에서 근거로 발전시켜라.

**DELEGATION PROMPT — 레드팀** (전체 브리프 1패스):
> 세 페르소나 파일(P1, P2, P3)을 첨부한다. 각 브리프에 대해 세 페르소나 각각으로 "내가 이 상무라면 이 브리프를 반려하는 가장 강한 이유"를 작성하라. 추가 점검: (a) 2주 MVP가 정말 2주인가 (b) 기술 데모 위장인가 (c) go/no-go 훅이 CTO가 실제 결정 가능한 수준인가 (d) P3: 경쟁 킬 테스트 — 구글/애플이 6개월 내 뻔한 버전을 내면 남는 것이 있는가, moat가 유통뿐 아닌가. 브리프당 VERDICT: APPROVE / APPROVE-WITH-CHANGES(필수 수정 목록) / REJECT(사유).

**DELEGATION PROMPT — 블루팀** (레드팀 반영 후 1패스, 대항 발산 압력):
> 레드팀 수정이 반영된 브리프를 첨부한다. 각 브리프에 대해 물어라: "이 아이디어의 **가장 야심차고 방어 가능한 버전**은 무엇인가. 레드팀이 깎아낸 것 중 복원할 가치가 있는 야망은 무엇이고, 어떤 wedge/슬라이스 설계면 리스크 없이 복원되는가. moat를 한 단계 강화하는 경로(복리 루프, 통합 깊이)가 브리프에 빠져 있지 않은가." 스코프 인플레 금지 — 복원 제안은 반드시 wedge 또는 검증 슬라이스 설계를 동반해야 유효. 브리프당 복원/강화 제안 최대 3건 + 각 1줄 근거.

**확정**: orchestrator가 레드팀 수정 + 블루팀 제안 중 채택분 반영 → `briefs/` 최종본 (헤더의 레드팀/블루팀 상태를 실제 판정으로 갱신 — "예정" 잔존 금지) → `templates/41-run-summary.md`로 비교표 작성 → run-log 완성 → run 폴더 커밋.

**QUALITY BAR**: 레드팀 REJECT 브리프는 CTO에 안 나감. 블루팀 제안은 wedge/슬라이스 동반 시만 반영. run-summary 1페이지 하드캡.
**FAILURE MODES**: 초안이 다이제스트에 없는 사실 인용 → 해당 주장 제거 또는 "확인 필요". 전 브리프 REJECT → S3 차순위로 1회 재시도, 그래도 실패면 시드 약함 보고. 블루팀 제안이 전부 스코프 인플레 → 반영 없이 기각 기록만.
