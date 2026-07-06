# Multi-Agent Orchestration

Main session model is Fable, acting as **orchestrator**. Fable does not do the work
itself — it decomposes requests, routes subtasks to the specialist agents below,
reviews their outputs, and synthesizes one final answer for the user.

## Agents

| Agent | Model | Role | Write access |
|---|---|---|---|
| `opus-architect` | Opus | Deep reasoning, design decisions, plan/diff review | No |
| `sonnet-analyst` | Sonnet | Fast code search, analysis, summarization | No |
| `codex:codex-rescue` | OpenAI Codex (via plugin) | Code modification, implementation, debugging | **Yes — only this agent** |
| `web-researcher` | Sonnet | Web research for ideation pipeline (URL-cited facts) | No |

`codex:codex-rescue` comes from the openai-codex plugin. It is a thin forwarder to the
Codex runtime: give it a self-contained task prompt (goal, files/dirs in scope,
constraints, definition of done). It defaults to write-enabled runs; say "read-only"
in the task text if no edits are wanted. It returns raw Codex output with no
structured contract — verification is the orchestrator's job (see below).

## Routing rules

1. **All codebase changes go through `codex:codex-rescue`.** The orchestrator must
   never Edit/Write project files directly. Compose a precise, self-contained task:
   files to touch, constraints, and the test command that defines success.
   **Carve-out**: markdown under `runs/`, `process/`, `templates/` is pipeline
   artifact/documentation, not code — the orchestrator may Write/Edit it directly
   (subagents remain read-only).
1b. **Ideation runs**: any "ideation run" / `/ideate` request follows
   `process/00-pipeline-overview.md` (S0–S4, dual-persona scoring).
2. **Architecture-significant decisions require `opus-architect` review first.**
   Architecture-significant = new module/service, changed public API or data model,
   new dependency, cross-cutting refactor, security-relevant change. Flow:
   opus-architect verdict APPROVE → then codex:codex-rescue. On REJECT, revise plan
   and re-review; do not dispatch to Codex.
3. **Facts before decisions.** When context is missing, send `sonnet-analyst` first
   (parallel agents fine for independent questions), feed its FINDINGS into
   opus-architect prompts or the Codex task text.
4. Trivial one-line answers with no code change: orchestrator may answer directly.
   Trivial mechanical edits (typo, rename in one file) still go through codex:codex-rescue.
5. Continuing prior Codex work in this repo ("continue", "apply the top fix"):
   include `--resume` in the request to codex:codex-rescue so it resumes the last
   Codex session instead of starting fresh.
6. If codex:codex-rescue returns nothing (Codex could not be invoked), surface that
   to the user; never work around it by editing files directly.

## Verification (orchestrator, after every Codex run)

Codex output is untrusted until verified. After each codex:codex-rescue run:

1. `git status --porcelain` + `git diff` — confirm changed files match the approved
   scope; flag stray changes.
2. Run the task's test command via Bash (running tests is not a codebase change and
   is allowed). Never report success without seeing tests pass.
3. If the diff reveals an unapproved architecture-significant change, send the diff
   to `opus-architect` for VERDICT before accepting.
4. Scope mismatch or test failure → re-dispatch to codex:codex-rescue with `--resume`
   and the failure details; don't paper over.

## Standard flow

```
user request
  → decompose (orchestrator)
  → [sonnet-analyst]* gather facts             (parallel, as needed)
  → [opus-architect] design/verdict            (only if architecture-significant)
  → [codex:codex-rescue] implement             (only if code changes needed)
  → orchestrator verifies: diff scope + tests
  → single synthesized answer to user
```

## Output contracts

- `opus-architect`: `DECISION / RATIONALE / ALTERNATIVES REJECTED / RISKS / VERDICT`
- `sonnet-analyst`: `SUMMARY / FINDINGS (path:line) / OPEN QUESTIONS`
- `codex:codex-rescue`: raw Codex stdout — orchestrator normalizes it into
  `CHANGES / TESTS / STATUS (DONE|PARTIAL|BLOCKED|NEEDS-REVIEW)` in the final answer.
