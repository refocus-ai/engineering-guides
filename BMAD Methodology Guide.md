|  |  |  |
|----|----|----|
| **Version or commit** | **Checked against repo on** | **Author** |
| [<u>BMAD Method v6.12.4</u>](https://github.com/bmad-code-org/BMAD-METHOD/releases/tag/v6.12.4) (modules core + bmm) | 20 Nov 2026 | A. Moiz |

# 1. What it is

**BMAD is a set of agent skills that runs AI coding like a small agile
team and sizes the process to the change.** It targets the agent that
starts coding on a vague ask and forgets decisions between sessions.
Planning skills turn an idea into a brief, a PRD, an architecture and
stories with acceptance criteria, saved in the repo for later sessions
to build from. One Build skill then clarifies, writes a spec,
implements, runs its own multi-layer review and presents the result. A
small, clear change skips the planning and goes straight to a one-shot
Build. Five named persona agents front the skills: Analyst, PM, UX
Designer, Architect and Developer.

# 2. Who made it and when

- Author or organization: [<u>BMad Code,
  LLC</u>](https://github.com/bmad-code-org/BMAD-METHOD) (npm author:
  Brian “BMad”)

- License:
  [<u>MIT</u>](https://github.com/bmad-code-org/BMAD-METHOD/blob/v6.12.4/LICENSE)

- First release: [<u>v1.0.1 on npm, 15 June
  2025</u>](https://www.npmjs.com/package/bmad-method?activeTab=versions)
  (GitHub repo created 13 April 2025)

- Latest version: [<u>v6.12.4, 14 October
  2026</u>](https://github.com/bmad-code-org/BMAD-METHOD/releases/tag/v6.12.4);
  main and the docs site show the V7 preview

- Release pace: [<u>23 v6 releases in eight
  months</u>](https://github.com/bmad-code-org/BMAD-METHOD/releases)
  (v6.0.0, 17 Feb 2026, to v6.12.4, 14 Oct 2026)

# 3. How to install it

npx bmad-method@6.12.4 install, then choose modules core + bmm and
Claude Code. Our 2 Nov 2026 manifest records that choice; no terminal
log was kept. Install uv first: every skill renders through uv run.

- Adds to the repo: \_bmad/, .claude/skills/bmad-\* (29 skills, 5 of
  them persona agents), and \_bmad-output/ (artifacts)

- Works with: [<u>48 agent platforms in the v6.12.4
  installer</u>](https://github.com/bmad-code-org/BMAD-METHOD/blob/v6.12.4/tools/installer/ide/platform-codes.yaml);
  it recommends Claude Code, Codex, Cursor and GitHub Copilot

# 4. The flow

1.  **Clarify:** bmad-brainstorming, bmad-product-brief or bmad-prfaq
    (Analyst): a brief or PRFAQ.

2.  **Spec and plan:** bmad-prd (PM): PRD; bmad-ux: UX doc if there is a
    UI; bmad-architecture (Architect): decisions.

3.  **Spec and plan:** bmad-create-epics-and-stories: stories with
    acceptance criteria.

4.  **Spec and plan, gate:** bmad-sprint-planning: readiness PASS,
    CONCERNS or FAIL, then a sprint status file.

5.  **Build:** bmad-build (Developer): clarify, spec file, implement.
    Small, clear work takes a one-shot route.

6.  **Verify:** Build’s review runs blind-hunter, edge-case and
    verification-gap subagents and logs a verdict per finding;
    bmad-code-review is optional.

7.  **Close:** Build presents and commits locally; bmad-retrospective
    closes an epic.

# 5. When to pick it

**Pick it when:**

- Work needs a written plan, such as a new product or multi-epic
  feature, so many agent sessions stay consistent.

- You want decisions to outlive the chat: specs, review logs and
  deferred work stay in the repo under \_bmad-output/.

- A repo lacks story files or a readiness gate: on stagehand (27 Oct
  mapping) those were the only BMAD pieces we lacked.

**Skip it when:**

- The change is a typo, formatting or config tidy-up; Build’s own
  description says to skip it.

- You need a process that holds still, or cannot install uv and Python.

# 6. What to watch for

- **Cost and churn:** review subagents run at the session’s model on
  every change, so tokens exceed a plain prompt. Minor releases rename
  things: v6.3 folded Scrum Master and QA into Developer; v6.11 retired
  the Tech Writer.

- **When it runs:** when called. In Claude Code, Build can also fire on
  its own when you delegate a feature or bug fix; bmad-build-auto
  (unattended loop) runs by name only.

- **Not tested by us:** that larger work gets the depth it needs. We ran
  only the one-shot path, not the planning track, the unattended loop or
  the Test Architect (TEA) module.

# How our team tested it

|  |  |
|----|----|
| **Harness** | Claude Code |
| **Task types** | Feature: the LRU+TTL cache utility, the same task as the Superpowers lane |
