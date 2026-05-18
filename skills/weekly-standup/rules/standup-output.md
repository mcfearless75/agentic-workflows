# Weekly Standup Output Schema

Every standup report MUST follow this shape exactly.

## Required sections (in order)

```markdown
## Weekly Standup — [DD Month YYYY]
**Sweep:** [Full / --blocked-only / --project <slug>]
**Projects scanned:** [n]

---

## BLOCKED (cannot progress without resolution)
- **[Project]** — [blocker description] — [what is needed to unblock]

*(If none: "None.")*

---

## NEEDS DECISION (stalled — waiting on a call or external input)
- **[Project]** — [decision required] — [options or context if known]

*(If none: "None.")*

---

## IN PROGRESS (actively moving this week)

| Project | What is happening | Next action | Owner |
|---|---|---|---|
| [name] | [current state] | [concrete next step] | [person or team] |

*(If none: "None.")*

---

## NEEDS FIRST ACTION (kicked off but not started)
- **[Project]** — kickoff dated [date], verdict [GO / GO WITH CHANGES] — suggested first step: [action]

*(If none: "None.")*

---

## ON HOLD / DEPRIORITISED
- **[Project]** — [reason parked] — [trigger to re-evaluate]

*(If none: "None.")*

---

## ADVISORY
- [Projects with no context file]
- [Stale entries — active status but no visible movement]
- [Any other flags that do not fit the above categories]

*(If none: "None.")*

---

**This week's focus: [one project or task — specific and actionable]**
```

## Tone rules
- British English throughout
- No em dashes
- No padding or filler phrases
- BLOCKED appears first — never buried in the middle of the report
- If a status cannot be determined from the context file, write UNVERIFIED — never assume ACTIVE or ON HOLD
- The "This week's focus" line must name something specific. "Multiple projects" is not acceptable.
- Every item under NEEDS DECISION and NEEDS FIRST ACTION must be genuinely actionable — a real decision or a real first step, not a vague reminder
