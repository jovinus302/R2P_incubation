# R2P Incubation — Ideation Pipeline

R2P(Research to Product)는 기술과 제품을 잇는 incubation 조직 (삼성 출발). 벤치마크: Google Labs가 NotebookLM을 내는 속도. 사이클: **기술 시드 → 아이디어 브리프 → CTO 리뷰 → 2주 MVP 데모 → go/no-go.**

이 repo는 그 앞단 **ideation 자동화**의 프로세스 + 템플릿. LLM 에이전트 오케스트레이션으로 실행된다.

```
S0 시드 인테이크 → S1 리서치 → S2 발산(10–12) → S3 듀얼 페르소나 평가(top 2–3) → S4 브리프+레드팀
```

평가는 실제 조직의 두 상무 페르소나로: P1 expert programmer, P2 이상인 (UX designer). 정의: `process/reference/personas/`.

## 런 시작
```
/ideate <기술 시드 설명 또는 URL>
```
또는 채팅으로 요청. 오케스트레이터가 `process/00-pipeline-overview.md`를 따라 실행, 산출물은 `runs/<YYYYMMDD>-<slug>/`.

## 구조
- `process/` — 파이프라인 정의, 단계별 위임 프롬프트, 페르소나·렌즈·anti-pattern
- `templates/` — 산출물 계약 (핵심: `40-idea-brief.md`, `30-scoring-rubric.md`)
- `runs/` — 실행 기록 (근거 트레일, git 커밋)

## 이력
- Round 1 (완료): C-DOT, Pages, Wellness Coach 데모. 소장 평가 — "모두 data 필요" → 루브릭에 데이터 의존성 체크 반영
- Round 2 (진행): frontier AI 파워 활용 제품 방향
