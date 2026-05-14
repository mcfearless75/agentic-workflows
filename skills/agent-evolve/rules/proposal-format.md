# Evolution Proposal Schema (Scope-Attached Rule File)

Every proposal the `agent-evolver` produces MUST use this exact shape. The diff + approve gate depends on it being parseable and decision-ready.

## Required structure per proposal

```markdown
### Proposal: <agent-file-name>.md

**Pattern detected:** [One sentence — the recurring critique theme]

**Evidence (N entries):**
- "<exact quote from log>" (YYYY-MM-DD, <workflow>)
- "<exact quote from log>" (YYYY-MM-DD, <workflow>)
- "<exact quote from log>" (YYYY-MM-DD, <workflow>)
[Minimum 3 quotes. Maximum 8 — pick the most representative.]

**Current text to change:**
```
[Exact existing snippet from the agent file]
```

**Proposed new text:**
```
[Exact replacement snippet]
```

**Reasoning:** [2-3 sentences. Why this change addresses the pattern. What it will and will not improve.]

**Risk:** [LOW | MEDIUM | HIGH — and one sentence on what could go wrong]

**Reversibility:** [Easy to revert via git? Yes/No]
```

## Rules for the evolver

1. **Evidence threshold:** Minimum 3 distinct log entries showing the same pattern. Below 3 = signal too thin, skip.
2. **No speculative proposals:** Only propose changes the evidence directly supports. Do not add "while we're at it" improvements.
3. **No deletions of behaviour:** Adding instructions is safer than removing them. If removing, justify it with evidence that the existing instruction is causing the problem.
4. **No scope creep:** Do not propose changing the agent's fundamental role. Only sharpen what it already does.
5. **One pattern per proposal:** If an agent has multiple distinct patterns, generate multiple proposals.

## Required wrapping output

```markdown
# Evolution Proposals — YYYY-MM-DD

**Log entries analysed:** N
**Date range:** YYYY-MM-DD to YYYY-MM-DD
**Agents with sufficient signal:** [list]
**Agents with thin signal (skipped):** [list with entry counts]

---

[Proposals, one per block, ordered by HIGH-confidence first]

---

## Summary
- Proposals generated: N
- Highest-confidence proposal: <agent-file>
- Recommended order of review: [list]
```

## Failure modes to avoid

- **Vague evidence** — "the agent was sometimes unclear" is not evidence; quoted critique entries are
- **Over-engineering** — proposing 8 changes when 2 have clear signal
- **Drift** — proposing changes that move the agent away from its defined role
- **False patterns** — clustering critiques that share a word but not a meaning
