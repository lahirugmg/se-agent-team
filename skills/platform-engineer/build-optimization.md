# Skill: build-optimization

**Type:** atomic

## Purpose

Identify and eliminate bottlenecks in build or pipeline execution time. Fast pipelines produce faster feedback and encourage more frequent commits. Slow pipelines produce batched changes and delayed defect detection.

## When to Invoke

- Pipeline execution time has increased to the point where it is slowing down developer workflows.
- A build or test stage is a known bottleneck and optimisation is being prioritised.
- A new pipeline is being designed and baseline performance targets are being established.

## Workflow

1. **Measure before optimising.** Collect current performance data:
   - Total pipeline duration (p50 and p95 over the last 30 days)
   - Duration per stage
   - Cache hit rate per cacheable stage
   - Frequency and impact of flaky stages
   Do not optimise without a baseline. Optimising what you don't measure produces unverifiable improvement.

2. **Identify the critical path.** Map the pipeline's dependency graph. The critical path is the sequence of stages that cannot be parallelised. Optimising a non-critical-path stage produces no improvement in total time.

3. **Parallelise independent stages.** Stages that do not depend on each other's output can run simultaneously. Common candidates: unit tests, linting, type checking, and security scanning.

4. **Optimise caching.** For each stage that runs dependencies or compilation:
   - Cache dependency installs (node_modules, pip packages, Go module cache)
   - Cache build artifacts (compiled binaries, Docker layers)
   - Verify cache keys are correctly scoped — too broad = stale cache, too narrow = cache miss on every run
   - Measure cache hit rate; anything below 80% warrants investigation

5. **Reduce test execution time.** For slow test suites:
   - Identify the slowest tests (run with `--verbose` or equivalent timing output)
   - Split the test suite into shards that run in parallel
   - Move integration tests that require external services to a separate, optional stage
   - Delete or fix tests that are consistently slow and test low-value behaviour

6. **Reduce build artifact size.** Smaller artifacts build faster and transfer faster:
   - For containers: apply multi-stage builds, remove unnecessary layers
   - For compiled artifacts: strip debug symbols in production builds
   - For packaged applications: exclude dev dependencies, documentation, and test files

7. **Fix flaky stages.** A flaky stage that retries adds its full duration to average pipeline time. For each flaky stage, identify whether the flakiness is in the test code, the test environment, or the application under test. Fix the root cause; do not add retries as a workaround.

8. **Set performance targets.** Define acceptable pipeline duration and put a regression check in place:
   - PR pipeline: under 5 minutes
   - Full pipeline: under 15 minutes
   Alert when these targets are breached.

## Output

- **Baseline metrics** — current duration per stage and total
- **Critical path analysis** — the bottleneck sequence
- **Optimisation actions** — what was changed (parallelisation, caching, test splitting, etc.)
- **Post-optimisation metrics** — duration per stage and total after changes
- **Performance targets** — defined acceptable durations with monitoring in place
