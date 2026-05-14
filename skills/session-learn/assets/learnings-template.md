# Session Learnings — {{YYYY-MM-DD}}

**Session topic:** {{One-line summary}}
**Session date:** {{YYYY-MM-DD}}
**Proposals generated:** {{N}}
**Applied:** {{N}}
**Rejected:** {{N}}
**Modified by user:** {{N}}
**Gaps flagged (no action):** {{N}}

---

## Applied Changes

### `<target-file>` — {{category}}

**Pattern:** {{the recurring critique or repeated correction}}
**Evidence:** Quoted moment from session
**Change summary:** One line
**Diff:**
```diff
- old text
+ new text
```
**Approved by:** user
**Reversible via:** `git checkout HEAD~1 -- <file>` (for repo files) or restore from previous CLAUDE.md backup

---

## Rejected Proposals

### `<target-file>` — {{category}}
**Reason:** {{user's reason or "no reason given"}}
**Status:** Logged. Will not be re-proposed unless evidence repeats in future sessions.

---

## Modified Proposals

### `<target-file>` — {{category}}
**Analyser proposed:** {{original new text}}
**User applied:** {{modified version}}
**User's note:** {{optional}}

---

## Gaps Flagged (no action this session)

- {{One-line description of a workflow / tool gap noticed. These accumulate over time and become candidates for the next build.}}

---

## Recommended Follow-up

1. **Sync to repo (if agents or skills changed):**
   ```bash
   cd /c/Users/LAPTOP80/pm-claude-stack
   cp -r ~/.claude/agents/* agents/  # or specific files
   cp -r ~/.claude/skills/* skills/
   git add . && git commit -m "feat: session-learn updates from YYYY-MM-DD" && git push
   ```

2. **Backup CLAUDE.md if it changed:**
   CLAUDE.md is loaded every session — verify the changes render correctly by starting a new session and asking the model to repeat one of the new rules.

3. **Cross-check with continuous-learning-v2:**
   Run `/instinct-status` — see if it captured anything complementary that should also be promoted.

---

## Reverting

CLAUDE.md changes — no automatic git history. Keep a manual backup before each /session-learn run if paranoid.

Agent / skill file changes — git-tracked in the pm-claude-stack repo. Revert via `git checkout`.
