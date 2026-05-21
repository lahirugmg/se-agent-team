# Skill: post-mortem

**Type:** atomic

## Purpose

Produce a blameless post-mortem that documents what happened, why it happened, and what will be done to prevent recurrence. A post-mortem is not a retrospective — it is a permanent record that drives systemic improvement.

## When to Invoke

- An incident has been resolved and the post-mortem is due (typically within 48–72 hours of resolution).
- A near-miss occurred that, with slightly different conditions, would have been a significant incident.
- A recurring type of incident warrants a structured analysis even if individual instances were minor.

## Workflow

1. **Schedule promptly.** Conduct the post-mortem while the incident is fresh — within 48 hours for SEV1, within one week for SEV2. Post-mortems written from memory weeks later are reconstructions, not records.

2. **Establish blamelessness.** The post-mortem analyses systems, processes, and decisions — not individuals. The question is never "who made the mistake?" but "what conditions made the mistake possible?" If blame enters the conversation, redirect to systemic causes.

3. **Reconstruct the timeline.** Using the incident record, logs, and participant recollection, build a chronological timeline from the first indication of the problem to resolution. Include:
   - When the problem started (even if it preceded the alert)
   - When each alert fired
   - Each action taken and by whom (role, not name)
   - When each mitigation was applied and its effect
   - When the incident was declared resolved

4. **Summarise the impact.** Quantify:
   - Duration of impact
   - Users or services affected (how many, what percentage)
   - Data affected (if any)
   - Business impact (transactions lost, SLO budget consumed, contractual impact)

5. **Identify the root cause.** Use 5 Whys or equivalent to reach the systemic cause behind the proximate trigger. The root cause is the condition that, if changed, would prevent this class of incident — not just this specific event. "Human error" is never a root cause — go deeper.

6. **Identify contributing factors.** Conditions that made the incident worse or harder to detect, but are not the root cause. Examples: insufficient monitoring, unclear runbook, delayed alert escalation.

7. **Define action items.** For each root cause and contributing factor, define a specific, ownable action:
   - What will be done
   - Who owns it
   - Target date
   Enter each action into the issue tracker before the post-mortem is published. Untracked actions do not get done.

8. **Review and publish.** Share the draft with incident participants for corrections. Publish to the team within the agreed timeframe. Post-mortems that are kept private cannot improve team or organisational practices.

## Output

- **Timeline** — chronological record from first signal to resolution
- **Impact summary** — duration, affected users/services, business impact
- **Root cause** — the systemic cause, reached via 5 Whys
- **Contributing factors** — conditions that amplified the incident
- **Action items** — specific, owned, dated, entered in the issue tracker
- **Detection and response gaps** — what would have caught this sooner or resolved it faster
