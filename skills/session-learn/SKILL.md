---
name: session-learn
description: Captures learnings from the current Claude Code session and proposes evidence-backed updates to CLAUDE.md, agent definitions, or new skills. Run at the end of any session (workflow or not) to keep every future session sharper than the last. Includes mandatory diff + approve gate.
---

# Session Learn Skill

The third layer of the self-improvement loop. Agents learn from workflow critiques. This skill learns from everything else.

**Genesis primitives used:**
- **Plan Memento (B4)** — proposals and approved changes persist to `~/.claude/session-learnings/`
- **Scope-Attached Rule File (S6)** — `rules/learning-proposal.md` enforces proposal shape
- **Attention Anchor (B8)** — re-anchors to original CLAUDE.md / agent intent before proposing changes

## When to use

- At the end of a productive session
- After a session where something surprised you (good or bad)
- After a session that revealed a recurring task worth automating
- After a session where you had to repeat the same correction to the model
- Periodic (every 1-2 weeks) catch-up sweep

**Do not run on trivial sessions.** If nothing meaningful happened, there's nothing to learn.

## 8-Step Architect Contract

### 1. State goal
Extract durable learnings from this session and propose evidence-backed updates to the user's setup so the same lessons do not need to be re-learned next time.

### 2. Name primitives
- Input: the current session conversation (in-context)
- Reference: `~/.claude/CLAUDE.md`, `~/.claude/agents/*.md`, `~/.claude/skills/*/SKILL.md`
- Scope-Attached Rule File: `rules/learning-proposal.md`
- Plan Memento (output): `~/.claude/session-learnings/learnings-YYYY-MM-DD-<slug>.md`

### 3. Pick pattern
**In-session sequential analysis with human gate.** Do NOT dispatch a subagent — the analysis must happen in the parent context where the session content lives. Subagents cannot see what just happened in this conversation.

### 4. Compose or build
Compose. All primitives exist.

### 5. Categorise learnings
Sort what happened in the session into these target categories:

| Category | Target file | Example |
|---|---|---|
| **Hard rule / preference** | `~/.claude/CLAUDE.md` | "Always check for SSR on compliance SaaS sites before reviewing positioning" |
| **Agent behaviour improvement** | `~/.claude/agents/<name>.md` | "sales-strategist should always check pricing page before assessing proposition" |
| **New repeatable workflow** | New skill scaffold | "This session repeated X three times — propose /scaffold-x" |
| **Project-specific fact** | `~/.claude/CLAUDE.md` (project section) | "Compliance Passport: client-rendered Wix, needs SSR before any marketing review" |
| **Anti-pattern to avoid** | `~/.claude/CLAUDE.md` | "Do not propose Next.js for client sites unless they have a developer on-staff" |
| **Tool / workflow gap** | Flag-only (no auto-action) | "No workflow exists for X — backlog candidate" |

### 6. Acceptance criteria
- Every proposal cites at least one specific moment from the session as evidence
- No proposal is generic ("be more helpful" is rejected — "when reviewing Wix sites, always check `view-source` first" is accepted)
- Each proposal targets ONE file with ONE change
- Human approval gate per proposal — no batch yes
- Approved changes apply via Edit tool
- Rejected proposals are logged with reason (they may resurface in future sessions and that's data)
- A dated learnings doc is written to `~/.claude/session-learnings/`

### 7. Analyse the session
Working in the parent context, scan the session for:

1. **Repeated corrections** — where the user said "no, actually X" or steered the model
2. **New facts revealed** — about projects, stack, preferences, constraints
3. **Patterns that emerged** — same kind of task done multiple times
4. **Surprises** — outputs that were unexpectedly good or bad and why
5. **Friction points** — where the workflow was clunky and could be smoother
6. **Successful moves** — things that worked particularly well and should be standard practice

For each, draft a proposal per the schema in `rules/learning-proposal.md`.

### 8. Diff + approve gate (non-negotiable)
For each proposal:
1. Surface the proposal inline with full evidence (quote the session moment)
2. Ask the user: "Apply this change to `<target-file>`? (yes / no / modify)"
3. On **yes**: apply edit, append to learnings doc as APPLIED
4. On **no**: skip, log with reason (or "no reason given")
5. On **modify**: capture modification, apply, log both versions

After all proposals processed:
1. Write the dated learnings doc using `assets/learnings-template.md`
2. Suggest a CLAUDE.md commit + agentic-workflows repo commit message
3. Suggest the user runs `/instinct-status` to see if `continuous-learning-v2` captured anything complementary

## Non-negotiables

- **Never edit any file without explicit per-proposal approval**
- **Never propose vague learnings** — "be more concise" is not actionable; "limit team-review verdicts to 80 words" is
- **Never propose changes that contradict existing CLAUDE.md** unless explicitly flagging the contradiction
- **Always preserve the original user voice** — CLAUDE.md additions should sound like the user wrote them (British English, direct, no em dashes, no AI-corporate language)
- If nothing meaningful was learned, say so plainly and exit. A blank learnings doc is fine. Inventing learnings to look productive is not.
