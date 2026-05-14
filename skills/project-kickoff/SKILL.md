---
name: project-kickoff
description: Pre-build project kickoff workflow using Fan-Out + Synthesizer pattern. Fires before any code, design, or content is created. Validates ICP, proposition, tech stack, scope, and commercial case in parallel. Produces a dated kickoff document as the single source of truth for the project. Use for new client engagements, new product builds, and new internal tools.
---

# Project Kickoff Skill

The upstream fix. Catches at zero cost what team-review finds after the fact.

**Genesis primitives used:**
- **Fan-Out (B1)** — four independent lenses run in parallel, fresh contexts
- **Scope-Attached Rule File (S6)** — `rules/kickoff-output.md` enforces identical output shape
- **Plan Memento (B4)** — kickoff doc persists to `~/.claude/kickoffs/`
- **Attention Anchor (B8)** — goal re-injected at synthesis boundary

## When to use

- New client engagement (before scoping call or proposal)
- New product or SaaS idea (before writing a line of code)
- New internal tool (before building)
- Pivoting an existing project (before changing direction)

**Do not skip this to save time. Skipping it costs more time later.**

## 8-Step Architect Contract

### 1. State goal
Produce a single, dated kickoff document for `$ARGUMENTS` that answers: should we build this, for whom, with what stack, scoped to what, and what does done look like?

### 2. Name primitives
- Persona Scoping Files: `commercial-consultant`, `sales-strategist`, `project-architect`, `security-reviewer`
- Scope-Attached Rule File: `rules/kickoff-output.md`
- Plan Memento: `assets/kickoff-template.md` → persisted to `~/.claude/kickoffs/`

### 3. Pick pattern
Fan-Out (4 lenses) + Synthesizer. Reasoning: each lens must be uncontaminated by the others — commercial bias must not soften the security read, and architectural enthusiasm must not inflate the commercial case.

### 4. Compose or build
Compose. All required agents exist. No new code.

### 5. Project type detection
Before dispatching, classify the project from `$ARGUMENTS`:

| Type | Indicators | Lens adjustments |
|---|---|---|
| **Client engagement** | "for [client name]", "client wants", managed site | Commercial lens interrogates *client's* brief and budget signal; architect picks from PaulMc stack |
| **Own product** | "our", "we're building", "I want to build" | Commercial lens interrogates *PaulMc's* unit economics and opportunity cost |
| **Internal tool** | "internal", "for us", "automate our" | Commercial = ROI vs time cost; security = internal data exposure |
| **Pivot / rebuild** | "rebrand", "rebuild", "new direction" | Add a fourth question: what are we walking away from and why |

State the detected type in one line before fan-out.

### 6. Acceptance criteria
- All four lenses return output conforming to `rules/kickoff-output.md`
- Synthesised doc answers all seven kickoff questions (see template)
- Kickoff doc written to `~/.claude/kickoffs/kickoff-YYYY-MM-DD-<slug>.md`
- User has a GO / GO WITH CHANGES / HOLD / KILL verdict before leaving this session
- First sprint is scoped to MVP only — no speculative features

### 7. Fan-Out (parallel dispatch)
Single message, four concurrent agents:

**Commercial-consultant** — go/no-go, unit economics, opportunity cost, scope discipline
Brief: project description + type + "interrogate the commercial case hard. Is this worth building? For whom? What's the unit economics model? What are we not doing while we do this?"

**Sales-strategist** — ICP sharpening, proposition clarity, differentiation, buyer journey
Brief: project description + "who is the specific buyer, what trigger event makes them buy, what one-line outcome do we promise, why this over alternatives?"

**Project-architect** — tech stack, scope MVP definition, delivery phases, build risks
Brief: project description + PaulMc stack context (Wix/Velo, Shopify, Flask, Streamlit, Bootstrap, Supabase, Netlify, Render, GitHub, Python) + "what's the right stack, what's the true MVP, what are the build risks, what's the realistic first sprint?"

**Security-reviewer** — early threat model, data handling, compliance surface
Brief: project description + "threat model this from scratch. What data will it touch? Who are the adversaries? What's the minimum viable security posture for launch?"

Each prompt MUST reference:
- `~/.claude/skills/project-kickoff/rules/kickoff-output.md` as the output contract
- `~/.claude/skills/team-review/assets/severity-rubric.md` for severity ratings
- British English, no em dashes, no padding

### 8. Synthesise + persist
1. Validate all four outputs conform to schema
2. Re-run any lens that returned weak/generic output with a sharper brief
3. Write the kickoff doc to `~/.claude/kickoffs/kickoff-YYYY-MM-DD-<slug>.md` using `assets/kickoff-template.md`
4. **Extract every Self-Critique entry** from the lens outputs and append them to `~/.claude/agent-evolution/log.md`. Format each entry as: `YYYY-MM-DD | project-kickoff | <lens-name> | <critique>`. Create the file/directory if missing.
5. Surface the doc inline
6. End with a single line: the verdict

## Non-negotiables

- All four lenses run in **parallel** — never sequential
- Scope must be MVPonly. If architect scope-creeps, flag it and cut
- If commercial verdict is KILL, say so plainly — do not soften
- Kickoff doc is the contract. Everything built after refers back to it
