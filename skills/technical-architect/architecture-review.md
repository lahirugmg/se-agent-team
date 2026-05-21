# Skill: architecture-review

**Type:** atomic

## Purpose

Review an existing or proposed architecture against its requirements, stated principles, and constraints. Identify gaps, risks, and violations before they become expensive to fix. Produce a structured finding set with recommendations, not just a list of concerns.

## When to Invoke

- A proposed architecture needs review before implementation begins.
- An existing architecture is being evaluated for a change, extension, or problem diagnosis.
- A periodic architectural health check is being conducted.

## Workflow

1. **Gather context.** Collect: the architecture document or diagram, the requirements it was designed to satisfy, the constraints it was designed within, and any ADRs recording past decisions. Do not review architecture without knowing what it was trying to achieve.

2. **Review against requirements.** For each functional and non-functional requirement, assess:
   - Does the architecture satisfy it?
   - Is the satisfaction explicit and traceable, or assumed?
   - Are there requirement gaps (things the architecture doesn't address)?

3. **Review structural integrity.** Assess the design against core architectural principles:
   - **Single responsibility** — do components have clear, bounded roles?
   - **Loose coupling** — can components change independently?
   - **High cohesion** — is related behaviour co-located?
   - **Explicit dependencies** — are dependencies named and justified?
   Flag any component that is doing too much, knows too much about its neighbours, or is being called in a way that bypasses its intended interface.

4. **Review for operational readiness.** Assess:
   - Observability — can the system be monitored and debugged in production?
   - Deployability — can components be deployed independently?
   - Rollback — can a bad deployment be reversed without data loss?
   - Scalability — are there obvious bottlenecks under load?

5. **Review for security.** Identify trust boundaries and assess whether they are enforced. Check: authentication at every external entry point, authorisation before sensitive operations, data in transit and at rest, secret handling.

6. **Identify risks.** For each concern found, assess severity:
   - **Blocking** — the architecture cannot meet its requirements as designed
   - **High** — significant risk of failure or future cost; should be addressed before implementation
   - **Medium** — will cause friction or tech debt; address in next design iteration
   - **Low** — worth noting; address opportunistically

7. **Produce recommendations.** For each High and Blocking finding, propose a specific remediation — not just "fix this." Recommendations must be concrete enough to act on.

## Output

- **Review summary** — overall assessment and verdict (Approved / Approved with conditions / Blocked)
- **Finding set** — each finding with severity, description, and recommendation
- **Requirements traceability** — which requirements are satisfied, partially satisfied, or missing
- **Approved elements** — what is explicitly confirmed as sound, so reviewees know what to keep
