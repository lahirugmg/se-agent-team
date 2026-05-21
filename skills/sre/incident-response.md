# Skill: incident-response

**Type:** atomic

## Purpose

Coordinate and document the response to an active incident: triage its severity, establish communication, drive mitigation, and maintain a real-time record. The goal is the fastest path to restoring service — not to finding the root cause during the incident.

## When to Invoke

- An alert has fired and the severity is not yet known.
- A service is degraded or unavailable and the response needs to be coordinated.
- An incident is in progress and needs a structured approach to drive it to resolution.

## Workflow

1. **Triage severity.** Classify the incident immediately using a consistent scale:
   - **SEV1** — complete service outage or data loss; immediate page to all relevant on-call
   - **SEV2** — significant degradation, major feature broken, or high business impact
   - **SEV3** — partial degradation, workaround available, low user impact
   Severity determines who is involved and how urgently. Do not under-classify to avoid disturbing people — an under-classified SEV1 wastes critical time.

2. **Establish the incident channel.** Create a dedicated communication channel (Slack channel, Zoom bridge, or equivalent). All incident communication happens there — not in DMs, not in the original alert thread. Announce the channel to relevant stakeholders.

3. **Assign roles.** For SEV1 and SEV2 incidents:
   - **Incident commander** — owns the response process; keeps people focused; makes decisions when there is disagreement
   - **Technical lead** — drives the technical investigation and mitigation
   - **Communications lead** — manages stakeholder updates and external communication
   One person can hold multiple roles for lower-severity incidents.

4. **Communicate status proactively.** Update stakeholders at regular intervals even if there is nothing new to report:
   - SEV1: every 10–15 minutes
   - SEV2: every 30 minutes
   - Template: "Update [HH:MM]: [What we know] | [What we're doing] | [Next update at HH:MM]"

5. **Drive mitigation, not diagnosis.** During an active incident, prioritise restoring service over understanding the cause:
   - Rollback if the change is recent and rollback is available
   - Increase capacity if the problem is resource exhaustion
   - Disable the failing feature flag or circuit-break the failing dependency
   Root cause analysis happens after service is restored.

6. **Maintain the incident timeline.** Log actions, observations, and decisions in real time with timestamps. This is the source of truth for the post-mortem. Do not reconstruct from memory afterwards.

7. **Declare resolution.** The incident is resolved when:
   - The service is operating within normal bounds for a defined stabilisation period
   - The immediate risk of recurrence is contained (not necessarily eliminated)
   - Relevant stakeholders have been notified of resolution
   Document the resolution time and the mitigation action that resolved it.

## Output

- **Incident record** — severity, affected services, timeline of actions and observations
- **Mitigation summary** — what was done to restore service
- **Stakeholder communications log** — all status updates sent during the incident
- **Resolution declaration** — when resolved, what was confirmed, and by whom
- **Handoff to RCA** — summary of what is known and what needs investigation
