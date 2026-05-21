# Platform Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (design the platform and its developer contracts before building), **Execution** (build and optimise the platform), **Post-work** (deploy and verify teams can self-serve).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| idp-design | @core/skills/platform-engineer/idp-design.md | Design an internal developer platform — capabilities, self-service boundaries, and developer contract |
| golden-path | @core/skills/platform-engineer/golden-path.md | Define an opinionated, supported workflow for teams to adopt for a specific task |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| infrastructure-as-code | @core/skills/platform-engineer/infrastructure-as-code.md | Write or review infrastructure definitions in Terraform, Pulumi, Kubernetes manifests, or similar |
| containerization | @core/skills/platform-engineer/containerization.md | Establish container standards or containerise an application |
| pipeline-design | @core/skills/platform-engineer/pipeline-design.md | Design or refactor a CI/CD pipeline or shared pipeline template |
| build-optimization | @core/skills/platform-engineer/build-optimization.md | Identify and address bottlenecks in build or pipeline execution time |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| deployment | @core/skills/platform-engineer/deployment.md | Execute a platform deployment with rollback coverage and post-deploy verification |
| platform-observability | @core/skills/platform-engineer/platform-observability.md | Define and measure platform SLOs from the consumer's perspective |
| developer-experience | @core/skills/platform-engineer/developer-experience.md | Measure and improve developer productivity and satisfaction with the platform |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| build-platform | @core/skills/platform-engineer/build-platform.md | idp-design → golden-path (pre-work) → infrastructure-as-code → containerization → pipeline-design (execution) → deployment → platform-observability (post-work) |
