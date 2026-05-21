# Skill: capacity-planning

**Type:** atomic

## Purpose

Forecast resource requirements based on growth trends, SLO requirements, and system behaviour under load. Ensures infrastructure is provisioned ahead of need — not in response to it.

## When to Invoke

- A service is growing and the current infrastructure is approaching its limits.
- A planned event (product launch, seasonal peak, marketing campaign) is expected to significantly increase load.
- Infrastructure is being right-sized and current provisioning needs to be validated against actual usage.
- An SLO is being defined and the infrastructure needed to support it needs to be quantified.

## Workflow

1. **Collect current usage data.** For each resource (CPU, memory, connections, storage, throughput):
   - Current utilisation as a percentage of provisioned capacity
   - Utilisation trend over the last 30/60/90 days
   - Peak utilisation and when it occurs (time of day, day of week)
   - Saturation point — the utilisation level at which performance degrades

2. **Model growth.** Extrapolate current trends to the planning horizon (typically 6 and 12 months):
   - Linear growth: constant amount added per period
   - Exponential growth: constant percentage increase per period
   Use the more conservative model unless there is specific evidence for one or the other.

3. **Model planned events.** If a specific event is expected to spike load:
   - Estimate the traffic multiplier (e.g. "2× normal load for 4 hours")
   - Determine whether the spike is predictable enough to pre-scale or requires autoscaling

4. **Determine headroom requirements.** Set the target utilisation ceiling:
   - CPU: operate below 60–70% average to handle spikes
   - Memory: operate below 70–80% to avoid swap and GC pressure
   - Storage: maintain at least 30% free and monitor growth rate
   The gap between target ceiling and projected utilisation is the headroom — when headroom reaches zero, action is required.

5. **Calculate when capacity will be needed.** Based on the growth model and current headroom, determine:
   - When each resource will reach its target ceiling
   - The lead time required to provision additional capacity
   - The date by which a capacity action must be taken

6. **Recommend capacity actions.** For each resource that will exceed its ceiling within the planning horizon:
   - What change is needed (add instances, increase instance size, shard the database, add read replicas)
   - By when it must be done
   - The estimated cost of the change

7. **Define scaling triggers.** For services using autoscaling, define the scaling policies:
   - Scale out when: CPU > X% for Y minutes
   - Scale in when: CPU < X% for Y minutes
   - Minimum instances: N (for availability)
   - Maximum instances: N (for cost control)

## Output

- **Current utilisation summary** — per-resource utilisation and trend
- **Growth model** — projected utilisation at 6 and 12 months
- **Headroom timeline** — when each resource will reach its ceiling
- **Capacity action plan** — what to provision, by when, and estimated cost
- **Scaling policy definitions** — autoscaling triggers and bounds
