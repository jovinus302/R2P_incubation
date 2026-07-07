# R2P Ideation Pipeline — Overview

기술 시드 → CTO-ready 아이디어 브리프 2–3개. 목표 소요: 오케스트레이션 세션 1회 (수 시간). 2주 케이던스 조직용 — 무거운 stage-gate 아님.

```
[S0.5 시드 소싱 (선택)] → S0 인테이크+3문 게이트 → S1 리서치 → S2 발산 → S3 페르소나 평가 → S4 브리프+레드팀/블루팀 → [CTO 리뷰 → 2주 MVP → go/no-go]
 sonnet + opus(P3)        orchestrator + opus(P3)   web-researcher   sonnet-analyst   opus-architect ×3      sonnet + opus            (다운스트림, 인간)
                                                    ×3 병렬          (opus 격상 가능)  (P1/P2/P3 병렬)
```

## 원칙

1. **1 run = 1 seed = 1 폴더.** 모든 산출물은 `runs/<YYYYMMDD>-<slug>/`에 커밋 — CTO 결정마다 추적 가능한 근거 트레일. run 밖 산출물(S0.5 소싱)은 `runs/_sourcing/`.
2. **stage 파일이 곧 프롬프트.** `process/stages/*.md`의 DELEGATION PROMPT를 그대로 서브에이전트에 전달. 프로세스 문서와 프롬프트의 이중화 없음.
3. **싸게 발산, 판단으로 수렴.** Sonnet이 넓게 (10–12개), Opus가 페르소나로 거른다 (2–3개). 테제·파급력 요구 시드는 발산도 opus 격상 가능 (사유를 run-log에 기록).
4. **제품 우선 가드레일.** 모든 템플릿이 "기술이 뭘 하나"보다 "누가 왜 쓰나"를 먼저 묻는다. 구조로 강제, 훈계로 하지 않음.
5. **휴먼 개입 분류.** 필수 게이트 2개: S0 BLOCKING(시드 3문 FAIL 포함) + 최종 CTO 리뷰(다운스트림). 선택적 피드백 주입: S1 사실 정정, `review_shortlist` 확인, S트랙 advance 확인. **루브릭·렌즈 개정은 run 사이에만** — run 중간 개정은 점수 비교 가능성을 깨는 안티패턴 (round 2 실증).
6. **시드가 천장.** 하류는 시드에 없던 파급력을 만들 수 없다 — S0 3문 게이트(전략적 긴장·삼성 비대칭·다음 문)가 이길 수 있는 판만 벌인다. 파이프라인 개선은 좋은 시드를 안 죽이는 장치, 시드 게이트는 판 자체를 고르는 장치.

## 단계 요약

| 단계 | 입력 | 출력 | 에이전트 | 체크포인트 |
|---|---|---|---|---|
| S0.5 소싱 (선택) | 전략 코퍼스 | `runs/_sourcing/<date>.md` (후보 5–8 + 사전채점) | sonnet-analyst + opus(P3) | — |
| S0 인테이크+게이트 | 자유 텍스트/URL | `00-seed.md` (3문 판정 포함) | orchestrator + opus(P3) ×1 | 3문 FAIL = BLOCKING (run 미착수), BLOCKING 질문 시 |
| S1 리서치 | seed | `10-research-digest.md` | web-researcher ×3 병렬 | — |
| S2 발산 | seed+digest+lenses+CTO급 정의 | `20-idea-candidates.md` (10–12 카드) | sonnet-analyst (opus 격상 가능) | — |
| S3 평가 | 후보+rubric v3+personas | `30-scoring.md` (트랙·moat 하한 포함) | opus-architect ×3 (P1/P2/P3) | `review_shortlist` 시 + S트랙 advance 시 필수 |
| S4 브리프 | 상위 2–3 + digest | `briefs/*.md`, `40-run-summary.md` | sonnet 초안 → opus 레드팀(×3 페르소나) → opus 블루팀 | 최종 (인간→CTO) |

상세: `process/stages/`. 사용자 제출 아이디어(예: PlaceLM)는 idea card 형식으로 변환해 S3에 합류 — 생성 아이디어와 동일 루브릭으로 평가.

## run 규칙

- run-id: `<YYYYMMDD>-<seed-slug>` (예: `20260706-frontier-ai`)
- 각 run에 `run-log.md`: 단계 타임스탬프, 사용 에이전트, 체크포인트 결정, 프로세스 이탈 기록
- run 종료 시 폴더 전체 git 커밋

## 실패 모드 대응

- 시드 3문 FAIL → run 미착수. 재프레이밍 또는 S0.5 역산 소싱으로 우회
- 리서치 LOW confidence 섹션 → run-log에 표기, 고위험 시드는 `deep-research` 스킬로 격상 (기본은 속도 우선이라 미사용)
- S3에서 advance 0개 → 시드 자체가 약함. 브리프 강행 금지, seed 재정의 또는 종료 보고
- 페르소나 점수 전부 동일 (특히 P3가 P1/P2와 동일) → 페르소나 프롬프트 실패 신호, 재실행
- 전 후보가 "빅테크 기존 기능 + 탑재 해자" 형태 → S2 렌즈 13/16/17 강조 재실행
