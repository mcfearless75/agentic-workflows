---
name: team-review
description: Multi-lens project review using Fan-Out + Dissent-Weighted Synthesizer pattern. Dispatches independent specialist agents in parallel against a project, page, proposition, or codebase, enforces a shared output schema, and persists findings to disk. Use for pre-launch reviews, go/no-go decisions, and proposition stress-tests.
---

# Team Review Skill

Multi-lens advisory review built on Genesis primitives:
- **Fan-Out (B1)** — independent lenses run in parallel, each in a fresh context
- **Scope-Attached Rule File (S6)** — `rules/review-output.md` enforces identical output shape
- **Dissent-Weighted Synthesizer (A1)** — surface disagreement, do not average
- **Plan Memento (B4)** — findings persist to dated file, not just chat

## When to use

- Pre-launch review of a project, page, or product
- Go/no-go calls on a proposition
- Stress-testing a business idea before commitment
- Periodic health check of an active project

## 8-Step Architect Contract

### 1. State goal
One sentence: produce an actionable, multi-perspective verdict on `$ARGUMENTS` that the user can act on tomorrow.

### 2. Name primitives
- Persona Scoping Files: `~/.claude/agents/sales-strategist.md`, `commercial-consultant.md`, `ui-ux-lens.md`, `security-reviewer.md`, `code-reviewer.md`
- Scope-Attached Rule File: `rules/review-output.md`
- Assets: `assets/severity-rubric.md`, `assets/findings.template.md`
- Child-Thread Spawn: parallel Agent tool calls

### 3. Pick pattern
**Fan-Out + Dissent-Weighted Synthesizer.** Reasoning: lenses must not influence each other; one strong voice should not contaminate another's read. Fresh contexts enforce isolation.

### 4. Compose or build
Compose. All required primitives exist. No new code.

### 5. Scope detection
Before dispatching, identify artefact type and pick lenses:

| Artefact | Lenses |
|---|---|
| Codebase / repo | security, code, ui-ux, sales, commercial |
| Live website / landing page | security (surface only), ui-ux, sales, commercial |
| Proposition / business idea (no artefact yet) | sales, commercial |
| Single page / component | ui-ux, sales (if customer-facing), security (if user data) |

State the detected scope in one line before fan-out.

### 6. Acceptance criteria
- All lenses return output conforming to `rules/review-output.md`
- Synthesis surfaces at least one disagreement when lenses disagree (do not average)
- Findings written to `~/.claude/team-reviews/findings-YYYY-MM-DD-<slug>.md`
- User has at least 3 concrete next actions ranked by priority

### 7. Fan-Out (parallel dispatch)
In a single message, launch all applicable agents concurrently. Each prompt MUST:
- State the artefact and provide URL / paths
- Reference `~/.claude/skills/team-review/rules/review-output.md` as the output contract
- Reference `~/.claude/skills/team-review/assets/severity-rubric.md` for severity meaning
- Instruct the agent to use WebFetch where the artefact is a URL
- Demand British English, no em dashes, no padding

### 8. Synthesise + persist
Once all lenses return:
1. Validate each output conforms to the schema. Re-run any lens that returned weak / generic output with sharper context.
2. Write the consolidated report to `~/.claude/team-reviews/findings-YYYY-MM-DD-<slug>.md` using `assets/findings.template.md` as the structure.
3. **Extract every Self-Critique entry** from the lens outputs and append them to `~/.claude/agent-evolution/log.md`. Format each entry as: `YYYY-MM-DD | team-review | <lens-name> | <critique>`. Create the file/directory if missing.
4. Surface the report inline as the response.

## Non-negotiables

- Lenses run in **parallel**, never sequential
- Do not edit lens outputs before synthesis — quote, don't paraphrase, when surfacing critical findings
- Disagreements between lenses are first-class output, not noise to smooth over
- If WebFetch returns nothing (client-rendered site), that IS a finding — flag it as CRITICAL credibility/SEO risk and continue with inferential review
