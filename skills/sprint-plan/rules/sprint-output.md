# Sprint Output Schema (Scope-Attached Rule File)

Every sprint-plan output MUST follow this shape exactly. No exceptions.

## Required sections (in order)

```markdown
## Project
[Project name — one-line context summary from the context file or inferred]

## Sprint Goal
[One sentence: what does a completed sprint look like? What is the user able to do that they cannot do now?]

## This Sprint

### 1. [Ticket title — verb-first]
**What it does:** [One sentence]
**Done when:**
- [ ] [Testable criterion]
- [ ] [Testable criterion]
- [ ] [Testable criterion]
**Size:** S / M / L
**Dependencies:** [None, or what it needs first]

[Repeat for each ticket — 5 to 7 max]

## Next Sprint
- [Item] — [One sentence: why next sprint, not this one]

## Binned
- [Item] — [One sentence: why it is binned]

## Blockers
[Bulleted list of blockers, or "None identified."]

## Skip This Sprint
**[Item name]** — [One sentence: why it is a scope trap right now]

## Saved to
`~/.claude/sprints/<project-slug>-YYYY-MM-DD.md`
```

## Acceptance criteria rules

Criteria must be testable statements, not intentions:

- GOOD: "User can download a CSV of all active contractors"
- BAD: "Export functionality works correctly"

- GOOD: "Login redirects to /dashboard on success, not /home"
- BAD: "Login flow is improved"

## Tone

- British English
- Direct, no padding
- Bin decisions are explained, not apologetic
- No em dashes
- No "this is a great idea" commentary
