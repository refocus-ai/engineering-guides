| **Version or commit** | **Checked against repo on** | **Author** | **Reviewer** |
|----|----|----|----|
| v7.0.2 (obra/superpowers) — pin actual Track 1 tag if different | 18 November 2026 | Waleed (Track 1) | Faheem (draft) |

# 1. What it is

Superpowers is a discipline layer for AI coding agents
(obra/superpowers). One sentence a new engineer can repeat: it forces
plan → failing tests → code, instead of dumping diffs first. It solves
vibe-coding—skipped specs, weak tests, messy long chats—by gating work
behind Socratic design, Git worktrees, mandatory RED-GREEN TDD, fresh
subagents per micro-task, and a dual-pass review. You install it into
Cursor via plugin or .cursor/rules; the agent checks for skills before
tasks and resists coding until the gates pass.

# 2. Who made it and when

- Author or organization: Jesse Vincent / Prime Radiant (obra) —
  https://github.com/obra/superpowers

- License: MIT — https://github.com/obra/superpowers/blob/main/LICENSE

- First release: repo created 9 October 2025; early public methodology
  releases through 2026

- Latest version: v7.0.2, 3 November 2026 —
  https://github.com/obra/superpowers/releases/tag/v7.0.2

- Release pace: frequent through 2026 (for example multiple v6.x and
  v7.x tags from August–November 2026)

# 3. How to install it

/add-plugin superpowers\
\# Or vendor rules from obra/superpowers into the project .cursor/rules\
\# Pin/checkout tag v7.0.2 (or the tag you actually ran) and record it
in the table below.\
\# Verify: new Agent chat → prompt a feature → agent must start Socratic
Q&A, not dump code.

- Adds to the repo / harness: .cursor/rules (or plugin skills) from
  obra/superpowers — brainstorming, writing-plans, TDD, subagent-driven
  development, review, finish-branch helpers

- Works with: Cursor Agent (our harness), Claude Code, Codex, and other
  agents supported by the Superpowers plugin ecosystem

# 4. The flow

1.  Clarify: brainstorming / Socratic Q&A → approved design.md (boundary
    conditions, types, contracts)

2.  Spec and plan: writing-plans + worktree isolation → feature
    branch/worktree, baseline tests green, micro-tasks (2–5 min)

3.  Build: subagent-driven TDD → RED (failing test) → GREEN (smallest
    code) → REFACTOR. Verify: self-heal on compiler/test failures;
    dual-pass review (spec compliance, then quality/lint). Close: finish
    branch when gates pass. Map to shared loop: clarify → spec and plan
    → build → verify → close. Iron law: production code before a failing
    test is rejected.

# 5. When to pick it

**Pick it when:**

- Multi-file or core domain logic where silent edge-case bugs are
  expensive (auth, billing-adjacent, shared utilities).

- Hard algorithms / utilities that need strict test coverage (our LRU +
  TTL + concurrency bench class of problem).

- Work that would take \>~30 minutes of human effort and benefits from
  worktree isolation + fresh subagents.

**Skip it when:**

- One-line bugfixes, CSS/UI polish, or exploratory spikes — ceremony and
  token cost dominate.

- Tight token budget or “time to first diff” is the only success metric
  — our sample was ~6× slower and ~8× tokens.

# 6. What to watch for

- Known limit / cost: high wall-clock and token overhead (~2→12 min,
  ~15k→120k on our paired task). Overkill for tiny edits.

- Runs as an always-on discipline layer once installed (agent checks
  skills before tasks); not a one-shot slash menu like Agent Skills
  phases.

- Author claim we did not test: multi-hour fully unattended portal work
  without leaving the plan — self-heal held on the sample, long
  unattended Refocus runs not proven.

# What our team observed

*Figures below are from our Track 1 paired run (plain Cursor control vs
Superpowers) on a TypeScript in-memory LRU cache with TTL and
concurrency guards. Not a full portal PR merge. Tokens are
Cursor-session estimates. Write \[pending check\] on any figure Faheem
has not confirmed.*

| **Harness** | Cursor Agent |
|----|----|
| **Task types** | hard utility / multi-edge algorithm (LRU+TTL+concurrency); weak fit for one-line UI |
| **Runs** | 1 paired run (control vs Superpowers); expand with portal tickets |
| **Setup time** | ~2 minutes (/add-plugin superpowers or copy .cursor/rules; verify with Socratic Q&A) |
| **Tokens per accepted change** | ~120k (control: ~15k) — Cursor estimate; ~8× |
| **Manual interventions per task** | 0 (control: 6–8) |
| **Test result** | ~100% coverage gated by RED-GREEN TDD (control: ~60% retroactive; missed race/zero-TTL edges) |
| **What surprised us** | Took longer and used ~8× tokens, but no re-prompting for fixes — 0 manual patches vs 6–8 on the same task. |
| **What we would change** | Keep selective: Superpowers for multi-file/domain/high-test work; native Cursor for one-liners/CSS/spikes; pin version and re-measure on a real portal PR. |
