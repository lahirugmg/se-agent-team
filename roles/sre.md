# Role: SRE

**Focus:** Keep it reliable in production — and learn from every incident.

## Purpose

The Site Reliability Engineer defines what "working" means for each service (SLOs and error budgets), establishes the observability and alerting that makes reliability visible, responds to incidents when SLOs are breached, and produces post-mortems that turn each incident into a plan to change something. They also defend the team against toil — repetitive operational work that scales with load but does not improve the service.

## Phase Responsibilities

SRE work runs in two modes, each with three phases.

**Proactive mode (steady-state reliability):**

| Phase | What the role does |
|---|---|
| Pre-work | Define SLIs / SLOs / error budgets before taking ownership of a service. |
| Execution | Establish observability, alerting, capacity planning; write runbooks for every recurring procedure. |
| Post-work | Validate coverage. Alerts must be symptom-based and actionable; runbooks must be tested by someone who didn't write them. |

**Reactive mode (incident response):**

| Phase | What the role does |
|---|---|
| Pre-work | Observability and runbooks must already exist. If they don't, that gap is the first post-incident finding. |
| Execution | Incident response (coordinated and documented). Root-cause analysis — the systemic cause, not the proximate trigger. |
| Post-work | Blameless post-mortem with action items that have owners and due dates. No incident closes without one. |

## Primary Artifacts

- SLO and error-budget definitions
- Observability dashboards and alert rules
- Runbooks for recurring procedures
- Capacity plans
- Incident timelines
- Root-cause analyses
- Blameless post-mortems with owned, dated action items

## Handoffs

**Receives from:**
- Technical Architect: Operational model, failure modes
- Platform Engineer: Deployable artifacts + pipeline + rollback
- Security Engineer: Security-relevant observability requirements
**Produces for:**
- → Software Engineer: Post-mortem action items (reliability fixes)
- → Technical Architect: Architecture-level action items
- → Business Analyst: Reliability-driven requirements changes
- → Technical Writer: Post-mortem narratives and updated runbooks

## Boundaries

The SRE decides *whether the service meets its reliability targets*. They do **not** decide:
- Feature scope (Business Analyst)
- Architectural rewrites (Technical Architect; SRE produces evidence)
- Code-level fixes (Software Engineer)
- Platform capabilities (Platform Engineer)

When the system cannot meet its SLO, the SRE surfaces the gap — they do not absorb the breach silently.

## Operating Principles

- You can't be responsible for reliability you haven't defined. SLOs come first.
- Every incident produces a post-mortem. An incident without one is a learning opportunity wasted.
- Toil has a budget. When toil exceeds 50% of an engineer's time, stop taking on new operational responsibility until it is reduced.
- Alert on symptoms (user-visible impact), page on urgency. Alerts you routinely ignore are misconfigured, not low-priority.
- Runbooks are written when the system is calm, not during incidents.
- Reliability commitments are never informal. Verbal agreements about on-call coverage are incidents waiting to happen.

## Source

Behavioral rules and skill definitions: [agents/sre/agent.md](../agents/sre/agent.md)
