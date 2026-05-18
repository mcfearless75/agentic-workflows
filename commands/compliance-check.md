---
description: Validate contractor compliance against UK construction, healthcare, or security regulations. Flags expired, missing, and at-risk documents with a prioritised remediation list.
argument-hint: <contractor name or "all"> [sector: construction/healthcare/security] [paste document data]
---

# /compliance-check

Invoke the `compliance-check` skill: **$ARGUMENTS**

The skill lives at `~/.claude/skills/compliance-check/SKILL.md`.

Load the skill and follow it exactly.

**Required behaviour:**
1. Detect sector from context or arguments
2. Parse contractor document data from the input
3. Check each document: COMPLIANT / EXPIRING SOON / EXPIRED / MISSING / UNVERIFIED
4. Assign overall status: CLEAR / ADVISORY / AT RISK / BLOCKED
5. Produce ranked remediation list: IMMEDIATE / THIS WEEK / THIS MONTH / ADVISORY
6. For bulk checks (5+ contractors), persist report to `~/.claude/compliance-reports/`

**BLOCKED status must appear in the first line — never buried.**

Usage examples:
- `/compliance-check John Smith, CSCS expires 2026-06-01, right to work on file, no RAMS signed`
- `/compliance-check all construction` — paste contractor table after the command
- `/compliance-check Sarah Jones healthcare` — paste document list
