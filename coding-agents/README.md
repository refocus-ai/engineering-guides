# Coding Agents: Five Methodologies and Spec-Driven Development

On November 17, 2026, Abbas Raza and Faheem Arshad presented "Same Codebase, Five Methodologies" on LinkedIn Live. Six of our engineers ran the same kind of tasks on the same codebase under five methodologies, plus a plain-agent control. These are the guides they wrote afterward.

Recording: [recording link]
Slides: [slides link]

## The guides

| Guide | Methodology | Written by |
|---|---|---|
| [agent-skills.md](agent-skills.md) | Agent Skills (Addy Osmani) | Nadir Ali |
| [pocock-skills.md](pocock-skills.md) | Matt Pocock's skills | Ghassan Gillani |
| [superpowers.md](superpowers.md) | Superpowers | Waleed Amjad |
| [gsd.md](gsd.md) | GSD | Mustansar Iqbal |
| [bmad.md](bmad.md) | BMAD | Agha Abdul Moiz |
| [spec-driven-development.md](spec-driven-development.md) | Spec-driven development (SDD), the lens across all five | Faheem Arshad |

## What we found, in one table

| Lane | Tokens per task | Manual fixes per task |
|---|---|---|
| Plain agent (control) | about 15k | often 6 to 8 |
| Agent Skills | about 40k | 2 to 3 |
| Pocock skills | about 35k | 4 to 5 |
| Superpowers | about 120k (about 8x control) | 0 |
| GSD | not metered by our tool | 0 |
| BMAD | about 281k (about 19x control) | 0 |

How to read it:

- A manual fix is a point where an engineer had to step in and correct the agent before committing.
- BMAD ran on a different tool and model than the other lanes, so its token figure is not directly comparable.
- The tool we used for GSD does not meter tokens, so we report none.
- More process cost more tokens. Superpowers and BMAD removed the manual fixes. The question for your team is whether that trade pays off on each task.

## What our team does

For major new work we run Superpowers, with five skills borrowed from Agent Skills for the anti-skip tables and the doubt review, and Spec Kit for the spec step. We skip all of it on CSS, copy changes, spikes and one-liners.

The agent never commits. An engineer reviews, iterates with the agent, and commits once. The author reviews first, then a peer, with automated review and CI gates after that.

We did not benchmark this combination as its own lane. It is our pick, not a tested result.

## Scope and limits

- One codebase, six engineers. This is a field test, not a benchmark.
- We did not measure lines changed, review time per pull request or defects after merge.
- Tool and model versions are listed at the top of each guide. Results will change as these tools change.

## Credit

The methodologies belong to their authors: Addy Osmani (Agent Skills), Matt Pocock (Pocock skills), and the maintainers of Superpowers, GSD and BMAD. These guides describe how we used them, not how they are meant to be used.
