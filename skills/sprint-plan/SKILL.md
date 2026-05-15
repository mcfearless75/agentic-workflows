---
name: sprint-plan
description: Turns a brain dump of ideas, bugs, and features into a scoped, prioritised sprint ready to work from. Reads project context if available. Outputs triage, sprint scope, acceptance criteria, and blockers. Use at the start of any work session or planning cycle.
model: sonnet
---

# Sprint Plan Skill

Converts rough input into a clean, executable sprint. No subagents. Fast, cheap, direct.

Built on Genesis primitives:
- **Scope-Attached Rule File (S6)** — `rules/sprint-output.md` enforces identical output shape every run
- **Plan Memento (B4)** — output persists to `~/.claude/sprints/` not just chat

## When to use

- Start of a new sprint or work session
- After a batch of ideas have piled up
- When you're not sure what to work on next
- Before committing dev time to a feature

## 8-Step Contract

### 1. State goal
Turn the provided input into a scoped, prioritised sprint the user can start immediately.

### 2. Read project context
Check for a context file at `~/.claude/projects/<project-slug>.md`. If it exists, read it first. It contains stack, current state, known constraints, and running decisions. Do not ask for context that is already in there.

Project slug mapping:
- "traknet" → `traknet.md`
- "tranmere" or "tranmere-tracker" → `tranmere-tracker.md`
- "prl" or "prl-console" → `prl-console.md`
- "passport" or "mypassport" → `compliance-passport.md`
- "myway" → `myway.md`

If no context file exists, infer from the input and note what was assumed.

### 3. Parse input
Accept input in any form:
- Pasted brain dump (bullet list, prose, mixed)
- Path to a notes file
- Verbal description ("fix the login, add exports, tidy the dashboard")

If no input is provided beyond the project name, ask: "Paste your idea list or describe what needs doing."

### 4. Triage
Sort every item into three buckets:

| Bucket | Criteria |
|---|---|
| **This sprint** | Clear, sized, unblocked, delivers real value now |
| **Next sprint** | Good idea but not urgent, or depends on something in this sprint |
| **Bin** | Scope creep, vague, low value, or contradicts project direction |

Be ruthless. A sprint with 10 items is not a sprint. Target 5-7 this-sprint items max.

### 5. Scope the sprint
From the This Sprint bucket, produce 5-7 tickets.

Each ticket must have:
- **Title** — one line, verb-first ("Add CSV export", "Fix login redirect on mobile")
- **What it does** — one sentence
- **Done when** — 2-3 testable acceptance criteria
- **Size** — S / M / L (S = under 2 hours, M = half day, L = full day)
- **Dependencies** — what it needs before it can start, or "none"

Total sprint must fit a realistic solo week. No more than 2 L tickets per sprint.

### 6. Flag blockers
List anything that will prevent the sprint completing:
- Missing decisions
- Waiting on third parties
- Tech unknowns that need a spike

If none, say "None identified."

### 7. Name one thing to skip
Call out the single item most likely to inflate scope if allowed in. One sentence on why it is a trap right now.

### 8. Persist output
Write the sprint plan to `~/.claude/sprints/<project-slug>-YYYY-MM-DD.md`.
Confirm the file path at the end of the response.

## Output format

Follow `~/.claude/skills/sprint-plan/rules/sprint-output.md` exactly.

## Non-negotiables

- Sprint scope must be completable in a realistic solo week
- Every ticket must have testable acceptance criteria
- Bin items must be named and explained — never silently dropped
- If the context file is missing key info, flag the gap — do not invent constraints
- No padding, no "great idea" commentary — triage and scope only
