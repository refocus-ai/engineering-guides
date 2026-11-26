|  |  |  |  |
|----|----|----|----|
| **Version or commit** | **Checked against repo on** | **Author** | **Reviewer** |
| v1.3.2 (d1478fc) | 23 November 2026 | Syed Ghassan Gillani | Nadir Ali |

# 1. What it is

**A set of small skills you call one at a time, so the agent moves from
a vague request to reviewed code in clear steps.**

Left alone, a coding agent jumps straight to code, and every engineer
prompts it differently. Pocock’s skills split the work into separate
stages: questioning, spec, tickets, implementation and review. Each
stage is a plain-file skill with its own instructions, and the output of
one becomes the input to the next. The developer decides when each skill
runs. Unlike Superpowers, nothing orchestrates the whole chain on its
own.

# 2. Who made it and when

- Author or organization: Matt Pocock (AI Hero).
  [<u>Repo</u>](https://github.com/mattpocock/skills)

- License: MIT. [<u>Repo</u>](https://github.com/mattpocock/skills)

- First release: v1.0, 18 June 2026.
  [<u>Releases</u>](https://github.com/mattpocock/skills/releases)

- Latest version: v1.3.2 (commit d1478fc), 29 October 2026.
  [<u>Releases</u>](https://github.com/mattpocock/skills/releases)

- Release pace: four minor releases in under four months (v1.0 on 18
  June, v1.1 on 8 July, v1.2 on 5 August, v1.3 on 5 October 2026), plus
  frequent patches. [<u>v1.3
  changelog</u>](https://www.aihero.dev/skills-changelog-v13-implement-spec-pr-retro-and-glossary-md)

# 3. How to install it

Setup took about two minutes. Install with the skills CLI, or as a
Claude Code plugin:

> npx skills@latest add mattpocock/skills \# Cursor and other agents
>
> claude plugins install mattpocock-skills \# Claude Code plugin

We tested v1.3.2 (commit d1478fc). Update a CLI install with npx skills
update; plugin installs update on their own.

- Adds to the repo: one folder per skill, each with a SKILL.md (for
  example under .agents/skills/). Some skills also write a GLOSSARY.md
  domain file, which replaced CONTEXT.md in v1.3.

- Works with: Cursor Agent (our tested harness), Claude Code and Codex.
  Each skill ships metadata for both Claude Code and Codex.

# 4. The flow

The developer moves the agent through the chain by calling each skill in
turn.

1.  **Clarify:** grill-with-docs, asks structured questions, checks the
    docs and surfaces assumptions.

2.  **Spec and plan:** to-spec, turns the clarified requirements into a
    written spec.

3.  **Spec and plan:** to-tickets, breaks the spec into small,
    actionable tickets.

4.  **Build:** implement, builds one ticket at a time against the spec
    and the repo’s conventions. implement-spec is the alternative that
    builds a whole spec.

5.  **Verify:** code-review, reviews the change for correctness, quality
    and defects.

6.  **Close:** retro, records lessons and improves the agent’s
    environment for the next task.

# 5. When to pick it

**Pick it when:**

- Token budget matters. In our runs it used about 35k tokens per change,
  against about 120k for Superpowers and 281k for BMAD.

- Requirements are unclear and need structured questioning before anyone
  writes code.

- Larger changes need a reusable spec, a ticket breakdown and a
  consistent review.

- Developers want to decide when each phase runs, not hand the whole
  loop to automation.

**Skip it when:**

- You need a workflow that enforces every phase on its own. Superpowers
  or BMAD fit better.

- The team will not call the skills consistently or keep the spec and
  tickets current.

- Large tasks need fresh-context subagents without manual coordination.

# 6. What to watch for

- Cost: about 35k tokens per accepted change, more than double the plain
  Cursor Agent control at about 15k.

- Runs only when called. The skills are opt-in, so the result depends on
  the developer calling the right skill in the right order. Skipping a
  phase weakens the result, and it still took 4 to 5 interventions per
  task.

- Context lives in files. The spec, tickets and GLOSSARY.md keep
  decisions outside the chat, and a handoff skill passes context between
  agents.

- The author’s claim, stated plainly: the v1.0 release notes claim 63%
  fewer tokens, with no method given. We saw about 71% fewer tokens than
  Superpowers, but more than the plain control, so the saving depends on
  the baseline.

- Not tested: long, unattended runs without a developer driving the
  chain.

# What our team observed

Figures come from the ReFocus AI five-methodology field test. Token
values are Cursor session estimates.

|  |  |
|----|----|
| **Harness** | Cursor Agent |
| **Task types** | New feature, bug fix, refactor, brownfield |
| **Runs** | 15 |
| **Setup time** | ~2 min |
| **Tokens per accepted change** | ~35k (control: ~15k; Superpowers: ~120k) |
| **Manual interventions per task** | 4–5 (control: 6–8) |
| **Test result** | ~80–90% coverage (control: ~60%) |
| **What surprised us** | Even with manual orchestration, it used about 71% fewer tokens than Superpowers and kept a structured process. |
| **What we would change** | Make skill calls more consistent, and automate the handoff from spec to tickets to build to review where we can. |
