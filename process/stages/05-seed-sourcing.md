# S0.5 — Seed Sourcing (역산, 선택 스테이지)

**PURPOSE**: 기술 트렌드에서 출발하지 않고 **CTO/소장 발언·전략 우선순위·경쟁 위협에서 역산**한 시드 후보를 여러 개 싸게 만들어 경쟁시킨다. 시드가 단수 입력이 아니라 경쟁하는 후보가 됨. run 밖 선택 스테이지 — **절대 blocker 아님, degrade해서라도 동작하거나 스킵.**

**INPUT** (코퍼스, 있는 것만 사용 — graceful degrade):
1. CTO/소장 발언록·전략 우선순위 (체계적 기록 있으면)
2. 없으면: 메모리(`r2p-org-context`, `samsung-pde-reality`) + `runs/round1-retrospective/` + 기존 run-log들
3. 그마저 얇으면: 인간이 준 "전략 우선순위" 1줄을 orchestrator가 3–4개 candidate framing으로 확장

**OUTPUT**: `runs/_sourcing/<YYYYMMDD>.md` — 후보 5–8개 + 3문 사전 채점 (원칙 1 traceability: run 밖 산출물도 폴더에 기록)
**AGENT**: `sonnet-analyst` 후보 생성 (1문단씩, 싸게) → `opus-architect` ×1 P3 페르소나 사전 채점

**절차**:
1. 코퍼스에서 전략적 긴장 후보 추출: 경쟁사 움직임 vs 삼성 보유 레이어(플릿/워치/실리콘/OS)의 비대칭 + 타이밍 창
2. 시드 후보 5–8개, 각 1문단 (기술/능력 층위 + 전략 가설 1문장)
3. 각 후보에 3문 테스트(`templates/00-seed-intake.md`) 사전 채점 — 후보당 짧게, P3 렌즈
4. 최고 1–2개만 full run (S0 정식 인테이크로 진입 — 시드 소스 `sourcing(S0.5)` 표기, 사전 채점 첨부)

**QUALITY BAR**: 후보 간 비대칭 자산이 겹치지 않게 (전부 "갤러리 탑재"면 소싱 실패). 3문 PASS/WEAK 후보가 0개면 코퍼스가 얇다는 신호 — 인간에게 전략 우선순위 질문 후 재시도.
**FAILURE MODES**: 코퍼스 부재 → 위 INPUT 2·3으로 degrade, 그래도 안 되면 스킵하고 manual 시드로 진행 (S0 게이트가 최후 방어선). 후보가 제품 아이디어로 새어나감 → 기술/능력 층위로 되돌림 (S0 규칙과 동일).
