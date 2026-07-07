# Research Digest — 20260707-appliance-trust (S1)

web-researcher ×3 병합 (패스 A 기술 성숙도 / B why-now·시장 / C 경쟁·prior art). 랭킹 축: 신선도·경쟁 공백 병기 (데모 안정성 단일축 금지 — v3 규칙).

## 1. 핵심 판정: 통합 갭 실재  `confidence: HIGH`

구성 블록 3개는 전부 productized, **셋을 잇는 통합은 표준·제품·논문 어디에도 없음 (research gap)**:
- **Knox Matrix/Vault 가전 적용** (2025년형 Wi-Fi 가전 전체 + 7/9" 화면 가전에 Knox Vault CC EAL 4/5+, PQC 적용) — [Samsung Newsroom CES 2026](https://news.samsung.com/uk/ces-2026-a-look-at-samsung-appliances-built-in-security) `HIGH`
- **Matter DAC** (전 인증 기기 의무, PAA→PAI→DAC 체인) — 단 **커미셔닝(페어링) 시점 1회 신원 증명뿐, 실시간 센서 상태 스트림 서명은 표준에 없음** — [Matter Handbook](https://handbook.buildwithmatter.com/how-it-works/attestation/) `HIGH`
- **홈 상태의 LLM 노출** (Home Assistant 공식 MCP 서버 `context-snapshot`, SmartThings MCP) — 단 신뢰 기반은 OAuth/토큰(앱 계층)이지 실리콘 신뢰 루트와 **연결 안 됨** (상호 참조 부재 확인) — [HA MCP](https://www.home-assistant.io/integrations/mcp_server/) `HIGH`
- "이 온도 값은 attested silicon root에서 나옴" 필드를 노출하는 API 사례: NOT FOUND. 연속 attested telemetry의 Matter 로드맵: NOT FOUND.

## 2. 경쟁 지형 — 비대칭 재정의  `confidence: HIGH`

| 제품 | 회사 | 하는 일 | 트랙션 | 갭 |
|---|---|---|---|---|
| Gemini for Home | Google | 자연어 홈 제어, Home Brief, $10/월 구독 | 2026 Assistant 대체 | 상태 검증 계층 없음, 가전 제조 안 함 |
| Alexa+ | Amazon | 대화형 제어 | 일부 기기 미지원 | 생태계 분리, 검증 없음 |
| Apple 홈 허브 | Apple | AI 허브(7", 안면인식) | **반복 연기** (2025봄→2026.9) | Siri 완성도, 가전 제조 안 함 |
| Home Assistant + 로컬 LLM | OSS | Assist 파이프라인, MCP | 커뮤니티 표준 | OAuth 신뢰, 실리콘 루트 없음 |
| OpenClaw + smartthings 스킬 | OSS | 범용 에이전트 홈 제어 | GitHub 24.7만 스타 | **보안 붕괴 실증** (아래) |
| Josh.ai | 스타트업 | 프리미엄 음성 홈 | 10년 운영, JoshGPT | 니치, 신뢰 계층 아님 |

- **"삼성만 기기 인증" 원 주장은 반박됨**: Matter DAC 체인은 Apple/Google/Amazon/삼성 4개 생태계 공통 — [Google Home Developers](https://developers.home.google.com/matter/primer/attestation) `HIGH`
- **살아남은 비대칭 (좁혀진 형태)**: ① 삼성만 가전을 **제조** (구글은 안 만듦, Apple도 안 만듦), ② Knox Matrix/Vault를 가전까지 이미 확장한 유일 벤더, ③ DAC(1회 신원)를 실시간 상태 증명으로 확장한 주체는 **아직 0** — 선점 창 존재. 경쟁 3사 로드맵은 전부 자연어 UX·구독에 집중 `MED`(로드맵 해석)

## 3. Why-now 신호  `confidence: HIGH`

- **에이전트가 가전 안으로**: CES 2026 삼성 Bespoke AI 냉장고·전자레인지·와인셀러에 Gemini 직접 탑재, SmartThings를 가전 데이터 허브로 재설계 — [Samsung Newsroom](https://news.samsung.com/global/samsung-to-unveil-ai-vision-built-with-google-gemini-at-ces-2026) `HIGH`
- **에이전트 보안 붕괴 실증 (시드 가설 사실 검증됨)**:
  - ClawHavoc: 2026-02 Koi Security 감사 — 스킬 2,857개 중 **341개(11.9%) 악성** 확인, 후속 824개(2/16), Antiy 카탈로그 1,184개. ClickFix 2.0 수법, AMOS 스틸러 페이로드 — [CyberSecurityNews](https://cybersecuritynews.com/clawhavoc-poisoned-openclaws-clawhub/) `HIGH`
  - ClawJacked: CVE-2026-32025 (CVSS 8.8) — 임의 웹페이지 JS가 클릭 없이 게이트웨이 탈취 가능 — [Oasis Security](https://www.oasis.security/blog/openclaw-vulnerability) `HIGH`
  - ClawHub 마켓: 코드 리뷰·스캔·승인 절차 전무 `HIGH`
- **소비자 불신 데이터**: AI 완전 신뢰 13%, 무단 행동 우려 44%, "한 번 실수 후 중단" 60%(영국 AI 쇼핑) `MED`; 커넥티드 기기 데이터 우려 30%↑, 통제권 없음 47% `MED`
- **규제**: EU CRA — 2026-09-11부터 24시간 취약점 신고 의무 (IP캠·경보·도어락 명시 포함, 최대 €15M/매출 2.5%) — [Crowell](https://www.crowell.com/en/insights/client-alerts/eu-cyber-resilience-act-countdown-11-september-2026-incidentvulnerability-reporting-deadline-is-less-than-100-days-away) `HIGH`
- **LLM 홈 신뢰성 자체가 미해결**: HomeBench — 다중기기 무효 명령에서 GPT-4o 성공률 0%; entity hallucination 문서화 — [arXiv:2505.19628](https://arxiv.org/abs/2505.19628) `MED`

## 4. 인접 수요 신호 (보험·에너지)  `confidence: MED`

- Hippo "Clara" AI FNOL 에이전트 (2026-04, 신규 청구 70% 디지털 처리 목표) `MED`
- 검증된 누수 감지기 기반 "Leak-Protected" 보험료 **5–12% 할인** 관행 `MED` (업계 블로그 — 1차 공시 아님)
- VPP 급성장 (CA 1,145MW, TX 1GW) — 단 "기기 상태 위조 정산 사기" 사례: NOT FOUND `LOW`
- WTP(검증 레이어 지불 의사) 정량 데이터: NOT FOUND

## 5. Prior Art / 실패 사례  `confidence: HIGH`

- Revolv(클라우드 종속 벽돌화)·Wink(구독 강제+70회 아웃티지)·Iris(사업 철수)·Insteon(돌연 중단) — 공통 실패 원인은 **암호학적 신뢰 설계 결함이 아니라 클라우드 단일 장애점·사업 지속성·구독 반발** — 신뢰 계층 자체를 시도하다 죽은 사례 없음 (미개척 확인) `HIGH`
- 학계: Dual-Stage Intent-Aware(의도/물리 실행 분리, 2026), Collective Remote Attestation(IoT 일반) — 가정용+LLM 특화 없음 `MED`

## 6. Open Questions (S2/S3에 전달)

- 가전 등급 실리콘 RoT: 화면 탑재 프리미엄 가전(Family Hub류)은 Knox Vault 확인 `HIGH`, **비화면 일반 가전(세탁기·에어컨)의 실리콘 신뢰 루트는 미확인** — MVP 기기군 선정에 직결 `LOW`
- Knox Matrix "Trust Chain" 기술 백서 부재 — 온체인 기록 대상(실시간 상태 포함?) 미확인
- SmartThings 기기 health = ONLINE/OFFLINE 연결성뿐 (실리콘 증명 아님) — 통합 시 신설 필요
- OpenClaw "3만 대 노출 인스턴스" 원 출처 미특정 (341개 악성 스킬·CVE는 검증 완료)
