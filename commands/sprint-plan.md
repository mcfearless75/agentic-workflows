---
description: Turn a brain dump into a scoped, prioritised sprint with tickets, acceptance criteria, and blockers flagged.
argument-hint: <project-name> [paste your idea list or describe what needs doing]
---

# /sprint-plan

Invoke the `sprint-plan` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/sprint-plan/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Read project context from `~/.claude/projects/<project-slug>.md` if it exists
2. Accept input in any form — pasted list, file path, or verbal description
3. Triage all items into This Sprint / Next Sprint / Bin
4. Produce 5-7 scoped tickets with acceptance criteria and size ratings
5. Flag blockers explicitly
6. Name one item to skip and explain why it is a scope trap
7. Persist output to `~/.claude/sprints/<project-slug>-YYYY-MM-DD.md`

**Never commit to a sprint longer than a realistic solo week.**

If `$ARGUMENTS` contains only a project name with no idea list, ask the user to paste their input before proceeding.
