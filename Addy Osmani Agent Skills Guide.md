| **Version or commit** | **Checked against repo on** | **Author** | **Reviewer** |
|----|----|----|----|
| 0.6.16 (addyosmani/agent-skills) | 18 November 2026 | Refocus AI methodology draft | Faheem (draft) |

# 1. What it is

Agent Skills is a pack of reusable engineering workflows for AI coding
agents. One sentence a new engineer can repeat: it tells the agent how a
senior engineer would work, phase by phase, instead of guessing. It
solves uneven agent quality—skipped specs, oversized diffs, weak
tests—by encoding DEFINE → PLAN → BUILD → VERIFY → REVIEW → SHIP as
skills plus slash commands (/spec, /plan, /build, /test, /review,
/ship). You install the skill files into the harness; the agent reads
the matching skill when the task fits. Skills guide behavior; they do
not hard-enforce it.

# 2. Who made it and when

- Author or organization: Addy Osmani,
  https://github.com/addyosmani/agent-skills

- License: MIT —
  https://github.com/addyosmani/agent-skills/blob/main/LICENSE

- First release: 0.5.0, 10 April 2026 (repo created 15 February 2026)

- Latest version: 0.6.16, 14 November 2026

- Release pace: 18 tagged releases from April to November 2026 (about
  every one to two weeks)

# 3. How to install it

npx skills add addyosmani/agent-skills \# pin/checkout tag 0.6.16 for
the install you keep. For Cursor at Refocus: sync that tag’s skills/
into .cursor/skills/ (see docs/cursor-setup.md). Pilot install example:
npx skills add addyosmani/agent-skills --skill using-agent-skills
--skill test-driven-development --skill code-review-and-quality

- Adds to the repo: .cursor/skills/\<name\>/SKILL.md (and optional
  .cursor/rules/\*.mdc pointer). Upstream also ships commands/, agents/,
  references/, docs/, hooks/

- Works with: Cursor Agent (our harness), Claude Code, Codex, Copilot,
  Gemini CLI, OpenCode, Antigravity, Windsurf, and 70+ agents via the
  open skills CLI

# 4. The flow

1.  DEFINE (clarify): /spec + using-agent-skills +
    spec-driven-development → SPEC.md the team can argue with before
    code

2.  PLAN: /plan + planning-and-task-breakdown → ordered tasks. BUILD:
    /build + incremental-implementation + test-driven-development → one
    thin, tested slice at a time

3.  VERIFY: /test + debugging-and-error-recovery → proof it works
    (failing test first). REVIEW: /review + code-review-and-quality →
    merge gate. SHIP (close): /ship + shipping-and-launch → go-live
    checklist. Map to the shared loop: clarify → spec and plan → build →
    verify → close. Load by phase; do not load all ~25 skills every
    session.

# 5. When to pick it

**Pick it when:**

- Multi-file behavior changes where a wrong assumption is expensive
  (money, status, enrollment, permissions).

- Hard bugs where writing the failing test first can catch a second
  break before merge.

- Brownfield work that needs verification-first adoption, not a big-bang
  dump of every skill.

**Skip it when:**

- One-line UI copy or tiny cosmetic tweaks — full lifecycle is overkill;
  a 3-skill pilot is enough.

- Any session where loading the whole pack would drown the signal — load
  by phase via using-agent-skills instead.

# 6. What to watch for

- Known limit / cost: skills are guides, not enforcement — the agent can
  still skip steps if you do not steer. Loading all ~25 skills every
  session burns context (adoption guide says not to).

- Runs only when called or routed: slash commands (/spec /plan /build
  /test /review /ship) or when using-agent-skills matches the task — not
  a silent always-on compiler.

- Author claim we did not test: we did not measure whether /build auto
  cut wall-clock time on Refocus portal work; treat autonomy speed
  claims as unmeasured here.

# What our team observed

*~40k (Cursor estimate / session usage; not native metering)*

| **Harness** | Cursor Agent |
|----|----|
| **Task types** | feature, bug fix, brownfield (multi-file); weak fit for one-line UI copy |
| **Runs** | 12 (pilot tasks on portal / Renewal Hub work) |
| **Setup time** | ~25 minutes (install + sync 3-skill pilot into .cursor/skills) |
| **Tokens per accepted change** | ~40k (Cursor estimate / session usage; not native metering) |
| **Manual interventions per task** | ~1–2 (steer skill choice or fix a skipped step) |
| **Test result** | pass on focused Jest suites for the changed paths; full suite not always re-run on one-liners |
| **What surprised us** | Overkill on one-liners (we cut to a 3-skill pilot); on harder bugs, failing-test-first caught a second break; skills guide, they do not enforce. |
| **What we would change** | Start verification-first on brownfield; do not load all 25 skills every session; reserve the full lifecycle for multi-file money/status logic. |
