# Kickoff Output Schema (Scope-Attached Rule File)

Every lens dispatched by the `project-kickoff` skill MUST emit output in this exact shape. No exceptions.

## Required Sections (in order)

```markdown
## Lens
[One of: commercial | sales | architect | security]

## Verdict
[GO / GO WITH CHANGES / HOLD / KILL / NEEDS-MORE-INFO — one word or phrase]

## Confidence
[HIGH | MEDIUM | LOW — one sentence on what limits confidence]

## Key Findings
[Bulleted list. Each finding MUST follow:]
- **[SEVERITY]** [One-line finding]. *Evidence or reasoning:* [...]. *Impact if ignored:* [...].

## Recommendations
[Numbered, ranked by priority. Concrete and specific — not advisory.]
1. [Action]
2. [Action]
3. [Action]

## Open Questions
[Questions this lens cannot answer but the synthesiser or user must resolve before proceeding.]
1. [Question]
2. [Question]

## What I Could Not Assess
[Blind spots due to missing information. Be explicit.]
```

## Severity values

Use ONLY values from `~/.claude/skills/team-review/assets/severity-rubric.md`:
- **CRITICAL** — blocks launch or commercial viability
- **HIGH** — significant risk or quality impact
- **MEDIUM** — worth addressing before scale
- **LOW** — polish or optional improvement

## Tone rules

- British English
- No em dashes
- No corporate AI-speak
- Direct — lead with the verdict, then the reasoning
- If you need more information to give a high-confidence answer, say so in Confidence and Open Questions — do not invent to fill space

## Failure modes to avoid

- **Over-enthusiasm** — "this is a great idea" is not a finding
- **Generic risks** — "market may be competitive" without naming competitors is useless
- **Scope inflation** — architects must not add features; they scope to MVP only
- **Soft verdicts** — if it should be KILL, say KILL. "HOLD pending further analysis" is usually cowardice

## Compliance check

Before returning:
- [ ] All sections present in order
- [ ] Every finding has SEVERITY + Evidence + Impact
- [ ] Verdict is one of the five allowed values
- [ ] Open Questions listed (at least one if confidence is not HIGH)
- [ ] No em dashes
