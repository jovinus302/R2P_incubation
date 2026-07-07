# S1 — Research

**PURPOSE**: 사실 기반 구축 — 기술 성숙도, why-now 신호, 경쟁/인접 제품, prior art. 사실만, 인용 필수, 아이디어 생성 금지.

**INPUT**: `00-seed.md`
**OUTPUT**: `runs/<run-id>/10-research-digest.md` (orchestrator가 3개 결과 병합)
**AGENT**: `web-researcher` ×3 병렬

**DELEGATION PROMPT** (3개 각각, `{seed}` 치환):

패스 A — 기술 성숙도:
> 다음 기술 시드의 현재 상태를 조사하라: {seed 본문}. 핵심 논문/레포 최대 5개(URL 인용), 성숙도 판정(research/prototype/productizable), 최근 12–18개월에 새로 가능해진 것. FINDINGS는 URL 인용 필수. 제품 아이디어 제안 금지. SUMMARY/FINDINGS/OPEN QUESTIONS 형식.

패스 B — why-now·시장:
> 다음 기술 시드의 why-now 신호와 시장을 조사하라: {seed 본문}. 비용 곡선, 모델 능력 점프, 플랫폼 전환, 규제, 사용자 행동 변화. 이 문제를 오늘 누가 겪고 어떻게 해결하며 지불 의사 신호는 무엇인가. URL 인용 필수. 제품 아이디어 제안 금지. SUMMARY/FINDINGS/OPEN QUESTIONS 형식.

패스 C — 경쟁·prior art:
> 다음 기술 시드 관련 경쟁/인접 제품과 과거 실패 사례를 조사하라: {seed 본문}. 테이블: 제품|회사|하는 일|트랙션 신호|갭. 과거 유사 시도와 실패 원인 포함. URL 인용 필수. 제품 아이디어 제안 금지. SUMMARY/FINDINGS/OPEN QUESTIONS 형식.

**병합**: orchestrator가 `templates/10-research-digest.md` 구조로 병합, 섹션별 HIGH/MED/LOW confidence 태그. LOW는 run-log에 기록. **능력 랭킹을 "라이브 데모 안정성" 단일축으로 정렬 금지** — 신선도(최근 12–18개월 edge)·경쟁 공백 축 병기 (round 2 교훈: 안전성 단일축 다이제스트는 발산을 안전한 유틸로 밀어붙임).

**QUALITY BAR**: 모든 주장에 URL. 다이제스트만 읽고 S2가 시장 감각 있는 아이디어를 낼 수 있어야 함.
**FAILURE MODES**: 검색 실패로 빈 섹션 → 빈 채로 두고 LOW 표기 (지어내기 금지). 전략적 고위험 시드 → `deep-research` 스킬 격상 경로.
