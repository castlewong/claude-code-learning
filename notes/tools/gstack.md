# gstack Learnings

Notes on using [gstack](https://github.com/garrytan/gstack) — a software factory built on top of Claude Code.

---

## What is gstack?

gstack turns Claude Code into a virtual engineering team with specialized roles. Instead of a generic AI assistant, you get 18 specialists (CEO, Eng Manager, QA Lead, Release Engineer, etc.) that you invoke as slash commands at the right stage of your sprint.

Created by Garry Tan (YC President & CEO) — he ships 10,000–20,000 lines of production code per day, part-time, using this setup.

---

## Core Principles

### 1. Boil the Lake

> AI makes the marginal cost of completeness near-zero. Always do the complete thing.

- A **lake** is boilable: 100% test coverage, full feature implementation, all edge cases
- An **ocean** is not: full system rewrites, multi-quarter migrations
- "Good enough" is legacy thinking from when human time was the bottleneck
- With AI, "complete" costs minutes more — there's no excuse to skip the last 10%

**Anti-patterns to avoid:**
- "Choose the 90% solution to save time" — if the full version is 70 lines more, just do it
- "We'll add tests in a follow-up PR" — tests are the cheapest lake to boil
- "This would take 2 weeks" — always say "2 weeks human / ~1 hour AI-assisted"

### 2. Search Before Building

Before building anything unfamiliar, stop and search first. The cost of checking is near-zero.

**Three Layers of Knowledge:**

| Layer | What it is | Risk |
|-------|-----------|------|
| **Layer 1** | Tried and true, battle-tested patterns | Assuming it's right without questioning |
| **Layer 2** | New and popular (blog posts, ecosystem trends) | Accepting the crowd uncritically |
| **Layer 3** | First principles — original reasoning about the specific problem | Not doing it at all |

The best projects avoid reinventing wheels (Layer 1) AND make brilliant out-of-distribution observations (Layer 3). Search results are **inputs to your thinking**, not answers.

---

## The Sprint Workflow

gstack is a process, not just a toolset. Each skill feeds into the next:

```
Think → Plan → Build → Review → Test → Ship → Reflect
```

| Stage | Skill | Role |
|-------|-------|------|
| Think | `/office-hours` | Reframes your product. Pushes back on your framing before you write code. |
| Plan | `/plan-ceo-review` | Challenges scope. Finds the 10-star product inside your request. |
| Plan | `/plan-eng-review` | Locks architecture, diagrams, data flow, edge cases, test matrix. |
| Plan | `/plan-design-review` | Rates design dimensions 0–10 and edits the plan to get there. |
| Build | `/design-consultation` | Build a complete design system. Writes DESIGN.md. |
| Review | `/review` | Finds bugs that pass CI but blow up in production. Auto-fixes obvious ones. |
| Review | `/investigate` | Root-cause debugging. Iron Law: no fixes without investigation. |
| Test | `/qa` | Opens real browser, clicks through app, finds and fixes bugs with atomic commits. |
| Test | `/qa-only` | Same as /qa but report-only — no code changes. |
| Ship | `/ship` | Merge base, run tests, audit coverage, bump version, create PR. |
| Ship | `/land-and-deploy` | Merges PR, waits for CI, verifies production. |
| Monitor | `/canary` | Post-deploy monitoring for errors and regressions. |
| Monitor | `/benchmark` | Track page load, Web Vitals, bundle size before/after. |
| Docs | `/document-release` | Syncs all docs (README, ARCHITECTURE, CHANGELOG) with what shipped. |
| Reflect | `/retro` | Weekly engineering retrospective with per-person breakdowns. |

### Power Tools

| Skill | What it does |
|-------|-------------|
| `/codex` | Second opinion from OpenAI Codex — cross-model adversarial review |
| `/careful` | Warns before destructive commands (rm -rf, DROP TABLE, force-push) |
| `/freeze` | Locks edits to one directory while debugging |
| `/guard` | `/careful` + `/freeze` combined — max safety for prod work |
| `/browse` | Real Chromium browser with real clicks — gives Claude eyes |

---

## Compression Ratios

With AI assistance, time estimates change dramatically:

| Task | Human team | AI-assisted | Compression |
|------|-----------|-------------|-------------|
| Boilerplate / scaffolding | 2 days | 15 min | ~100x |
| Test writing | 1 day | 15 min | ~50x |
| Feature implementation | 1 week | 30 min | ~30x |
| Bug fix + regression test | 4 hours | 15 min | ~20x |
| Architecture / design | 2 days | 4 hours | ~5x |
| Research / exploration | 1 day | 3 hours | ~3x |

---

## Key Lessons Learned

### On testing
- 100% test coverage is the goal — tests make vibe coding safe instead of yolo coding
- `/ship` bootstraps test frameworks from scratch if you don't have one
- Every bug fix should generate a regression test
- Every conditional (if/else) needs tests for both paths

### On the /ship workflow
- Always work from a **feature branch** — /ship creates a PR against the base branch
- /ship runs: merge base → tests → coverage audit → pre-landing review → version bump → CHANGELOG → bisectable commits → push → PR → docs sync
- Version format is 4-digit: `MAJOR.MINOR.PATCH.MICRO`
- Auto-picks MICRO or PATCH based on diff size; asks for MINOR/MAJOR

### On parallel sprints
- gstack is powerful with one sprint; transformative with 10–15 running in parallel
- Each agent knows what to do and when to stop because the process is structured
- You manage them like a CEO: check in on decisions that matter, let the rest run

### On the Review Readiness Dashboard
- /ship shows a dashboard before pushing: Eng Review, CEO Review, Design Review, Adversarial
- Eng Review is required by default — gates shipping
- Adversarial review auto-scales: small diffs skip it, large diffs get 4 passes

### On the /office-hours philosophy
- Don't say what feature you want — describe the pain
- The agent reframes the problem before you write a line of code
- "You said daily briefing app — but you're really building a personal chief of staff AI"

---

## Install

```bash
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```

Then add a `gstack` section to your project's `CLAUDE.md` listing the available skills (see this repo's CLAUDE.md for an example).
