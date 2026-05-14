---
name: agent-evolve
description: Reads the agent self-critique log, clusters recurring patterns by agent, and proposes diffs to the relevant agent definition files. Includes mandatory human diff + approve gate before any file is modified. Use periodically (every 2-4 weeks) to evolve agents based on observed weaknesses.
---

# Agent Evolve Skill

Closes the self-improvement loop. The agents critique themselves on every run; this skill turns those critiques into actual file changes — with a human approval gate.

**Genesis primitives used:**
- **Plan Memento (B4)** — `~/.claude/agent-evolution/log.md` is the input substrate
- **Persona Scoping File** — `agent-evolver` agent does the analysis
- **Scope-Attached Rule File (S6)** — `rules/proposal-format.md` enforces proposal shape
- **Attention Anchor (B8)** — every proposal re-anchors to the original agent's defined role

## When to use

- Every 2-4 weeks, or once the log has 20+ entries
- After a workflow has been used heavily on real projects
- Before publishing a new version of the repo

**Do not run too often.** Self-improvement on thin data produces drift, not improvement.

## 8-Step Architect Contract

### 1. State goal
Surface evidence-backed improvement proposals for the agent definitions in `~/.claude/agents/`, based on patterns in `~/.claude/agent-evolution/log.md`. Apply only those the user explicitly approves.

### 2. Name primitives
- Plan Memento (input): `~/.claude/agent-evolution/log.md`
- Plan Memento (output): `~/.claude/agent-evolution/changelog.md`
- Persona: `agent-evolver`
- Scope-Attached Rule File: `rules/proposal-format.md`
- Asset: `assets/changelog-template.md`

### 3. Pick pattern
**Sequential analysis with human gate.** Not fan-out — this is a deliberate, single-thread review where consistency matters more than perspective diversity. Diff + approve is non-negotiable.

### 4. Compose or build
Compose. All primitives exist.

### 5. Pre-flight checks
Before invoking the evolver:
1. Confirm `~/.claude/agent-evolution/log.md` exists. If missing or empty, abort with: "No critique data yet. Run /team-review or /project-kickoff a few times, then return."
2. Count entries. If < 10, warn the user and ask: "Only N entries. Recommend at least 20 before evolving. Continue anyway? (yes/no)"
3. List which agents have entries and how many.

### 6. Acceptance criteria
- Every proposal includes: agent name, evidence (quoted log entries), proposed change (diff format), and reasoning
- No file modification happens before explicit user approval per proposal
- Approved changes are written via Edit tool to the agent file
- A changelog entry is appended to `~/.claude/agent-evolution/changelog.md` for every applied change
- Log entries that informed approved changes are archived (moved, not deleted) to `~/.claude/agent-evolution/log-archive-YYYY-MM-DD.md`

### 7. Invoke evolver
Use the `agent-evolver` agent. Prompt MUST include:
- The full contents of `log.md` (or a clustered summary if > 100 entries)
- The list of agent files in `~/.claude/agents/` and their current content
- A reference to `~/.claude/skills/agent-evolve/rules/proposal-format.md` as the output contract
- Instruction: "Cluster by agent. Only propose changes where you have evidence from ≥3 critique entries. Quote the entries as evidence. Output one proposal block per agent, or 'No actionable patterns for <agent>' if signal is too thin."

### 8. Diff + approve gate (non-negotiable)
For each proposal:
1. Surface the proposal inline with full evidence and the proposed diff
2. Ask the user explicitly: "Apply this change to `<agent-file>`? (yes / no / modify)"
3. On **yes**: apply the edit via the Edit tool, then append to changelog
4. On **no**: skip, log the rejection in the changelog with reason
5. On **modify**: capture user's modification, apply that instead, log both versions

Do not batch-approve. Each proposal gets its own gate.

After all proposals are processed:
1. Write the dated changelog entry
2. Archive informing log entries
3. Suggest a git commit message for the repo sync

## Non-negotiables

- **Never edit an agent file without explicit user approval for that specific edit**
- Never apply changes silently
- Never delete log entries — archive them
- Never propose a change without quoting the evidence
- If the evolver returns vague or unsupported proposals, reject the output and re-prompt with sharper constraints
