# Skill: build-platform

**Type:** composite
**Trigger:** Take a platform end-to-end from developer-contract design to self-served deployment
**Sub-skills:** idp-design → golden-path → infrastructure-as-code → containerization → pipeline-design → deployment → platform-observability
**Phases:** Pre-work: idp-design, golden-path | Execution: infrastructure-as-code, containerization, pipeline-design, build-optimization | Post-work: deployment, platform-observability

## Purpose

End-to-end workflow for delivering a new or significantly updated internal developer platform capability. Covers the developer contract design, infrastructure, container standards, CI/CD systems, deployment, and verification that teams can self-serve — in that order.

## When to Invoke

- A new platform capability is being introduced (new golden path, new environment type, new shared pipeline).
- An existing platform component is being significantly redesigned.
- The platform is being extended to serve a new team or workload type.

## Workflow

### Step 1 — IDP Design · Pre-work (@idp-design)

Before writing any infrastructure code:

1. Run the idp-design skill: define the platform capability's scope, the developer-facing interface, and the self-service boundary.
2. Identify which teams will use this capability and what they currently do instead.
3. Document what is on the golden path and what is explicitly off it.

**Gate:** The developer contract — what teams interact with, what is internal — is documented and reviewed by at least one representative of the teams that will use it. Do not build until this review is complete.

### Step 2 — Golden Path · Pre-work (@golden-path)

With the developer contract defined:

1. Run the golden-path skill: design the opinionated, supported workflow teams will follow.
2. The path must be completable by a team without platform team intervention.
3. Write the path documentation and validate it against the actual implementation plan — not against the ideal.

**Gate:** The golden path documentation exists and has been walked through by someone who did not write it. Do not build infrastructure until the path is validated.

### Step 3 — Infrastructure as Code · Execution (@infrastructure-as-code)

With the design agreed:

1. Run the infrastructure-as-code skill: write all platform infrastructure definitions in version control.
2. All compute, networking, storage, and secrets management must be in code.
3. Run `plan` or `diff` and review before applying. Infrastructure drift must be zero.

**Gate:** IaC reviewed, planned, and applied successfully to a non-production environment.

### Step 4 — Containerization · Execution (@containerization)

Where container standards are part of the platform capability:

1. Run the containerization skill: write or review the base image definitions, Dockerfile standards, and orchestration config the platform provides to teams.
2. Standards must be minimal, non-root, and pinned to specific digests.

**Gate:** Any container artifact the platform provides builds cleanly and the reference service starts inside it.

### Step 5 — Pipeline Design · Execution (@pipeline-design)

For CI/CD capabilities:

1. Run the pipeline-design skill: design or update the shared pipeline templates, triggers, and promotion model teams will use.
2. Pipeline definitions must be version-controlled alongside the platform code they build.
3. Fail explicitly on error — no silent skips.

**Gate:** A reference pipeline run completes successfully through all stages using the new design.

### Step 6 — Deployment · Post-work (@deployment)

With the platform capability built:

1. Run the deployment skill: release the platform change with a documented rollback plan.
2. Identify all teams and services affected. Communicate before deploying.
3. Monitor through a soak period. Do not declare complete until metrics are stable.

**Gate:** Post-deploy metrics within normal bounds for the full soak period. Affected teams notified before and after.

### Step 7 — Platform Observability · Post-work (@platform-observability)

After deployment:

1. Run the platform-observability skill: define or update the SLOs for this platform capability from the consumer's perspective.
2. Confirm teams can complete the golden path end-to-end without platform team intervention.
3. Set up alerts on platform SLO breach — not just on infrastructure uptime.

**Gate:** At least one team has successfully completed the golden path end-to-end without platform team involvement. SLOs are defined and alerts are active.

## Output

A platform capability package containing:

- **Developer contract** — what teams interact with, what is internal, what is on and off the golden path
- **Golden path documentation** — the supported, validated workflow teams follow
- **Infrastructure code** — all platform resources in version control, applied to production
- **Deployment record** — what changed, when, who was notified, with rollback procedure
- **Platform SLOs** — consumer-perspective metrics with active alerts
- **Self-serve verification** — evidence that at least one team completed the golden path without assistance

This package is the handoff artifact confirming the platform capability is production-ready.
