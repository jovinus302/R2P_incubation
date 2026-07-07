# S0 — Seed Intake

**PURPOSE**: 원시 입력(키워드, 논문 초록, 트렌드 URL)을 구조화된 시드로 정규화 + **시드 설득력 게이트** — 이길 수 없는 판에 run 전체를 태우지 않는다. 파이프라인 하류는 시드에 없던 파급력을 만들 수 없다.

**INPUT**: 사용자 자유 텍스트 또는 URL (S0.5 소싱 산출물이면 사전 채점 첨부)
**OUTPUT**: `runs/<run-id>/00-seed.md` (`templates/00-seed-intake.md` 채움, 3문 판정 포함)
**AGENT**: orchestrator 직접 (폼 채우기) + `opus-architect` ×1 P3 페르소나 (3문 게이트 판정)

**절차**:
1. `runs/<YYYYMMDD>-<slug>/` 생성
2. 템플릿 채움. 모르는 필드는 비워두지 말고 추정 + `(추정)` 표기
3. **시드 3문 게이트**: P3 페르소나(`process/reference/personas/p3-cto-strategy-vp.md`)를 입은 opus-architect 1콜로 판정. 기준 = frame 명료성 (완성된 테제 요구 금지 — 가설 진위는 S1 몫):
   - PASS → 진행
   - WEAK → 보강 조건 명시, 인간 체크포인트 상신 후 진행 (S1이 가설 진위 검증)
   - **FAIL(frame 부재·자산 optional) → BLOCKING. run 미착수** — 시드 반려 또는 재프레이밍 유도 (FAIL은 종단이 아니라 재프레이밍 신호)
4. Open questions에 [BLOCKING] 있으면 사용자에게 2–3개 질문 후 진행. 없으면 자동 진행
5. `run-log.md` 시작 (3문 판정 기록 포함)

**QUALITY BAR**: 시드만 읽고 S1 리서처가 검색 쿼리를 만들 수 있어야 함. 3문 판정과 근거가 seed 파일에 기록돼 있어야 함.
**FAILURE MODES**: 스코프 무한정 ("AI로 뭔가") → BLOCKING 질문으로 좁힌다. 시드에 이미 제품 아이디어가 박혀 있음 → 기술/능력 층위로 되돌려 기술하고, 원 아이디어는 S3 합류용 idea card로 별도 보존. 순수 능력 나열 시드(round 2 frontier-AI 꼴) → 3문 FAIL, S0.5 역산 소싱으로 우회 권고.
