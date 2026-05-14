# Agent Evolution Changelog

A dated record of every agent definition change made through the `/agent-evolve` workflow.

This file is the audit trail. Every entry is reversible via git.

---

## YYYY-MM-DD — Evolution run

**Log entries analysed:** N
**Date range:** YYYY-MM-DD to YYYY-MM-DD
**Proposals generated:** N
**Applied:** N
**Rejected:** N
**Modified by user:** N

### Applied changes

#### `<agent-file>.md`

**Pattern:** [The recurring critique theme]
**Evidence:** N log entries between YYYY-MM-DD and YYYY-MM-DD
**Change summary:** [One line]
**Diff:**
```diff
- old text
+ new text
```
**Approved by:** user (default — this is a single-user workflow)
**Reversible via:** `git checkout HEAD~1 -- agents/<agent-file>.md`

### Rejected proposals

#### `<agent-file>.md` — [pattern]
**Reason given:** [User's reason, or "no reason given"]
**Status:** Logged. Original critique entries remain in the log for future re-analysis.

### Modified proposals

#### `<agent-file>.md` — [pattern]
**Evolver proposed:** [original new text]
**User applied:** [modified new text]
**User's note:** [optional]

### Archived log entries

Entries that informed approved changes have been moved to:
`~/.claude/agent-evolution/log-archive-YYYY-MM-DD.md`

Entries supporting rejected or skipped proposals remain in the live log.

---

## Reverting a change

```bash
cd /c/Users/LAPTOP80/pm-claude-stack
git log --oneline agents/<agent-file>.md
git checkout <commit-hash>~1 -- agents/<agent-file>.md
cp agents/<agent-file>.md ~/.claude/agents/
```
