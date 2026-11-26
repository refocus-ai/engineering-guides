| **Version or commit** | **Checked against repo on** | **Author** | **Reviewer** |
|----|----|----|----|
| 1.19.0 (latest: 1.21.0) | 2026-11-18 | Mustansar Iqbal | \[pending\] |

# 1. What it is

GSD Core keeps a project's plan and state in Markdown files on disk, not
in a long chat. It targets context rot: output quality drops as a chat
fills with retries, logs and stale decisions. Each phase runs a
five-step loop (discuss, plan, execute, verify, ship). Research,
planning and coding run in fresh-context subagents that read only the
plan files, so the main session stays small and a new session can resume
from the state files.

# 2. Who made it and when

- Author or organization: OpenGSD, github.com/open-gsd/gsd-core
  (https://github.com/open-gsd/gsd-core)

- License: MIT (https://www.npmjs.com/package/@opengsd/gsd-core)

- First release: 2026-05-30, version 1.2.0-rc.1 (npm registry)

- Latest version: 1.21.0, 2026-11-13 (npm registry)

- Release pace: 47 published versions (including release candidates) in
  about 5.5 months, roughly one release a week lately

# 3. How to install it

npx @opengsd/gsd-core@1.19.0 --cursor --local

- Adds to the repo: runtime command and agent files for the chosen tool,
  plus a .planning/ folder (CONTEXT, PLAN, STATE, SUMMARY, VERIFICATION)
  once a project or phase starts. Exact installed folders: \[pending
  check\]

- Works with: Claude Code, OpenCode, Antigravity CLI, Kimi CLI, Kilo,
  Codex, Copilot, Cursor, Windsurf (per the README). Use the installer;
  do not copy files by hand.

# 4. The flow

1.  Clarify: /gsd-discuss-phase, locks implementation decisions into
    CONTEXT.md

2.  Spec and plan: plan step \[command pending check\], research and
    breakdown into PLAN.md

3.  Build: execute step \[command pending check\], fresh-context
    executors run the plan and write the code and tests

4.  Verify: verify step \[command pending check\], checks what was built
    and writes VERIFICATION.md

5.  Close: ship step \[command pending check\], opens the PR, archives
    the phase, moves to the next phase

# 5. When to pick it

**Pick it when:**

- Work spans many sessions and the agent must resume without being
  re-briefed.

- The task is big enough to split into phases with written decisions.

- You want a written record of what was decided, built and verified.

**Skip it when:**

- The change is a quick one-off fix.

- You will not maintain the state files; stale state misleads the agent.

# 6. What to watch for

- State files need upkeep and can go stale. Tests and review still
  decide quality. Token cost is unmeasured in our setup.

- Only when called: it runs through its commands, not on its own.

- Not tested: the claim that fresh-context subagents prevent context rot
  on long work. Our run was one small task, so long-chat rot was not
  induced.

# What our team observed

| **Harness** | Cursor Agent |
|----|----|
| **Task types** | feature (new TypeScript utility with tests) |
| **Runs** | 1 \[pending check\] |
| **Setup time** | about 2 seconds (install) \[pending check\] |
| **Tokens per accepted change** | not available, Cursor does not meter tokens (control: \[pending check\]) |
| **Manual interventions per task** | 0 (control: \[pending check\]) |
| **Test result** | 21/21 tests passed, tsc clean \[pending check\] |
| **What surprised us** | The whole loop finished in about 2.5 minutes on a small task with no corrections. |
| **What we would change** | Run it on a longer, multi-session task to test the context-rot claim. |
