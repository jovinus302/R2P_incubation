# S0 — Seed Intake

**PURPOSE**: 원시 입력(키워드, 논문 초록, 트렌드 URL)을 구조화된 시드로 정규화. 다운스트림 에이전트가 추측하지 않게.

**INPUT**: 사용자 자유 텍스트 또는 URL
**OUTPUT**: `runs/<run-id>/00-seed.md` (`templates/00-seed-intake.md` 채움)
**AGENT**: orchestrator 직접 (분석 아님, 폼 채우기)

**절차**:
1. `runs/<YYYYMMDD>-<slug>/` 생성
2. 템플릿 채움. 모르는 필드는 비워두지 말고 추정 + `(추정)` 표기
3. Open questions에 [BLOCKING] 있으면 사용자에게 2–3개 질문 후 진행. 없으면 자동 진행
4. `run-log.md` 시작

**QUALITY BAR**: 시드만 읽고 S1 리서처가 검색 쿼리를 만들 수 있어야 함.
**FAILURE MODES**: 스코프 무한정 ("AI로 뭔가") → BLOCKING 질문으로 좁힌다. 시드에 이미 제품 아이디어가 박혀 있음 → 기술/능력 층위로 되돌려 기술하고, 원 아이디어는 S3 합류용 idea card로 별도 보존.
