# R2P Ideation Pipeline — Overview

기술 시드 → CTO-ready 아이디어 브리프 2–3개. 목표 소요: 오케스트레이션 세션 1회 (수 시간). 2주 케이던스 조직용 — 무거운 stage-gate 아님.

```
S0 시드 인테이크 → S1 리서치 → S2 아이디어 발산 → S3 페르소나 평가 → S4 브리프+레드팀 → [CTO 리뷰 → 2주 MVP → go/no-go]
   orchestrator     web-researcher   sonnet-analyst    opus-architect ×2      sonnet + opus        (다운스트림, 인간)
                    ×3 병렬                            (P1/P2 병렬)
```

## 원칙

1. **1 run = 1 seed = 1 폴더.** 모든 산출물은 `runs/<YYYYMMDD>-<slug>/`에 커밋 — CTO 결정마다 추적 가능한 근거 트레일.
2. **stage 파일이 곧 프롬프트.** `process/stages/*.md`의 DELEGATION PROMPT를 그대로 서브에이전트에 전달. 프로세스 문서와 프롬프트의 이중화 없음.
3. **싸게 발산, 판단으로 수렴.** Sonnet이 넓게 (10–12개), Opus가 페르소나로 거른다 (2–3개).
4. **제품 우선 가드레일.** 모든 템플릿이 "기술이 뭘 하나"보다 "누가 왜 쓰나"를 먼저 묻는다. 구조로 강제, 훈계로 하지 않음.
5. **휴먼 체크포인트 최대 2개.** S0 BLOCKING 질문 (선택), 최종 CTO 리뷰 (필수·다운스트림).

## 단계 요약

| 단계 | 입력 | 출력 | 에이전트 | 체크포인트 |
|---|---|---|---|---|
| S0 인테이크 | 자유 텍스트/URL | `00-seed.md` | orchestrator | BLOCKING 질문 시 |
| S1 리서치 | seed | `10-research-digest.md` | web-researcher ×3 병렬 | — |
| S2 발산 | seed+digest+lenses | `20-idea-candidates.md` (10–12 카드) | sonnet-analyst | — |
| S3 평가 | 후보+rubric+personas | `30-scoring.md` | opus-architect ×2 (P1/P2) | `review_shortlist` 플래그 시 |
| S4 브리프 | 상위 2–3 + digest | `briefs/*.md`, `40-run-summary.md` | sonnet 초안 병렬 → opus 레드팀 | 최종 (인간→CTO) |

상세: `process/stages/`. 사용자 제출 아이디어(예: PlaceLM)는 idea card 형식으로 변환해 S3에 합류 — 생성 아이디어와 동일 루브릭으로 평가.

## run 규칙

- run-id: `<YYYYMMDD>-<seed-slug>` (예: `20260706-frontier-ai`)
- 각 run에 `run-log.md`: 단계 타임스탬프, 사용 에이전트, 체크포인트 결정, 프로세스 이탈 기록
- run 종료 시 폴더 전체 git 커밋

## 실패 모드 대응

- 리서치 LOW confidence 섹션 → run-log에 표기, 고위험 시드는 `deep-research` 스킬로 격상 (기본은 속도 우선이라 미사용)
- S3에서 advance 0개 → 시드 자체가 약함. 브리프 강행 금지, seed 재정의 또는 종료 보고
- P1/P2 점수 전부 동일 → 페르소나 프롬프트 실패 신호, 재실행
