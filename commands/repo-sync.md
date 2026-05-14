---
description: One-shot sync of ~/.claude/ workflow files to the agentic-workflows GitHub repo with auto-generated commit message and explicit approval gate.
argument-hint: [optional: --dry-run to preview what would sync without pushing]
---

# /repo-sync

Invoke the `repo-sync` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/repo-sync/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Run pre-flight checks per SKILL.md step 2
2. Copy the three published folders only (skills, agents, commands)
3. Show staged diff via `git status --short` before doing anything else
4. Generate the commit message per the heuristics in SKILL.md step 6
5. Surface the proposed message and ask: "Commit and push with this message? (yes / edit / no)"
6. On yes: commit, push, surface the repo URL
7. On edit: take the user's message and use it instead
8. On no: abort cleanly, leave staged changes in repo for manual handling

**Never push without explicit yes to the commit message.**

If `$ARGUMENTS` contains `--dry-run`, show what would sync and the proposed commit message, but do not commit or push.

Private folders that are NEVER synced:
- `~/.claude/CLAUDE.md`
- `~/.claude/kickoffs/`
- `~/.claude/team-reviews/`
- `~/.claude/session-learnings/`
- `~/.claude/agent-evolution/`
- `~/.claude/settings.json`
