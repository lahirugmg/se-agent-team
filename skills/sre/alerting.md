# Skill: alerting

**Type:** atomic

## Purpose

Define or tune alerts so that they are symptom-based, actionable, correctly calibrated, and paged to the right person at the right time. An alert that fires and is ignored is worse than no alert — it trains operators to ignore alerts.

## When to Invoke

- A new service is being deployed and needs alerting from the start.
- Existing alerts are too noisy (too many pages, too many false positives).
- An incident occurred with no alert — a gap needs to be closed.
- An alert fired for something that was not actionable — it needs to be retuned or removed.

## Workflow

1. **Alert on symptoms, not causes.** A symptom is something the user experiences (high latency, errors, unavailability). A cause is an internal state (high CPU, low memory, slow query). Alert on symptoms. Let dashboards and runbooks guide operators to causes.
   - Good: "p99 latency > 2s for 5 minutes"
   - Bad: "CPU utilisation > 80% for 5 minutes"

2. **Define the SLO-based alert set.** For each SLO:
   - **Burn rate alert** — how fast is the error budget being consumed? Alert at 2× and 5× the expected burn rate. Fast burn = page immediately; slow burn = ticket.
   - This produces exactly two alerts per SLO: a short-window high-sensitivity alert and a long-window high-specificity alert.

3. **Define the alert properties.** For each alert:
   - **Condition** — the specific metric query and threshold
   - **Window** — how long the condition must hold before firing (avoids spikes triggering pages)
   - **Severity** — Page (wake someone up) / Ticket (fix during business hours) / Informational (log only)
   - **Runbook link** — the URL of the runbook for this specific alert
   - **Owner** — which team or rotation receives this alert

4. **Tune thresholds.** Set thresholds based on observed production behaviour — not on arbitrary numbers:
   - Run the alert query against historical data to see how often it would have fired
   - Target: a Page alert fires fewer than 2 times per on-call shift on average
   - If the threshold produces too many alerts in back-testing, raise it or lengthen the window

5. **Test the alert.** Verify the alert fires correctly:
   - Simulate the condition in a non-production environment if possible
   - Verify the alert reaches the intended recipient (notification routing)
   - Verify the runbook link is correct and the runbook is actionable

6. **Audit existing alerts.** For each existing alert that has not fired in the last 90 days: assess whether it should be removed, retuned, or kept. Alerts that never fire are either broken or unnecessary.

## Output

- **Alert inventory** — all alerts with condition, window, severity, owner, and runbook link
- **SLO alert set** — the burn rate alerts derived from each SLO
- **Threshold rationale** — how thresholds were determined (back-testing results)
- **Routing map** — which alert goes to which team/rotation and via which channel
- **Audit results** — assessment of existing alerts (keep / retune / remove)
