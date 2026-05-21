# Skill: pipeline-design

**Type:** atomic

## Purpose

Design or refactor a CI/CD pipeline that makes the path from committed code to production fast, reliable, and safe. A well-designed pipeline enforces quality gates, minimises feedback time, and makes bad changes impossible to ship accidentally.

## When to Invoke

- A new service or repository needs a CI/CD pipeline for the first time.
- An existing pipeline is slow, flaky, or failing to catch defects before production.
- A delivery process is being redesigned to support a new deployment model (e.g. moving to containers, GitOps, or trunk-based development).

## Workflow

1. **Understand the delivery requirements.** Collect:
   - What triggers a pipeline run? (push, PR, tag, schedule)
   - What environments exist? (dev, staging, production, canary)
   - What is the promotion model? (auto-deploy to staging; manual gate to production)
   - What are the SLAs? (how fast must a commit reach production?)
   - What quality gates are required? (tests, coverage, security scans, approvals)

2. **Define pipeline stages.** Map the stages from commit to production:
   - **Build** — compile, lint, type-check
   - **Test** — unit, integration, contract tests
   - **Security** — SAST, dependency scan, secrets detection
   - **Package** — produce the deployable artifact (container image, binary, archive)
   - **Deploy to staging** — deploy and run smoke tests
   - **Deploy to production** — deploy with health checks, rollback trigger
   Each stage must have a clear pass/fail condition. A stage that always passes is not a gate.

3. **Minimise pipeline time.** Parallelise independent stages. Cache dependencies, build layers, and test results. Run fast tests before slow ones. Target: PR feedback in under 5 minutes; full pipeline under 15 minutes.

4. **Design for reliability.** A flaky pipeline is worse than a slow one — it trains developers to ignore failures. Design to avoid flakiness:
   - Isolate tests from shared state
   - Use deterministic build inputs (lockfiles, pinned base images)
   - Set realistic timeouts on all stages

5. **Design the artifact model.** Define what artifact is produced, how it is versioned, and where it is stored. The same artifact must be promoted through environments — building separately for each environment is a defect.

6. **Define the rollback model.** For each deployment stage, define: what triggers a rollback, how the rollback is executed, and how long the rollback window lasts.

7. **Define secrets handling.** Secrets must be injected at runtime via the CI/CD platform's secret management — never stored in repository files or pipeline logs.

## Output

- **Pipeline diagram** — stages, triggers, gates, and environment flow
- **Stage definitions** — what each stage does, its inputs, outputs, and pass/fail criteria
- **Timing targets** — expected duration per stage and total
- **Artifact model** — what is produced, how it is versioned, where it is stored
- **Rollback model** — trigger, execution, and window for each deployment stage
- **Secrets handling plan** — how secrets are injected at each stage
