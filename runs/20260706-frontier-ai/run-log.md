# run-log — 20260706-frontier-ai

## 타임라인
- 07-06 S0: 시드 작성 (소장 방향 + PlaceLM 사용자 제출 카드). BLOCKING 질문 없음.
- 07-06 S1: web-researcher ×3 병렬 (기술성숙도/why-now·시장/경쟁) → 다이제스트 병합. LOW confidence: 삼성 PDE 8억대 적용, 일부 METR 수치.
- 07-06 **사내 교정**: PDE 내부 평가 나쁨 (graphDB·데이터 축적 난) — 다이제스트 §2 반영. S2(round A)는 교정 전 다이제스트 사용 → S3에서 교정 적용.
- 07-06 S2 (round A): sonnet-analyst, 12 카드. S3: P1/P2 병렬 → advance 장보기(3.30)/라이더(3.23)/동선(3.08), PlaceLM kill (위장 PARTIAL).
- 07-07 **프로세스 중간 개정 (사용자 피드백)**: ① 산출물이 "대학생 수준 유틸" — 테제 부재 진단 ② 루브릭 v2 (공감20/retention15/frontier20/테제15/데모15/자산10/시장5) ③ cold-start 캡 완화 — wedge 설계 있으면 캡 없음 (CTO 주안점 = AI 파워) ④ 범용 우선, 안 되면 뾰족한 역할군 ⑤ anti-patterns에 파급력 기준.
- 07-07 OpenClaw 추가 리서치 + opus-architect 접목처 판단 (35-) — 케이지드 버틀러 코어 판정, 착수 전제 3건 미확인.
- 07-07 S2-T (테제 트랙): **Opus** 발산, T1–T8. S3-T: P1/P2 재채점 → T6(3.80)/T2(3.53) ADVANCE, T1(3.20) 경합.
- 07-07 라인업 확정 (사용자): T6·T2·T1. Round A 브리프 3장 track-a/ 보관.
- 07-07 S4: sonnet 초안 ×3 병렬 → opus 레드팀: T6/T2 APPROVE-WITH-CHANGES (수정 반영 완료), T1 REJECT → 전환 조건 3건 반영 + 요청 결정 "재리뷰 상신"으로 하향.
- 07-07 run-summary 확정, 커밋.

## 사용 에이전트
web-researcher ×5 (S1 3병렬 + OpenClaw + insane-search 검증), sonnet-analyst ×7 (S2 발산 + 브리프 초안 6장), opus-architect ×6 (S3 2라운드 ×2페르소나 + 접목처 판단 + 레드팀), general-purpose(Opus) ×1 (S2-T 테제 발산).

## 프로세스 이탈/개선 기록
- 루브릭 v1→v2 run 중간 개정 — round A와 T트랙 점수 액면 비교 불가, merit 비교로 처리 (30-scoring-thesis.md 명시)
- S2가 루브릭에 과최적화되는 문제 발견 → 테제 우선 발산(렌즈 13–15) 신설
- G2 "설득력" 정의 명문화 (retrospective에서 P1/P2 게이트 갈림 원인)
- 발산 에이전트 모델: 파급력 요구 시 sonnet → opus 격상이 유효 (round A vs T트랙 품질 차)
