# Severity Rubric

Shared definitions so "CRITICAL" means the same thing across every lens.

## CRITICAL

**Definition:** Blocks launch, breaks the commercial model, exposes the business to legal/financial risk, or makes the artefact unusable for its intended buyer.

**Examples by lens:**
- *Security*: secrets in repo, SQL injection, missing auth on protected endpoint, GDPR breach pattern
- *Code*: data loss bug, race condition in payment flow, build broken on main
- *UI-UX*: site fails to render on mobile, primary CTA broken, content invisible to crawlers
- *Sales*: proposition is unintelligible to target buyer in 5 seconds, no CTA
- *Commercial*: unit economics inverted (CAC > LTV with no path to fix), single point of failure threatens continuity

**Action implied:** Fix before any further activity. No marketing spend, no demos, no launch.

---

## HIGH

**Definition:** Significant quality or commercial impact. Will measurably hurt conversion, credibility, performance, or velocity if shipped as-is.

**Examples by lens:**
- *Security*: weak rate limiting, missing CSRF on state-changing forms, verbose error messages leaking stack
- *Code*: 200-line function in critical path, no tests on payment logic, N+1 query on hot endpoint
- *UI-UX*: hero looks like a default template, no trust signals above the fold, generic stock imagery
- *Sales*: weak headline, no price anchor, undifferentiated from named competitors
- *Commercial*: scope has drifted, no clear ICP, no metric proving customer value

**Action implied:** Fix before launch or paid acquisition. Acceptable to ship to friendly users while fixing.

---

## MEDIUM

**Definition:** Worth fixing. Not blocking. Affects polish, maintainability, or marginal conversion.

**Examples by lens:**
- *Security*: missing HSTS header, third-party script without SRI
- *Code*: duplication that hasn't bitten yet, missing JSDoc
- *UI-UX*: inconsistent button styles between pages, mediocre typography pairing
- *Sales*: secondary CTA underused, FAQ section missing
- *Commercial*: no clear pricing page (but pricing is communicated elsewhere)

**Action implied:** Add to backlog. Address in next sprint or grouped polish pass.

---

## LOW

**Definition:** Polish. Optional. Style or minor improvement.

**Examples by lens:**
- *Security*: cosmetic header tweaks
- *Code*: variable naming, formatting
- *UI-UX*: micro-animation timing, single icon swap
- *Sales*: wording refinements on non-hero copy
- *Commercial*: nice-to-have reporting metric

**Action implied:** Park. Address when convenient or never.

---

## Calibration test

If you find yourself marking more than ~30% of findings CRITICAL, you are inflating. Re-calibrate. Most reviews should return a small number of CRITICAL, a handful of HIGH, more MEDIUM, and a long tail of LOW (or LOW omitted entirely).
