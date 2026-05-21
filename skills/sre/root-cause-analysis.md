# Skill: root-cause-analysis

**Type:** atomic

## Purpose

Investigate and document the root cause of a failure, degradation, or recurring problem at a level specific enough to drive a preventive action. Root cause analysis is complete when the identified cause, if changed, would prevent this class of problem — not just this instance.

## When to Invoke

- A resolved incident requires a root cause before the post-mortem can be written.
- A problem is recurring and the surface-level fixes are not preventing recurrence.
- An anomaly has been detected that did not cause an incident but needs to be understood.

## Workflow

1. **Gather evidence.** Collect all available information about the problem:
   - Incident timeline and actions taken
   - Relevant logs from the affected time window
   - Metrics showing anomalous behaviour
   - Recent changes (deployments, configuration changes, dependency updates, traffic changes)
   - Previous occurrences of similar problems
   Work from evidence, not from assumptions.

2. **Establish the timeline.** Reconstruct a chronological sequence:
   - When did the problem start? (This may predate the first alert)
   - What changed immediately before the problem started?
   - How did the problem propagate across services?
   - What actions were taken and what was their effect?
   Each timeline event must have evidence — log lines, metric readings, deployment records.

3. **Identify the proximate cause.** The proximate cause is the immediate trigger: the specific action or event that directly caused the failure. It is often a recent change, a resource exhaustion event, or an external dependency failure.

4. **Apply 5 Whys.** Starting from the proximate cause, ask "Why did this happen?" at each level until you reach a systemic cause:
   ```
   The service was slow. Why?
   → The database query was slow. Why?
   → A new index was missing. Why?
   → The migration was incomplete. Why?
   → There was no test for query performance after migration. Why?
   → The team has no standard for performance regression testing on schema changes.
   ```
   Stop when further "why" questions lead to factors outside the team's control or to fundamental human limitations.

5. **Distinguish root cause from contributing factors.** The root cause is the single systemic condition that, if changed, prevents the class of problem. Contributing factors made the incident worse or harder to detect but are not sufficient on their own.

6. **Validate the root cause.** The identified root cause must:
   - Explain the observed behaviour fully — no unexplained residuals
   - Be specific enough to drive a concrete preventive action
   - Not be "human error" — human error is a symptom, not a cause

7. **Define the preventive action.** For the root cause, define a specific change that would prevent recurrence. The preventive action must be actionable by the team and verifiable as done.

## Output

- **Evidence summary** — logs, metrics, and change records used in the investigation
- **Timeline** — chronological sequence from start of problem to resolution
- **Proximate cause** — the immediate trigger
- **5 Whys chain** — the full chain from symptom to root cause
- **Root cause statement** — one or two sentences naming the systemic cause
- **Contributing factors** — conditions that amplified the incident
- **Preventive action** — the specific change that would prevent recurrence
