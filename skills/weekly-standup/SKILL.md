# Weekly Standup Skill

Friday sweep across all active projects. One place to see what's moving, what's stuck, and what needs a decision before the week closes.

**Genesis primitives used:**
- **Sequential collation** — no fan-out needed; this is a read-and-synthesise task
- **Scope-Attached Rule File (S6)** — `rules/standup-output.md` enforces identical output shape every week
- **Plan Memento (B4)** — report persists to `~/.claude/standups/`

## When to use

- Every Friday (or Monday morning catch-up)
- Before a client call when you need to know the status of their project fast
- When you've been heads-down on one thing and need to resurface the full picture

**Do not skip this because it feels like admin. It is the filter that stops things falling through the cracks.**

## 8-Step Architect Contract

### 1. State goal
Produce a dated standup report that answers: what's actively in progress, what's stalled, what needs a decision or action this week, and what can be safely deprioritised.

### 2. Name primitives
- Primary input: `~/.claude/projects/*.md` (all project context files)
- Supporting: `~/.claude/kickoffs/` (recent project decisions — check last 30 days)
- Output schema: `rules/standup-output.md`
- Persistence: `~/.claude/standups/standup-YYYY-MM-DD.md`

### 3. Pick pattern
Sequential read + synthesise in parent context. No subagents — this is collation, not analysis fan-out.

### 4. Compose or build
Compose. All required files exist.

### 5. Flags

| Flag | Behaviour |
|---|---|
| *(none)* | Full sweep — all projects |
| `--blocked-only` | Surface only BLOCKED and NEEDS DECISION items |
| `--project <slug>` | Focus on one project; deep-read its context file and surface all detail |

Announce the active flag (or "Full sweep") on the first line of output.

### 6. Sweep logic

#### Step A — Read all project context files
Read every `.md` file in `~/.claude/projects/`. For each file extract:
- Project name and slug
- Current status (active / stalled / needs decision / on hold / shipped)
- What is in progress right now
- Any explicit blockers
- Next action and who owns it
- Evidence of last meaningful update (stated date or recency of content)

If a project listed in CLAUDE.md has no context file, note it as **no context file** in the ADVISORY section.

#### Step B — Staleness check
Flag any project where:
- Status reads "active" but the context file has no stated current sprint or next action
- A "next action" appears to be the same one from a prior standup (no movement)
- A kickoff was run but no first sprint is evidenced

Staleness means potential falling-through-the-cracks. Surface it — do not quietly skip it.

#### Step C — Recent kickoffs check
Scan `~/.claude/kickoffs/` for any file dated within the last 30 days.
- Verdict GO or GO WITH CHANGES + no sprint plan found → flag as **needs first sprint**
- Verdict HOLD or KILL → confirm still parked, or surface for re-evaluation if date suggests it should be reviewed

#### Step D — Assemble report
Follow `rules/standup-output.md` exactly. No improvised sections.

### 7. Persist
Write the completed report to `~/.claude/standups/standup-YYYY-MM-DD.md`.
Create the directory if it does not exist.

### 8. Surface and close
Print the report inline. End with a single line:

> **This week's focus: [one project or task that most needs your attention]**

This line is a genuine prioritisation call. It must name something specific — not "several things need attention."

## Non-negotiables

- If `~/.claude/projects/` is empty or missing, say so plainly and exit — do not fabricate a report
- Only report what context files actually say — UNVERIFIED beats assumed
- BLOCKED items appear first in the report, never buried
- Every item under NEEDS ACTION must include a concrete next step — vague flags are not actionable
- The report must be readable in under 2 minutes — trim anything that does not drive a decision
