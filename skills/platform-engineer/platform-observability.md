# Skill: platform-observability

**Type:** atomic

## Purpose

Define and measure platform SLOs from the consumer's perspective — what teams experience when using the platform, not just whether the infrastructure is running. A platform SLO that measures uptime but not time-to-first-deploy tells teams nothing about whether the platform is serving them.

## When to Invoke

- A new platform capability is being deployed and needs SLOs before going to production.
- An existing capability has no consumer-perspective SLOs defined.
- Teams are complaining the platform is slow or unreliable but there are no metrics to confirm or deny it.
- Platform SLOs need to be reviewed after a significant infrastructure change.

## Workflow

1. **Define what platform success looks like from the consumer's perspective.** For each platform capability, identify the user-visible outcome: not "the API is responding" but "a team can provision a new environment in under 10 minutes." Write consumer-perspective SLIs (what to measure):
   - **Availability:** Can teams complete the golden path at all?
   - **Latency:** How long does the golden path take?
   - **Error rate:** How often does the golden path fail and require manual intervention?
   - **Adoption:** Are teams using the golden path or working around it?

2. **Set SLO thresholds and error budgets.** For each SLI:
   - What level is acceptable? (e.g., 99% of environment provisions complete in < 10 minutes over a rolling 30-day window)
   - What is the error budget? (e.g., 1% failure rate = ~7 hours of downtime per month)
   - Who is accountable when the SLO is breached?
   Document thresholds before instrumenting — thresholds set after you can see the data are shaped by the data, not by what teams actually need.
   **Gate:** SLO thresholds must be reviewed with at least one consumer team before being set. A threshold the platform team chose unilaterally may not reflect what teams actually need.

3. **Instrument the golden path.** Add measurement at each step of the golden path:
   - Emit an event when the path starts, at each major step, and when it completes or fails.
   - Measure wall-clock time from consumer action to observable outcome — not internal processing time.
   - Capture failure reasons, not just failure counts.

4. **Build dashboards and alerts from the consumer's perspective.** The primary dashboard for a platform capability should show what a team lead would ask: "Is our deployment pipeline healthy? Can new teams onboard today?" Secondary dashboards can show infrastructure-level metrics.
   - Alerts must fire before the SLO is breached, not after.
   - Every alert must have a corresponding runbook or golden path for the platform team to respond.

5. **Review SLOs against actual consumer experience at regular intervals.** An SLO that teams never look at is not improving platform reliability — it is improving platform reporting. Review with a consumer team at each major release and after any SLO breach.

## Output

- **Consumer-perspective SLIs and SLOs** — specific metrics and thresholds for each platform capability, reviewed by consumer teams.
- **Error budgets** — what amount of unreliability is acceptable per period, with named accountable owners.
- **Instrumented golden paths** — measurements from consumer action to observable outcome.
- **Dashboards and alerts** — consumer-perspective primary view, with actionable alerts tied to runbooks.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "Infrastructure uptime covers this" | Uptime measures whether the servers are running. It does not measure whether teams can deploy. These are different things. |
| "Teams would tell us if something was wrong" | Teams adapt. They build workarounds, avoid the flaky part, or ask colleagues instead of using the platform. Metrics surface what complaints don't. |
| "We'll add SLOs once the capability is stable" | SLOs define what "stable" means. Without them, you cannot tell whether the capability is stable or just quiet. |
| "We set the SLO threshold — we know what's acceptable" | Consumer teams know what's acceptable to them. Validate thresholds with the people the platform serves. |

## Red Flags

- SLOs defined only in terms of infrastructure metrics (CPU, memory, disk) with no consumer-perspective metrics
- Thresholds set after observing the data rather than based on consumer requirements
- Alerts that fire only after an SLO is already breached
- No named accountable owner for SLO breaches
- Dashboards that the consumer team cannot read or does not look at
- SLOs never reviewed after being set

## Verification

Before declaring a platform capability production-ready:

- [ ] Consumer-perspective SLIs defined for availability, latency, and error rate
- [ ] SLO thresholds reviewed and approved by at least one consumer team
- [ ] Error budgets calculated and named accountable owners assigned
- [ ] Golden path instrumented — measurement from consumer action to observable outcome
- [ ] Dashboard shows consumer-perspective primary view
- [ ] Alerts fire before SLO breach with runbooks for each alert
- [ ] SLO review schedule set (next review date or trigger)
