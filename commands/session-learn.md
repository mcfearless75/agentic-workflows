---
description: Capture learnings from the current session and propose evidence-backed updates to CLAUDE.md, agent files, or new skills. Includes per-proposal diff + approve gate.
argument-hint: [optional: --dry-run to preview proposals without applying]
---

# /session-learn

Invoke the `session-learn` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/session-learn/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Analyse the current session in-context — do NOT dispatch a subagent (subagents cannot see the parent conversation)
2. Categorise learnings per SKILL.md step 5
3. Generate proposals per `rules/learning-proposal.md` schema
4. Surface each proposal with quoted session evidence
5. For each proposal, ask the user: yes / no / modify — wait for response, do not batch
6. Apply approved changes via Edit / Write tool only
7. Write dated learnings doc to `~/.claude/session-learnings/learnings-YYYY-MM-DD-<slug>.md`
8. Suggest a git commit message at the end if any agent/skill files changed

**Never modify CLAUDE.md, an agent file, or create a new skill without explicit per-proposal approval.**

If `$ARGUMENTS` contains `--dry-run`, surface proposals only. Do not apply, do not write the learnings doc.

If the session contains nothing meaningful to learn from, say so plainly and exit. Do not invent learnings.
