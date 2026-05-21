# Skill: incident-to-action

**Type:** composite
**Sub-skills:** incident-response → root-cause-analysis → post-mortem
**Phases:** Pre-work: observability, alerting, runbook (established in advance) | Execution: incident-response, root-cause-analysis | Post-work: post-mortem

## Purpose

End-to-end incident lifecycle workflow: from the moment a problem is detected through mitigation, investigation, and the production of a blameless post-mortem with actionable follow-up items. Closes the loop between incident and systemic improvement.

## When to Invoke

- An active incident is in progress or has just been mitigated.
- A significant degradation or outage has occurred and requires structured follow-up.
- A near-miss warrants a full investigation even if users were not impacted.

## Workflow

### Step 1 — Incident Response · Execution (@incident-response)

During or immediately after detection:

1. Run the incident-response skill: triage severity, establish communication channels, coordinate mitigation.
2. Document actions and observations in real time — this record becomes the source of truth for the investigation.
3. Declare the incident resolved only when the system has returned to normal and the immediate risk is contained.

**Gate:** Incident is declared resolved with a mitigation confirmed. Live documentation covers the full timeline from detection to resolution.

### Step 2 — Root Cause Analysis · Execution (@root-cause-analysis)

After the incident is resolved, while context is fresh:

1. Run the root-cause-analysis skill using the incident timeline as input.
2. Apply 5 Whys or equivalent to reach the systemic root cause — not the proximate trigger.
3. Distinguish contributing factors from the root cause. A single incident often has multiple contributing factors but one root cause.

**Gate:** Root cause is identified at a level specific enough to produce a preventive action. "Human error" is never an acceptable root cause — go one level deeper.

### Step 3 — Post-Mortem · Post-work (@post-mortem)

With the root cause established:

1. Run the post-mortem skill to produce the blameless report.
2. The report must include: timeline, impact summary, root cause, contributing factors, and a set of concrete action items with owners and due dates.
3. Action items must be entered into the issue tracker before the post-mortem is published.

**Gate:** Post-mortem is reviewed by the on-call team and at least one stakeholder. All action items have owners and deadlines.

## Output

A complete incident record containing:

- **Incident timeline** — chronological log from detection to resolution
- **Impact summary** — affected users, services, duration, and severity
- **Root cause** — the systemic cause, not the proximate trigger
- **Contributing factors** — conditions that made the incident worse or harder to detect
- **Action items** — specific, ownable tasks to prevent recurrence, linked to issue tracker tickets
- **Blameless post-mortem document** — suitable for team and stakeholder review

This document is the handoff artifact for engineering teams (code fixes, infrastructure changes) and the Technical Writer (operational runbook updates).
