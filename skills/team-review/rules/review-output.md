# Review Output Schema (Scope-Attached Rule File)

Every lens dispatched by the `team-review` skill MUST emit output in this exact shape. Synthesis depends on mechanical parsing of identical structure across lenses.

## Required Sections (in order)

```markdown
## Lens
[One of: sales | commercial | ui-ux | security | code]

## Verdict
[One sentence. The headline finding. Use: SHIP / GO WITH CHANGES / HOLD / KILL / NOT-APPLICABLE]

## Confidence
[HIGH | MEDIUM | LOW — and one sentence on what limits confidence]

## Findings
[Bulleted list. Each finding MUST follow this shape:]
- **[SEVERITY]** [One-line finding]. *Evidence:* [What you observed]. *Impact:* [What it costs if unfixed].

## Strengths
- [Bullets — what is actually good and should be preserved]

## Recommended Actions
[Numbered list, ranked by priority. Each action MUST be concrete and executable, not advisory.]
1. [Specific action, not "consider improving X"]
2. [Specific action]
3. [Specific action]

## What I Could Not Assess
[Be explicit about blind spots so the synthesiser knows the coverage gaps. If you used WebFetch on a client-rendered site and got nothing useful, state it here.]

## Self-Critique
[ONE sentence only. What would you ask, assess, or do differently if you ran this review again? This feeds the agent self-improvement loop. Be specific — "be more concise" is useless; "I should have checked the pricing page before assessing proposition clarity" is useful. If nothing meaningful to improve, write "None this run.".]
```

## Severity values

Use ONLY the values defined in `~/.claude/skills/team-review/assets/severity-rubric.md`:
- **CRITICAL** — blocks launch / ships broken / loses money
- **HIGH** — significant quality or commercial impact
- **MEDIUM** — worth fixing, not blocking
- **LOW** — polish, optional

## Tone rules

- British English
- No em dashes
- No corporate AI-speak ("leverage", "synergy", "robust solutions")
- Direct, commercial, no padding
- If something is fine, write "fine" and move on — do not invent weaknesses to fill space

## Failure modes to avoid

- **Padding** — do not pad bullets to look thorough
- **Hedging** — "could potentially be improved" → just say "improve this"
- **Generic advice** — "improve SEO" is useless; "add Organization JSON-LD with sameAs links to LinkedIn and Companies House" is useful
- **Inventing evidence** — if you can't see it, say so in "What I Could Not Assess"

## Compliance check

Before returning, verify your output:
- [ ] All required sections present, in order
- [ ] Every finding has SEVERITY, Evidence, Impact
- [ ] Verdict is one of the five allowed values
- [ ] No em dashes
- [ ] No invented evidence
