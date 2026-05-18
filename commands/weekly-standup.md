---
description: Friday sweep across all active projects. Surfaces what's blocked, what's in flight, what needs a decision, and what needs a first action. Persists to ~/.claude/standups/.
argument-hint: [--blocked-only] [--project <slug>]
---

# /weekly-standup

Invoke the `weekly-standup` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/weekly-standup/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Read all project context files from `~/.claude/projects/`
2. Check recent kickoffs in `~/.claude/kickoffs/` (last 30 days)
3. Flag: BLOCKED / NEEDS DECISION / IN PROGRESS / NEEDS FIRST ACTION / ON HOLD / ADVISORY
4. Persist report to `~/.claude/standups/standup-YYYY-MM-DD.md`
5. End with one line: the single project or task that most needs attention this week

**BLOCKED items must appear first — never buried.**

Usage examples:
- `/weekly-standup` — full sweep of all projects
- `/weekly-standup --blocked-only` — surface only what's stuck or waiting on a decision
- `/weekly-standup --project traknet` — deep-read one project's context and status
