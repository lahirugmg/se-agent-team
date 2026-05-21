# Skill: compliance-review

**Type:** atomic

## Purpose

Assess a system against the requirements of a specific compliance framework (SOC 2, GDPR, PCI-DSS, HIPAA, ISO 27001, or similar). Produces a gap analysis — what controls are in place, what is missing, and what must be remediated to achieve or maintain compliance.

## When to Invoke

- An audit is approaching and the system's compliance posture needs to be assessed.
- A new system or feature is being designed and must meet compliance requirements from the start.
- A compliance framework is being newly adopted and the gap between current state and requirements needs to be mapped.
- A change has been made to a system in scope and its compliance impact needs to be assessed.

## Workflow

1. **Identify the applicable framework and scope.** Specify:
   - Which framework(s) apply (SOC 2 Type I/II, GDPR Article X, PCI-DSS requirement set, etc.)
   - Which systems, data, and processes are in scope
   - Which controls are the primary responsibility of this team vs. inherited from a cloud provider or upstream service
   Do not assess a system against a framework without knowing which parts of the framework apply.

2. **Map controls to requirements.** For each requirement in the framework, identify the control(s) that satisfy it. Controls may be:
   - **Technical** — encryption, access controls, logging, patching
   - **Administrative** — policies, procedures, training, documentation
   - **Physical** — data centre controls (often inherited from cloud providers)

3. **Assess each control.** For each control, determine:
   - **Implemented** — the control exists and is operating effectively
   - **Partially implemented** — the control exists but has gaps or is not consistently applied
   - **Not implemented** — the control does not exist
   Gather evidence for each assessment: configuration screenshots, policy documents, audit logs, test results.

4. **Identify gaps.** For each requirement with a missing or partial control, document:
   - The specific requirement text
   - The gap description
   - The risk created by the gap
   - The effort required to close it (High / Medium / Low)

5. **Prioritise remediation.** Group gaps by:
   - **Blocking** — must be closed before a compliance audit can be passed
   - **Significant** — will be flagged in an audit; should be closed before the next review
   - **Advisory** — best practice improvements that strengthen posture but are not audit failures

6. **Document evidence.** Compliance reviews must be defensible. For every control assessed as Implemented, record the evidence. This becomes the audit evidence package.

## Output

- **Scope definition** — framework, in-scope systems, and control ownership map
- **Controls assessment** — each control rated Implemented / Partial / Not implemented with evidence
- **Gap analysis** — each gap with description, risk, effort, and priority
- **Remediation plan** — prioritised list with owners and target dates
- **Evidence package** — documentation supporting each Implemented control
