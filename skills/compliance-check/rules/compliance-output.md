# Compliance Check Output Schema

Every compliance-check output MUST follow this shape exactly.

## Required sections (in order)

```markdown
## Compliance Check
**Contractor / Workforce:** [Name or group]
**Sector:** [Construction / Healthcare / Security]
**Check date:** [YYYY-MM-DD]
**Overall status:** CLEAR / ADVISORY / AT RISK / BLOCKED

---

## Document Status

| Document | Status | Expiry | Days remaining | Notes |
|---|---|---|---|---|
| [Doc name] | COMPLIANT / EXPIRING SOON / EXPIRED / MISSING / UNVERIFIED | [date or —] | [n or —] | [any notes] |

---

## Remediation Required

### IMMEDIATE (cannot work until resolved)
- [Action] — [regulatory basis e.g. "CSCS card required under CDM 2015"]

### THIS WEEK (expires within 7 days)
- [Action] — [deadline]

### THIS MONTH (expires within 30 days)
- [Action] — [deadline]

### ADVISORY
- [Action] — [reason]

*(If no items in a category, write "None.")*

---

## Regulatory Notes
[Any sector-specific compliance notes relevant to this contractor's role or documents]
```

## Tone rules
- British English
- No em dashes
- No padding
- BLOCKED status must appear in the first line summary, not buried
- Regulatory references must name the specific regulation (CDM 2015, HASAWA 1974, SIA licensing requirements, etc.)
- If a document's validity cannot be confirmed, say UNVERIFIED — never assume COMPLIANT
