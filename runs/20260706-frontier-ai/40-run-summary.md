# Run Summary: Frontier AI 파워로 가능해진 제품 — CTO 리뷰용 1페이지

run: 20260706-frontier-ai · 시드: 소장 round 1 리뷰 방향 지시 · 2026-07-07 확정

## 시드 요약
Round 1(C-DOT·Pages·Wellness Coach)의 공통 사인은 wedge 없는 데이터 의존. Round 2는 frontier 능력(컴퓨터 조작·실시간 멀티모달·장문맥·자율 에이전트)이 필수 전제인 제품을 발산 — 총 21개 후보(유틸 트랙 12 + 테제 트랙 8 + 사용자 제출 PlaceLM), 듀얼 상무 페르소나(P1 expert programmer / P2 이상인 UX) 독립 채점 2라운드.

## 브리프 비교

| 브리프 | 원라인 피치 | 점수 (P1/P2/평균) | MVP 비용 | cold-start | 최대 리스크 | 레드팀 | 요청 결정 |
|---|---|---|---|---|---|---|---|
| **① 삶의 증거 검색** | 사진 5만 장은 심문 안 한 삶의 증언 — 기억은 검색되어야 한다 | 3.75/3.85/**3.80** | 2명×2주 | YES (선존재 갤러리 일회성 인덱싱) | 집계형 confabulation → 데모에서 stretch 분리 | 조건부 승인 (수정 반영 완료) | **2주 MVP 승인** |
| **② 곁눈** | 결제·계약 화면은 이제 혼자 보면 안 된다 | 3.55/3.50/**3.53** | 2명×2주 | YES (화면 공유가 곧 입력) | 오탐 신뢰 붕괴 → 정상 화면 10개 오경보 측정 내장 | 조건부 승인 (수정 반영 완료) | **2주 MVP 승인** |
| **③ 플레이스 트레일** | 추천은 죽었다 — 검증한 것의 복원이 맞다 (PlaceLM 부활판) | 3.10/3.30/**3.20** | 2명×2주 | PARTIAL (Takeout+EXIF 일회성 임포트) | 맥락 confabulation + frontier 필요성 입증 필요 | **REJECT→전환 조건 반영** | **재리뷰 상신** (승인 요청 아님) |

## 추천 및 근거
**①·② 승인 권고, ③은 조건 충족 검증 후 재리뷰.** ①은 양 페르소나 최고점 — 삼성 갤러리 자산 직결 + 데모 가장 안전 + 범용 공감. ②는 데모 최안전 + "판정 능력"까지만 승인 요청하는 정직한 훅. ③은 사용자 제출 아이디어의 부활판 — round A에서 kill된 사유(검증 데이터 미유입)를 Takeout wedge로 해소했으나, 레드팀이 "정직한 버전은 frontier 불필요 가능성"을 지적 — frontier 3지점 입증을 kill 기준으로 내장.

**페르소나 갈림 (참고 신호)**: T8 진위 가디언(딥페이크 실시간 판정) — P2 3.50 vs P1 2.95. 테제·공감 최상급이나 탐지 능력 미성숙. 온디바이스 실시간 탐지 성숙 시 재도전 1순위. OpenClaw 격리 임베드(차량·TV)는 인프라 3전제(Tizen 컨테이너·latency·capability-gating) 확인 후 "케이지드 버틀러" 형태로 재설계 후보 (35-openclaw-graft-assessment.md).

## 요청 결정
- 브리프 ①: [2주 MVP 승인 | 보류 | kill]
- 브리프 ②: [2주 MVP 승인 | 보류 | kill]
- 브리프 ③: [재리뷰 조건 충족 검증 착수 | 보류 | kill]

## 링크
- 브리프: `briefs/brief-t6-gallery-interrogator.md`, `briefs/brief-t2-gyeotnun.md`, `briefs/brief-t1-place-trail.md`
- 근거 트레일: `10-research-digest.md` → `20-idea-candidates(-thesis).md` → `30-scoring(-thesis).md` → `35-openclaw-graft-assessment.md`
- 유틸 트랙(round A) 브리프 3장: `briefs/track-a/` 보관 — 테제 트랙이 merit로 능가해 교체됨
