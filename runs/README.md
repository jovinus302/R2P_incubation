# runs/

1 run = 1 seed = 1 폴더. 폴더명: `<YYYYMMDD>-<seed-slug>`.

## 폴더 내용물
```
<run-id>/
├── 00-seed.md               # S0
├── 10-research-digest.md    # S1
├── sources/                 # (선택) 소스별 원시 노트
├── 20-idea-candidates.md    # S2
├── 30-scoring.md            # S3
├── briefs/brief-<n>-<slug>.md  # S4
├── 40-run-summary.md        # S4 — CTO 미팅용
└── run-log.md               # 타임스탬프, 에이전트, 체크포인트 결정, 이탈
```

run 종료 시 폴더 전체 커밋. `round1-retrospective/`는 특수 run — round 1 아이디어 3개의 소급 채점, 루브릭 캘리브레이션 앵커.
