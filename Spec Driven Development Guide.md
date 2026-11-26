|  |  |  |  |
|----|----|----|----|
| **Version or commit** | **Checked against repo on** | **Author** | **Reviewer** |
| specify-cli 1.4.3 | 23 November 2026 | Faheem Arshad | Waleed Amjad |

# 1. What it is

**Write down what the software should do before any code is written, and
treat that spec as the team’s contract for “done.”**

Coding agents write code fast, but they guess at intent, skip edge cases
and drift from the plan. Vague requirements then turn into rework after
release. Spec-driven development (SDD) fixes this by turning an idea
into a short spec with testable acceptance criteria, reviewing it, and
deriving the plan and tasks from it. The agent builds against those
tasks, and every task, pull request and test traces back to a criterion.
When behavior changes, the spec changes first. We run it with GitHub
Spec Kit, which turns each phase into an agent command that writes a
versioned file into the repo.

# 2. Who made it and when

- Author or organization: GitHub. Den Delimarsky and John Lam conceived
  it; community-stewarded since January 2026.
  [<u>Repo</u>](https://github.com/github/spec-kit) · [<u>Project
  history</u>](https://github.github.com/spec-kit/history.html)

- License: MIT. [<u>PyPI
  listing</u>](https://pypi.org/project/specify-cli/)

- First release: initial commit 21 August 2025, public launch 2
  September 2025, version 1.0.0 on 21 August 2026.
  [<u>History</u>](https://github.github.com/spec-kit/history.html) ·
  [<u>Launch
  post</u>](https://github.blog/ai-and-ml/github-copilot/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)

- Latest version: specify-cli 1.4.3, 19 November 2026.
  [<u>PyPI</u>](https://pypi.org/project/specify-cli/)

- Release pace: 18 releases in six weeks (1.1.1 on 6 October to 1.4.3 on
  19 November 2026). [<u>Release
  history</u>](https://pypi.org/project/specify-cli/#history)

# 3. How to install it

Needs Python 3.11+ and uv. Install the CLI once, pinned, then initialize
the repo for Cursor:

> uv tool install specify-cli==1.4.3
>
> specify init --here --integration cursor-agent \# existing repo
>
> specify init my-project --integration cursor-agent \# new project

- Adds to the repo: .specify/ (memory/constitution.md, templates, helper
  scripts), .cursor/skills/ (the speckit commands),
  .cursor/rules/specify-rules.mdc, and one specs/NNN-feature/ folder per
  feature holding spec.md, plan.md and tasks.md.

- Works with: Cursor as a first-class integration, plus Claude Code,
  Codex CLI, Gemini CLI, GitHub Copilot, Cline and many more agents.

# 4. The flow

Run each command in the agent chat, one at a time, and review the result
before moving on. The constitution step runs once per project; the rest
repeats per feature.

1.  **Set principles (once):** /speckit.constitution, writes
    .specify/memory/constitution.md: quality, testing and UX rules every
    run must follow.

2.  **Specify (spec and plan):** /speckit.specify, writes spec.md on a
    new feature branch: the what and why, user stories and acceptance
    criteria.

3.  **Clarify (clarify):** /speckit.clarify, the agent asks questions
    about gaps and records the answers in spec.md.

4.  **Plan (spec and plan):** /speckit.plan, writes plan.md with tech
    choices, data model and contracts. Review it here; it is the
    cheapest place to change course.

5.  **Tasks (spec and plan):** /speckit.tasks, writes tasks.md: ordered,
    small tasks, each tied to a spec section.

6.  **Implement (build):** /speckit.implement, writes the code and
    tests, task by task.

7.  **Converge (verify):** /speckit.converge, checks the build against
    the spec. Repeat implement and converge until it reports Converged.

8.  **Review and merge (close):** human gate, check that every change
    traces to the spec, then merge. Specs commit with the code.

Optional checks: /speckit.analyze tests spec, plan and tasks for
consistency; /speckit.checklist builds a quality checklist. Our deck
writes commands as /speckit.specify; current releases show them as
skills (/speckit-specify), and the exact syntax depends on the agent.

# 5. When to pick it

**Pick it when:**

- You are adding features to an existing system and the new behavior has
  to respect its constraints. GitHub names this as the strongest case.

- Many engineers or a strict review process need a versioned, reviewable
  record of what “done” means.

- Security, compliance or failure paths must be pinned down as
  acceptance criteria before code, as in our password-reset example.

- You plan to switch models or agents: the spec and the acceptance suite
  are the safety net.

**Skip it when:**

- The change is a one-liner, CSS, copy or a spike. The spec costs more
  than the change.

- You are still exploring and the behavior is unknown. Over-specifying
  slows that down; spike first, then write the spec.

# 6. What to watch for

- Cost: a good spec takes real upfront time. In our runs, tokens per
  change matched the control (~15k).

- Runs only when called. Nothing fires on its own; enforcement comes
  from the review gates and the constitution. The files are only durable
  if the team follows every phase.

- Specs go stale if nobody owns them. Agents read them on every run, so
  a stale spec misleads the agent and wastes tokens.

- It moves fast. Pin the version, and re-run specify init after an
  upgrade; existing specs are kept.

- Not tested by us: we piloted Spec Kit but did not run it as a scored
  lane, so GitHub’s claim that SDD pays off most on feature work in
  existing systems is untested here. The bundled bug-fix and
  idea-assessment extensions are also untested.

# What our team observed

Spec Kit was run on actual code, outside the five scored lanes. Control
figures come from the scoreboard.

|  |  |
|----|----|
| **Harness** | Cursor Agent |
| **Task types** | Bug fix, feature |
| **Runs** | Run on actual code |
| **Setup time** | ~5 min |
| **Tokens per accepted change** | ~15k, same as control (control: ~15k) |
| **Manual interventions per task** | 6–8, same as control (control: 6–8) |
| **Test result** | ~60% coverage, same as control (control: ~60% coverage) |
| **What surprised us** | Spec Kit left durable spec, plan and task files in the repo, but only when every phase was followed. |
| **What we would change** | Skip it on CSS, copy, spikes and one-liners, and run it as a scored lane in the next bake-off. |
