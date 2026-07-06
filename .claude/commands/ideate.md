---
description: Run the full ideation pipeline on a tech seed (S0–S4 → CTO-ready briefs)
---

Run the R2P ideation pipeline end-to-end on this seed: $ARGUMENTS

Follow `process/00-pipeline-overview.md` exactly:

1. **S0**: Create `runs/<YYYYMMDD>-<slug>/`, fill `templates/00-seed-intake.md` → `00-seed.md`. Ask the user only if a [BLOCKING] open question exists. Start `run-log.md`.
2. **S1**: Dispatch 3 parallel `web-researcher` agents using the delegation prompts in `process/stages/10-research.md` (passes A/B/C). Merge into `10-research-digest.md` with confidence tags.
3. **S2**: Dispatch `sonnet-analyst` with the prompt in `process/stages/20-idea-generation.md` + the digest + `process/reference/generation-lenses.md` → `20-idea-candidates.md` (10–12 cards).
4. **S3**: Dispatch 2 parallel `opus-architect` agents, one per persona file in `process/reference/personas/`, using the prompt in `process/stages/30-filter-and-score.md`. Include any user-submitted idea cards from the seed. Build the consensus score table → `30-scoring.md`. Honor `review_shortlist` flag.
5. **S4**: Dispatch parallel `sonnet-analyst` drafts (one per shortlisted idea) per `process/stages/40-brief-writing.md`, then one `opus-architect` red-team pass with both personas. Apply required edits → `briefs/`, write `40-run-summary.md` from `templates/41-run-summary.md`, complete `run-log.md`.
6. Commit the run folder. Present the run summary to the user.

Rules: pipeline artifacts under `runs/` are written directly by you (carve-out in CLAUDE.md). Kill rules and quality bars in each stage file are binding — never advance weak ideas to fill quota.
