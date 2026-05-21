# Skill: estimation

**Type:** atomic

## Purpose

Estimate the effort or complexity of a backlog of work using a consistent, documented method. Produces estimates the team trusts and stakeholders understand, alongside explicit confidence levels and assumptions.

## When to Invoke

- A backlog of stories or epics needs to be sized before planning or roadmapping.
- Stakeholders need a rough timeline for a body of work.
- An existing estimate is being challenged and needs to be revisited with new information.

## Workflow

1. **Choose the estimation unit.** Select the unit appropriate to the scope:
   - **Story points** — relative complexity for sprint-level stories
   - **T-shirt sizes** (XS/S/M/L/XL) — rough effort for roadmap-level epics
   - **Ideal days** — calendar-time equivalent when stakeholders need a schedule
   Document the unit being used and its definitions. Never mix units in the same estimation session.

2. **Establish a reference point.** Pick one well-understood story or epic as an anchor. Calibrate the team's sense of the unit against this anchor before estimating anything else.

3. **Estimate each item.** For each backlog item:
   - Discuss briefly (timebox: 5 minutes per story, 15 for epics)
   - Have estimators give their estimate independently before revealing
   - Where estimates diverge, discuss the reasons — divergence signals different understanding, not different opinions
   - Record the consensus estimate and any dissenting view

4. **Flag uncertainty.** For each estimate, record confidence:
   - **High** — well-understood, similar work done before
   - **Medium** — some unknowns, likely to hold within 50%
   - **Low** — significant unknowns, treat as a spike candidate
   Low-confidence estimates should not be used for commitments without a discovery spike first.

5. **Identify assumptions.** Each estimate rests on assumptions about scope, dependencies, and technical approach. Record the top assumption for any medium or low confidence item.

6. **Aggregate with a buffer.** When rolling up estimates to a timeline, apply a buffer proportional to the uncertainty in the work. A backlog of all High confidence items needs less buffer than one with many Low confidence items.

## Output

- **Estimation table** — each item with estimate, unit, confidence level, and key assumption
- **Aggregate estimate** — total with buffer range and confidence distribution
- **Spike candidates** — items too uncertain to estimate reliably, recommended for discovery first
