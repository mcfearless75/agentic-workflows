---
name: repo-sync
description: One-shot sync of ~/.claude/ workflow files to the agentic-workflows GitHub repo. Detects changes since the last sync, copies files, generates a sensible commit message, and pushes. Use after building or evolving any workflow, agent, skill, or command.
---

# Repo Sync Skill

Eliminates the manual `cp` + `git add` + `git commit` + `git push` dance every time a workflow file changes.

## Repo location

Local clone: `C:\Users\LAPTOP80\pm-claude-stack`
Remote: `https://github.com/mcfearless75/agentic-workflows`

## When to use

- After any change to `~/.claude/skills/`, `~/.claude/agents/`, or `~/.claude/commands/` that you want public
- After running `/agent-evolve` or `/session-learn` and approving changes
- Periodic catch-up sweep if changes have piled up

## What it syncs

Only these subdirectories of `~/.claude/`:
- `skills/` → `pm-claude-stack/skills/`
- `agents/` → `pm-claude-stack/agents/`
- `commands/` → `pm-claude-stack/commands/`

It does NOT sync:
- `~/.claude/CLAUDE.md` (personal — never publish)
- `~/.claude/kickoffs/` (project-specific outputs)
- `~/.claude/team-reviews/` (project-specific outputs)
- `~/.claude/session-learnings/` (personal learning audit)
- `~/.claude/agent-evolution/` (personal critique log)
- `~/.claude/settings.json` (personal hooks and permissions)

Anything outside the three published folders is private. Always.

## 8-Step Contract

### 1. State goal
Sync local workflow changes from `~/.claude/` to the agentic-workflows repo with an honest, auto-generated commit message.

### 2. Pre-flight checks
1. Confirm repo exists at `C:\Users\LAPTOP80\pm-claude-stack`. If not, abort.
2. Confirm remote is `https://github.com/mcfearless75/agentic-workflows.git`. If not, warn and ask.
3. Check for uncommitted changes already in the repo — if dirty, surface them first before adding more.

### 3. Copy changed files — WHITELIST ONLY

**CRITICAL:** Do NOT blanket-copy `~/.claude/skills/*`, `~/.claude/agents/*`, or `~/.claude/commands/*`. Those folders contain hundreds of global Claude Code system files (system agents, third-party skills, etc.) that must never enter the public repo.

Copy ONLY the files explicitly authored for this stack. The whitelist:

**Agents (authored personas):**
- `agents/sales-strategist.md`
- `agents/commercial-consultant.md`
- `agents/project-architect.md`
- `agents/ui-ux-lens.md`
- `agents/agent-evolver.md`
- `agents/paulmc-voice.md`

**Skills (authored workflows):**
- `skills/team-review/` (whole folder)
- `skills/project-kickoff/` (whole folder)
- `skills/agent-evolve/` (whole folder)
- `skills/session-learn/` (whole folder)
- `skills/repo-sync/` (whole folder)
- `skills/sprint-plan/` (whole folder)

**Commands (authored triggers):**
- `commands/team-review.md`
- `commands/project-kickoff.md`
- `commands/agent-evolve.md`
- `commands/session-learn.md`
- `commands/repo-sync.md`
- `commands/sprint-plan.md`

Copy each explicitly (Git Bash syntax):

```bash
cd /c/Users/LAPTOP80/pm-claude-stack

# Agents
for f in sales-strategist commercial-consultant project-architect ui-ux-lens agent-evolver paulmc-voice; do
  cp /c/Users/LAPTOP80/.claude/agents/$f.md agents/
done

# Skills
for d in team-review project-kickoff agent-evolve session-learn repo-sync sprint-plan; do
  cp -r /c/Users/LAPTOP80/.claude/skills/$d skills/
done

# Commands
for f in team-review project-kickoff agent-evolve session-learn repo-sync sprint-plan; do
  cp /c/Users/LAPTOP80/.claude/commands/$f.md commands/
done
```

If a new authored file is added to the stack, add it to the whitelist above before the next sync.

### 4. Stage and review
```bash
git add -A
git status --short
```

Surface the staged changes to the user. **Do NOT proceed without showing what changed.**

### 5. Skip when empty
If `git status --short` returns nothing after staging, exit cleanly: "Nothing to sync. Local already matches repo."

### 6. Auto-generate commit message
Analyse the staged files and build a message in this shape:

```
<type>: <one-line summary>

- <change 1>
- <change 2>
```

Type heuristic:
- New files only → `feat:`
- Modified files only → `refactor:` (if behaviour same) or `feat:` (if behaviour changed)
- Deletes only → `chore:`
- Mixed → `feat:` if any feature-shaped change, else `refactor:`

Summary heuristic — name what changed at the highest meaningful level:
- New skill: "add /<name> workflow"
- New agent: "add <name> agent"
- Edited rule file: "tighten <name> output schema"
- Edited SKILL.md: "improve <name> orchestration"
- Multiple things: "sync <N> changes across <areas>"

### 7. Confirm before committing
Show the proposed commit message to the user. Ask: **"Commit and push with this message? (yes / edit / no)"**

- **yes** → proceed
- **edit** → take the user's version
- **no** → abort, leave repo dirty for them to handle manually

### 8. Commit, push, surface URL
```bash
git commit -m "<message>"
git push 2>&1 | tail -3
```

Confirm success and surface the repo URL: `https://github.com/mcfearless75/agentic-workflows`

## Non-negotiables

- **Always show the staged diff before committing** — the user must see what's being published
- **Never push without explicit yes** to the commit message
- **Never sync CLAUDE.md or any of the private folders** listed above
- **Never use --force** push under any circumstance

## Failure modes to watch

- **PowerShell vs Git Bash** — commands assume Git Bash on Windows. If the user is in PowerShell, use the semicolon-chained variant instead.
- **LF/CRLF warnings** — harmless, ignore them.
- **Detached HEAD** — if `git status` shows detached HEAD, abort and ask user to resolve.
