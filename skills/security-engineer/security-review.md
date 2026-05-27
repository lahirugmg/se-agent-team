# Skill: security-review

**Type:** composite
**Trigger:** Take a system end-to-end from threat model to a compliance-checked risk picture
**Sub-skills:** threat-modeling → security-audit → vulnerability-assessment
**Phases:** Pre-work: threat-modeling | Execution: security-audit, vulnerability-assessment | Post-work: compliance-review (run after this composite)

## Purpose

End-to-end security assessment workflow for a system or feature. Starts with understanding the threat landscape, moves to hands-on code and configuration review, and closes with a prioritised vulnerability assessment. Produces a risk-ranked finding report with actionable remediation guidance.

## When to Invoke

- A new system or feature is approaching release and requires security sign-off.
- A significant architectural change has introduced new trust boundaries or data flows.
- A periodic security review is due on an existing system.
- A security incident has prompted a broader audit.

## Workflow

### Step 1 — Threat Modeling · Pre-work (@threat-modeling)

Before looking at any code:

1. Read the architecture documentation, data flow diagrams, and PRD.
2. Run the threat-modeling skill: identify assets, trust boundaries, threat actors, and attack vectors using STRIDE.
3. Produce a list of threats ranked by likelihood and impact. This list drives the focus of the audit.

**Gate:** Threat model is complete and reviewed. The audit checklist in Step 2 is derived from the threat model — do not conduct a generic audit without one.

### Step 2 — Security Audit · Execution (@security-audit)

With the threat model as a guide:

1. Run the security-audit skill focused on the threat areas identified in Step 1.
2. Review code, configuration, and infrastructure against the security-guidelines knowledge source.
3. Document every finding with: location, description, severity (Critical/High/Medium/Low), and a suggested remediation.

**Gate:** All high-priority threat areas from the model have been audited. No Critical or High findings are left unreviewed.

### Step 3 — Vulnerability Assessment · Execution (@vulnerability-assessment)

After the code audit:

1. Run the vulnerability-assessment skill to assess the full set of findings from Steps 1 and 2, plus any dependency vulnerabilities.
2. Triage: confirm severity, assess exploitability in the specific deployment context, and assign a remediation priority.
3. Produce the final prioritised finding list.

## Output

A security review report containing:

- **Threat model** — assets, trust boundaries, STRIDE analysis, ranked threat list
- **Audit findings** — each finding with location, description, severity, and remediation guidance
- **Vulnerability assessment** — triaged and prioritised full finding set
- **Remediation plan** — Critical and High items with owners and target dates
- **Sign-off verdict** — CLEAR (no blocking findings), CONDITIONAL (ship with remediation plan), or BLOCKED (critical issues must be fixed before release)

This report is the handoff artifact for the Platform Engineer (to implement infrastructure mitigations) and the Software Engineer (to remediate code findings).
