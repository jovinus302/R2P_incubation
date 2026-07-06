# Research Digest: Frontier AI 파워로 가능해진 제품 (2026-07-06)

> 3병렬 web-researcher 패스 병합. 모든 주장 URL 인용. 제품 아이디어 없음.

## 1. 기술 State of the Art  `confidence: HIGH`

능력별 성숙도 + **2주 MVP 라이브 데모 안정성**:

| 능력 | 성숙도 | 라이브 데모 | 근거 |
|---|---|---|---|
| 컴퓨터/브라우저 조작 | productizable | **최안전** | Opus 4.8 OSWorld 83.5% (인간 근접), ChatGPT Atlas('25-10), Claude Cowork('26-03) — https://llm-stats.com/benchmarks/osworld, https://openai.com/index/introducing-chatgpt-atlas/ |
| 실시간 멀티모달 (음성+화면+영상) | productizable | **안전** | Gemini Live API GA, 화면 보며 대화 — https://ai.google.dev/gemini-api/docs/live-api |
| 영상 생성 | productizable | 중 | Veo 3.1 대사·립싱크 동시 생성 — https://deepmind.google/models/veo/ |
| 초장문 컨텍스트 (1M GA) | productizable, 유효 길이 주의 | 중 | '26-03 1M 프리미엄 요금 폐지 — 단 "context rot": 실효 ~130K부터 불안정 — https://research.trychroma.com/context-rot |
| 장시간 자율 에이전트 | 성장 중, 신뢰도 리스크 | 위험 | METR: 50% 신뢰 Opus 4.5 ~5.3h, 배가 주기 3–4개월로 가속 — https://metr.org/blog/2026-1-29-time-horizon-1-1/ |
| 음악 생성 | productizable, 라이선스 제약 | 중 | Warner×Suno 계약('25-11) 후 다운로드·상업 사용 제한 — https://www.prnewswire.com/news-releases/warner-music-group-and-suno-forge-groundbreaking-partnership-302626017.html |
| 인터랙티브 월드 생성 | prototype | 위험 | Genie 3 60초 제한 — https://deepmind.google/models/genie/ |

최근 12–18개월 신규: 데스크톱 전체 제어, 화면 실시간 공유 대화, 1M 컨텍스트 표준화, 영상+오디오 동시 생성.

## 2. Why-Now 신호  `confidence: HIGH`

- 추론 비용: GPT-4급 $20 → $0.40/1M토큰 ('22말→'26초) — https://epoch.ai/data-insights/llm-inference-price-trends
- 에이전트 시간 지평 지수 성장, 배가 3–4개월 — https://metr.org/time-horizons/
- 온디바이스 전환: '26Q1 출하 스마트폰 54% GenAI-capable ('23년 11%), 연말 70% 전망 `MED`
- **삼성 자산 직결**: Personal Data Engine(PDE) — 기기 내 메시지·캘린더·알림·앱 활동을 AI용 구조화 맥락으로 변환. Now Brief/Now Nudge 출시 — https://news.samsung.com/us/samsung-advances-galaxy-ai-connected-ecosystem-mwc-2026 `MED`
- ⚠️ **사내 실측 교정 (내부 정보, HIGH)**: PDE는 사내 구현 중이나 평가 좋지 않음 — 개인 데이터 특성상 graphDB 구축이 어렵고 실사용 데이터 축적이 어려움. **"PDE 레버리지" 전제의 아이디어는 이 제약을 반영해 평가할 것** — 공개 발표 대비 실제 가용성 낮음. PDE 의존 = 사실상 또 하나의 데이터 의존성.
- Apple Siri AI ('26-06 WWDC): 개인 맥락 + 온스크린 어웨어니스 — 3사 모두 "개인 맥락 × AI"가 '26 핵심 전략 — https://www.apple.com/newsroom/2026/06/apple-introduces-siri-ai-a-profoundly-more-capable-and-personal-assistant/

## 3. 시장·유저 지형  `confidence: HIGH`

- 지불: ChatGPT Go $8/월 전 세계 ('26-01), Plus $20/Pro $200 병행 — https://openai.com/index/introducing-chatgpt-go/ ; OpenAI ARR $25B, 유료 ~5천만 명 `MED`
- AI 앱 IAP '26 상반기 $4B (+36% YoY) — https://sensortower.com/blog/state-of-ai-2026
- 컴패니언 앱 지불의향 상승 (다운로드당 매출 $0.52→$1.18) `MED`
- **위임 신뢰 갭**: 저위험 위임 의향 74%, 그러나 자율 구매 실행 허용 9–12% — https://www.accenture.com/us-en/insights/consulting/talk-my-ai-agent ; OpenAI Instant Checkout 초기 실패 후 전략 선회 — https://www.cnbc.com/2026/03/24/openai-revamps-shopping-experience-in-chatgpt-after-instant-checkout.html
- 시사점(사실): "제안·감독 장치 있는 에이전트"는 수용, "완전 자율 실행"은 시기상조

## 4. 경쟁·인접 제품  `confidence: HIGH`

| 제품 | 회사 | 하는 일 | 트랙션 | 갭 |
|---|---|---|---|---|
| NotebookLM (Video Overviews 등) | Google Labs | 소스 기반 리서치·영상 생성 | AI Ultra 확장 | 실시간 개인 상황 반영 없음 |
| Ask Maps | Google | 저장 장소·이력 반영 대화형 지도 | '26-03 미/인도 | **신규 추천형 — 검증 장소의 동선 복원 아님** |
| ChatGPT Atlas / Comet | OpenAI / Perplexity | 에이전틱 브라우저 | Comet 무료화, $200M 조달 | 개인 라이프스타일 특화 없음 |
| Manus | Butterfly Effect→Meta | 자율 에이전트 | ARR $100M+/8개월, Meta 인수 $2–3B | 범용 태스크 |
| Meta Ray-Ban Display | Meta | AI 안경+EMG 밴드 | $799 '25-09 출시 | 장소 맥락은 내비 수준 |
| Wanderlog/Mindtrip/Plotline | 스타트업 | AI 여행 플래너/장소 수집 | Mindtrip $20M+ | 전부 신규 추천 또는 회고형 |

**PlaceLM 관련 (S3 평가용)**: "저장·검증된 개인 장소 + 실시간 상황을 실행 동선으로 재구성"하는 제품 미확인 — 직접 경쟁 부재 `MED` (부재 증명 한계, 네이버/카카오 미조사).

## 5. Prior Art / 실패 사례  `confidence: HIGH`

- **AI Pin** ('25-02 사망, HP $116M): 기능 미작동 + 폰 대비 부가가치 부재 — https://techcrunch.com/2025/02/18/humanes-ai-pin-is-dead-as-hp-buys-startups-assets-for-116m/
- **Rabbit R1**: 데모 기능 대부분 미작동, 대량 반품 — "폰이 이미 하는 일" 함정
- **Sora 앱** ('26-04 종료): frontier 생성 능력 ≠ 지속 가능한 소비자 제품 — https://www.forbes.com/sites/johnsviokla/2026/04/02/when-ai-vendors-fail-lessons-from-the-sora-shutdown/
- **Limitless** (Meta 인수 후 종료): 개인 맥락 축적형 서드파티 하드웨어의 독자 생존 난이도 + 데이터 삭제 신뢰 붕괴
- 공통 사인: 폰 대비 부가가치 부재, 연출 데모와 실제 갭, 상시 수집 프라이버시 반발

## 5b. OpenClaw (추가 조사, 2026-07-07)  `confidence: HIGH`

- 정체: Peter Steinberger의 MIT 오픈소스 개인 에이전트 프레임워크 ('25-11 Clawdbot → '26-01 OpenClaw). 로컬 우선 Gateway 제어 평면 + 스킬 마켓(ClawHub). 기본 인터페이스는 24개+ 메신저 — https://github.com/openclaw/openclaw
- 트랙션: GitHub 38만 스타 (역대 최속 성장 에이전트 프레임워크)
- **비메신저 선례**: SwitchBot AI Hub ($259.99, OpenClaw 네이티브 탑재 첫 하드웨어, '26-02) — https://www.prnewswire.com/news-releases/switchbot-launches-ai-hub-the-worlds-first-local-home-ai-agent-supporting-openclaw-302682438.html ; Home Assistant MCP 통합; 서드파티 음성/Wear OS 앱 (비공식) `MED`
- **보안 리스크 (임베드 시 치명적 고려사항)**: 노출 인스턴스 3만+, ClawHavoc (악성 스킬 341개, 멀웨어 유포) — https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html ; ClawJacked (웹사이트만으로 에이전트 장악); 구조적 프롬프트 인젝션 취약 — arXiv:2603.27517
- 시사점(사실): 임베드 자체는 검증된 경로(SwitchBot), 단 보안 격리·스킬 큐레이션이 상용화 전제조건

## 6. Open Questions
- METR 세부 수치 그래프 기반 — 원자료 재검증 필요 `MED`
- 삼성 PDE 8억 대 적용 1차 소스 미확인 `LOW`
- 네이버지도/카카오맵 AI 저장장소 기능 미조사 (PlaceLM 국내 경쟁 확인 필요)
- 한국 소비자 에이전트 위임 신뢰 데이터 없음
