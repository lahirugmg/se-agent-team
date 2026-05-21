# SDLC Flow

The eight roles map cleanly onto an eight-stage lifecycle. Each stage has an owning role, an input from the prior stage, an output to the next, and a quality gate that must be true before the work is considered handed off.

```
requirements → architecture → implementation → testing → security → deployment → operations → documentation
     BA              TA              SWE           QA       SecEng     Platform        SRE         TW
```

This is not waterfall. Roles overlap in real work — Security may threat-model alongside Architecture, the Writer may draft alongside Implementation, the SRE may push for observability requirements during Architecture. But every stage has an *owner* who is accountable for the gate, regardless of who participates.

## Stages

### 1. Requirements

**Owner:** Business Analyst
**Input:** Stakeholder request, market signal, or unspoken need
**Output:** PRD + user stories with testable acceptance criteria, explicit out-of-scope list, stakeholder sign-off
**Gate:** Acceptance criteria are independently testable by the QA Engineer without further clarification.

### 2. Architecture

**Owner:** Technical Architect
**Input:** PRD + hard constraints (compliance, latency, cost, team capability)
**Output:** System design, ADRs for every irreversible decision, technical specification a new engineer can implement against
**Gate:** Feasibility confirmed; failure modes and operational model are defined; architecture-review is signed off against the original requirements.

### 3. Implementation

**Owner:** Software Engineer
**Input:** Technical spec + ADRs + golden paths from the Platform Engineer
**Output:** Implementation in thin vertical slices, each with passing tests, commit-by-commit traceable to spec cases
**Gate:** Every spec case has a corresponding passing test; code-review or agent-output-review is complete; no unspecified behaviour is added.

### 4. Testing

**Owner:** QA Engineer
**Input:** Implementation + spec + acceptance criteria
**Output:** Test plan executed, bug reports for defects (reproducible steps, severity), sign-off verdict (PASS / PASS WITH CONDITIONS / FAIL)
**Gate:** All acceptance criteria are covered; performance baselines are met; the verdict is backed by a documented test record.

### 5. Security

**Owner:** Security Engineer
**Input:** System design + implementation + dependency manifest
**Output:** Threat model (STRIDE), audit findings with severity, exploit path, and remediation; dependency-vulnerability triage; compliance verdict
**Gate:** All Critical findings have remediation plans; any accepted risks are documented with named owners and review dates.

### 6. Deployment

**Owner:** Platform Engineer
**Input:** Verified, security-reviewed build + service manifest
**Output:** Deployment through the golden path with infrastructure-as-code, CI/CD pipeline records, rollback capability
**Gate:** The service is deployable end-to-end by the product team without platform-team intervention; rollback is tested.

### 7. Operations

**Owner:** SRE
**Input:** Deployed service + SLO definitions + runbooks
**Output:** Observability and alerting in place; incident response when SLOs are breached; root-cause analysis; post-mortem with owned action items
**Gate:** SLOs are defined from user-visible behaviour; alerts are symptom-based and actionable; every incident produces a post-mortem with dated remediation.

### 8. Documentation

**Owner:** Technical Writer
**Input:** Implementation diff + spec + runbooks + post-mortems + release notes
**Output:** API docs, user guides, runbooks, changelogs, onboarding materials; stakeholder-facing impact summary
**Gate:** Every procedural document has been followed step-by-step on the real system; every significant doc has a named owner and review date.

## Cross-Cutting Concerns

Some work does not belong to a single stage:

| Concern | Threaded through | Owned by |
|---|---|---|
| Threat modeling | Architecture, Implementation | Security Engineer |
| Observability requirements | Architecture, Implementation, Deployment | SRE (defining), Platform Engineer (providing) |
| Performance baselines | Architecture, Testing, Operations | QA Engineer (defining), SRE (measuring in prod) |
| Documentation updates | Every stage | Technical Writer |
| Compliance evidence | Architecture through Operations | Security Engineer |

## Gate Failure

A gate failure is not a delay — it is a defect in the prior stage. The flow:

1. The receiving role names the gap explicitly (the playbook's `Fail Loud` rule applies to every role).
2. Work returns to the owning role for the failed stage.
3. The handoff is re-attempted once the gate is met.

Skipping a gate (`PASS WITH CONDITIONS` accepted without remediation, an ADR-less architectural decision, an undocumented accepted risk) creates debt that surfaces in a later stage — usually in production.

## Loop Back, Don't Skip Forward

The flow is iterative within scope, not linear across the lifecycle:

- A QA finding loops back to Implementation, not forward to Deployment.
- A Security finding may loop back to Architecture, not forward to Operations.
- An SRE post-mortem produces action items that may loop into Implementation, Architecture, or Requirements.

The team is healthy when loop-backs happen at the right gate — not when they bypass it.
