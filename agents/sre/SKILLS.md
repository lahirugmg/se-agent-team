# SRE — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (establish observability and runbooks before incidents occur), **Execution** (respond to and investigate an incident), **Post-work** (document findings and drive systemic improvement).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| observability | @core/skills/sre/observability.md | Design or improve the metrics, logging, and tracing for a service |
| alerting | @core/skills/sre/alerting.md | Define or tune alerts to be symptom-based, actionable, and correctly calibrated |
| capacity-planning | @core/skills/sre/capacity-planning.md | Forecast resource needs based on growth trends and SLO requirements |
| runbook | @core/skills/sre/runbook.md | Write or update an operational runbook for a recurring procedure |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| incident-response | @core/skills/sre/incident-response.md | Coordinate and document the response to an active incident |
| root-cause-analysis | @core/skills/sre/root-cause-analysis.md | Investigate and document the root cause of a failure or degradation |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| post-mortem | @core/skills/sre/post-mortem.md | Produce a blameless post-mortem with timeline, root cause, and action items |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| incident-to-action | @core/skills/sre/incident-to-action.md | incident-response → root-cause-analysis (execution) → post-mortem (post-work; observability and runbooks are pre-work established in advance) |
