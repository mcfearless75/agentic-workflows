# pm-claude-stack

A set of agentic workflows and specialist agents for Claude Code, built on [Daniel Meppiel's Genesis framework](https://github.com/danielmeppiel/genesis).

Two core workflows — one fires before you build anything, one fires before you ship anything.

---

## What's included

### Workflows

| Workflow | Command | When to use |
|---|---|---|
| **Project Kickoff** | `/project-kickoff` | Before any code, design, or content is created |
| **Team Review** | `/team-review` | Before launch, or against any live project |

### Agents (specialist lenses)

| Agent | Role |
|---|---|
| `sales-strategist` | Proposition clarity, buyer psychology, conversion, ICP sharpening |
| `commercial-consultant` | Go/no-go calls, unit economics, scope discipline, P&L lens |
| `project-architect` | Stack decisions, MVP scoping, delivery phases, build risk |
| `ui-ux-lens` | Design quality, hierarchy, trust signals, template-smell detection |

---

## Install

Copy the folders into your Claude Code global config directory.

**macOS / Linux:**
```bash
cp -r agents/* ~/.claude/agents/
cp -r skills/* ~/.claude/skills/
cp -r commands/* ~/.claude/commands/
```

**Windows (Git Bash):**
```bash
cp -r agents/* /c/Users/<yourname>/.claude/agents/
cp -r skills/* /c/Users/<yourname>/.claude/skills/
cp -r commands/* /c/Users/<yourname>/.claude/commands/
```

Restart Claude Code after copying. The workflows and agents are available immediately.

---

## Usage

### `/project-kickoff`

Runs before anything is built. Four lenses fire in parallel: commercial, sales, architect, security.

Produces a dated kickoff doc in `~/.claude/kickoffs/` — your single source of truth for the project.

```
/project-kickoff MyWay — GCSE revision app for dyslexic students, targeting schools and parents

/project-kickoff Client: GLEAM Auto Valeting — new Wix site + online booking, local B2C, West London

/project-kickoff Compliance Passport — SaaS for UK contractor compliance, own product, targeting construction SMEs
```

**Outputs:** `~/.claude/kickoffs/kickoff-YYYY-MM-DD-<slug>.md`

---

### `/team-review`

Runs before launch or against any live project. Dispatches applicable lenses in parallel, enforces a shared output schema, surfaces disagreements rather than averaging them.

```
/team-review https://mypassport.work

/team-review /path/to/project/repo

/team-review "GLEAM wants to add a subscription tier — is it worth it?"
```

**Outputs:** `~/.claude/team-reviews/findings-YYYY-MM-DD-<slug>.md`

---

## Architecture

Built on Genesis primitives:

| Primitive | Genesis concept | What it does here |
|---|---|---|
| `SKILL.md` | Module Entrypoint | Orchestrator — 8-step contract, fan-out logic, acceptance criteria |
| `rules/*.md` | Scope-Attached Rule File | Output schema enforced across all lenses |
| `assets/*.template.md` | Plan Memento | Persisted findings doc written to disk each run |
| `agents/*.md` | Persona Scoping File | Specialist lens identity, frameworks, output format |
| `commands/*.md` | Trigger Orchestrator | Thin invocation layer — loads the skill |

Lenses run in **parallel** (Fan-Out pattern, B1). Synthesis is **dissent-weighted** — disagreements between lenses are surfaced, not smoothed over.

---

## Severity rubric

All findings use four levels: **CRITICAL** / **HIGH** / **MEDIUM** / **LOW**

Defined in `skills/team-review/assets/severity-rubric.md`. Shared across both workflows so "CRITICAL" means the same thing regardless of which lens raised it.

---

## Extending

To add a new lens:

1. Create `~/.claude/agents/<lens-name>.md` — define role, frameworks, output format referencing the relevant `rules/` schema
2. Add the lens to the applicable `SKILL.md` fan-out table
3. Done — no other wiring needed

To add a new workflow:

Follow the Genesis pattern: `SKILL.md` + `rules/<output-schema>.md` + `assets/<template>.md` + `commands/<trigger>.md`.

---

## Credits

Architecture based on [Daniel Meppiel's Genesis framework](https://github.com/danielmeppiel/genesis).
Harness: [Claude Code](https://claude.ai/code) by Anthropic.

---

## Licence

MIT. Use freely, adapt for your stack, credit Genesis if you build on this further.
