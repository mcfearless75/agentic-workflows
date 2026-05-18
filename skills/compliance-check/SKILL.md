---
name: compliance-check
description: Validates contractor compliance status against UK construction and workplace regulations. Checks document currency, flags expiries, identifies gaps, and produces a prioritised remediation list. Use for PRL Console, Compliance Passport, and any contractor management context.
model: sonnet
---

# Compliance Check Skill

Audits a contractor or workforce against UK regulatory requirements and flags what is missing, expired, or at risk. No subagents. Fast, direct output.

## Regulations in scope

### Construction / Site (PRL Site Solutions context)
- **CSCS card** — Construction Skills Certification Scheme. Must be valid and appropriate to the role.
- **Right to Work** — UK statutory check. Must be evidenced and on file.
- **Public Liability Insurance** — if self-employed/subcontractor. Check limit and expiry.
- **Employer's Liability Insurance** — if employing others. Legally required.
- **RAMS** — Risk Assessment and Method Statement. Site/task specific. Must be signed.
- **Induction** — site-specific induction signed off before first day on site.
- **DBS check** — required for roles involving vulnerable persons or security.
- **First Aid certificate** — required for designated first aiders. 3-year validity.
- **Asbestos Awareness** — required for any work in buildings pre-2000.
- **Working at Height** — PASMA/IPAF certification where relevant.

### Healthcare / Clinical (Compliance Passport / CQC context)
- **DBS Enhanced** — mandatory for all patient-facing roles. Renewed per employer policy.
- **Right to Work** — as above.
- **Professional registration** — NMC, GMC, HCPC, GDC as applicable. Check active status.
- **Immunisation records** — Hep B, MMR, TB, VZV as per NHS occupational health requirements.
- **Mandatory training** — fire safety, infection control, manual handling, safeguarding. Annual renewal.
- **Professional indemnity** — required for clinical contractors.
- **Fit to practise** — no current fitness to practise concerns on register.

### Security (Copeland Group / site security context)
- **SIA licence** — Security Industry Authority. Door Supervisor or Security Guard as applicable. Check active + expiry.
- **Right to Work** — as above.
- **First Aid** — required for most SIA roles.
- **CCTV licence** — if operating surveillance equipment.

---

## 8-Step Contract

### 1. State goal
Produce a compliance status report for the named contractor or workforce that tells the user exactly what is compliant, what is at risk, and what action is required and by when.

### 2. Detect context
From `$ARGUMENTS`, identify:
- **Sector:** construction / healthcare / security / mixed
- **Input type:** single contractor, list of contractors, or a pasted data dump
- **Check date:** today's date (use current date for expiry calculations)

### 3. Parse input
Accept input in any form:
- Named contractor with document list and dates
- Pasted table or CSV of contractor records
- Free text description of what documents are held

If input is ambiguous, ask one clarifying question before proceeding. Do not guess.

### 4. Check each document
For each document type relevant to the detected sector, assess:

| Status | Meaning |
|---|---|
| COMPLIANT | Present, valid, not expiring within 30 days |
| EXPIRING SOON | Valid now but expires within 30 days |
| EXPIRED | Past expiry date |
| MISSING | No record held |
| UNVERIFIED | Record exists but cannot confirm validity |

Calculate days to expiry where a date is provided.

### 5. Score overall status

| Overall | Criteria |
|---|---|
| CLEAR | All documents COMPLIANT |
| ADVISORY | One or more EXPIRING SOON, none MISSING or EXPIRED |
| AT RISK | One or more EXPIRED, no CRITICAL items |
| BLOCKED | Any MISSING item that is legally required before site/work |

### 6. Produce remediation list
Rank actions by urgency:
1. IMMEDIATE — legally required, missing or expired. Contractor cannot work until resolved.
2. THIS WEEK — expiring within 7 days.
3. THIS MONTH — expiring within 30 days.
4. ADVISORY — best practice gaps, not blocking.

### 7. Output
Follow `rules/compliance-output.md` exactly.

### 8. Persist if bulk check
If checking more than 5 contractors, write output to `~/.claude/compliance-reports/report-YYYY-MM-DD-<slug>.md`.

---

## Non-negotiables
- Never mark a document COMPLIANT if the expiry date is not provided — mark UNVERIFIED
- Never assume a document is held unless explicitly stated
- BLOCKED status must be flagged in the first line of the report, not buried
- Regulatory references must be accurate — if unsure of the exact requirement, say so
