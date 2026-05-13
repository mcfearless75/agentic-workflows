---
description: Pre-build project kickoff. Runs four specialist lenses in parallel (commercial, sales, architect, security) before a single line of code or design is created. Produces a dated kickoff document as the project's single source of truth.
argument-hint: [project name + one-sentence description + who it's for]
---

# /project-kickoff

Invoke the `project-kickoff` skill for: **$ARGUMENTS**

The skill lives at `~/.claude/skills/project-kickoff/SKILL.md`.

Load the skill and follow it exactly. Do not duplicate the workflow here.

**Required steps once loaded:**
1. Detect project type (step 5 in SKILL.md)
2. Fan-out all four lenses in parallel in a single dispatch (step 7)
3. Validate lens outputs against `rules/kickoff-output.md`
4. Synthesise using `assets/kickoff-template.md`
5. Create `~/.claude/kickoffs/` directory if it does not exist
6. Persist to `~/.claude/kickoffs/kickoff-YYYY-MM-DD-<slug>.md`
7. Surface inline and close with the verdict on one line

**Tip:** The more context in `$ARGUMENTS`, the sharper the lenses. Include:
- What it does
- Who it's for (specific, not "SMEs")
- Any known constraints (budget, timeline, existing stack)
- Whether this is client work or a PaulMc product
