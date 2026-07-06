# S4 — Brief Writing + 레드팀

**PURPOSE**: 상위 2–3개를 CTO-ready 브리프로 확장, 페르소나 레드팀 통과 후 확정.

**INPUT**: 선정된 idea cards, `10-research-digest.md`, `30-scoring.md`, `templates/40-idea-brief.md`
**OUTPUT**: `runs/<run-id>/briefs/brief-<n>-<slug>.md` ×2–3, `40-run-summary.md`
**AGENT**: sonnet-analyst 초안 (브리프당 1개, 병렬) → opus-architect 레드팀 1패스 → orchestrator 반영·확정

**DELEGATION PROMPT — 초안** (브리프당):
> 첨부한 idea card를 `templates/40-idea-brief.md` 템플릿의 전체 브리프로 확장하라. 근거는 첨부한 리서치 다이제스트에서 인용 (새 사실 지어내기 금지, 다이제스트에 없으면 "확인 필요" 표기). 2–3페이지 하드캡. 아키텍처 설명 금지 — 사용자가 보고 만지는 것 중심. 섹션 7(데이터 의존성)과 섹션 9(2주 MVP 스케치)는 특히 구체적으로.

**DELEGATION PROMPT — 레드팀** (전체 브리프 1패스):
> 두 페르소나 파일(P1, P2)을 첨부한다. 각 브리프에 대해 두 페르소나 각각으로 "내가 이 상무라면 이 브리프를 반려하는 가장 강한 이유"를 작성하라. 추가 점검: (a) 2주 MVP가 정말 2주인가 (b) 기술 데모 위장인가 (c) go/no-go 훅이 CTO가 실제 결정 가능한 수준인가. 브리프당 VERDICT: APPROVE / APPROVE-WITH-CHANGES(필수 수정 목록) / REJECT(사유).

**확정**: orchestrator가 수정 반영 → `briefs/` 최종본 → `templates/41-run-summary.md`로 비교표 작성 → run-log 완성 → run 폴더 커밋.

**QUALITY BAR**: 레드팀 REJECT 브리프는 CTO에 안 나감. run-summary 1페이지 하드캡.
**FAILURE MODES**: 초안이 다이제스트에 없는 사실 인용 → 해당 주장 제거 또는 "확인 필요". 전 브리프 REJECT → S3 차순위로 1회 재시도, 그래도 실패면 시드 약함 보고.
