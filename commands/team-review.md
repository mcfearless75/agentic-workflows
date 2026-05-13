---
description: Multi-lens team review of a project, page, proposition, or codebase. Invokes the team-review skill (Fan-Out + Dissent-Weighted Synthesizer). Persists findings to disk.
argument-hint: [URL, path, or short description of what to review]
---

# /team-review

Invoke the `team-review` skill against: **$ARGUMENTS**

The skill lives at `~/.claude/skills/team-review/SKILL.md` and defines the full 8-step contract, scope detection, lens dispatch, output schema, and persistence rules.

**Do not duplicate the workflow here.** Load the skill and follow it exactly.

Required steps once the skill is loaded:
1. Perform scope detection per SKILL.md step 5
2. Fan-out applicable lenses in a single parallel dispatch (SKILL.md step 7)
3. Each lens output must conform to `rules/review-output.md`
4. Synthesise per `assets/findings.template.md`
5. Persist the report to `~/.claude/team-reviews/findings-YYYY-MM-DD-<slug>.md`
6. Surface the report inline

If the `~/.claude/team-reviews/` directory does not exist, create it before writing.
