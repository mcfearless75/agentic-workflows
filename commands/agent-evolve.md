---
description: Evolve agent definitions based on accumulated self-critique log entries. Surfaces evidence-backed proposals with a mandatory diff + approve gate before any file is modified.
argument-hint: [optional: --dry-run to preview proposals without applying]
---

# /agent-evolve

Invoke the `agent-evolve` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/agent-evolve/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Run pre-flight checks per SKILL.md step 5
2. Invoke the `agent-evolver` agent with the log contents and agent file contents
3. Surface every proposal with full evidence
4. For each proposal, ask the user: yes / no / modify — wait for response, do not batch
5. Apply approved changes via Edit tool only
6. Write changelog entry to `~/.claude/agent-evolution/changelog.md`
7. Archive informing log entries to `~/.claude/agent-evolution/log-archive-YYYY-MM-DD.md`
8. Suggest a git commit message at the end for syncing to the repo

**Never modify an agent file without explicit per-proposal approval.**

If `$ARGUMENTS` contains `--dry-run`, surface proposals only. Do not apply, do not archive, do not write changelog.
