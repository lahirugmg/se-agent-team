# Skill: performance-testing

**Type:** atomic

## Purpose

Design and execute performance tests that verify a system meets defined throughput, latency, and stability targets under realistic and peak load conditions. Performance testing without a baseline and a target is not testing — it is profiling.

## When to Invoke

- A performance target has been defined and needs to be verified before release.
- A change has been made to a performance-critical path and regression must be ruled out.
- A system is experiencing performance problems in production and the cause needs to be isolated.
- A capacity estimate needs empirical validation before infrastructure is provisioned.

## Workflow

1. **Define targets.** Performance testing must verify against specific, agreed targets. Collect or define:
   - **Throughput target** — requests per second or transactions per second at peak load
   - **Latency targets** — p50, p95, p99 response time under load
   - **Error rate target** — acceptable error rate under peak load (typically <1%)
   - **Stability target** — behaviour over sustained load (e.g. no memory leak over 1 hour at peak)
   If targets don't exist, establish a baseline first, then set targets relative to it.

2. **Identify the scope.** Which endpoints, flows, or operations will be tested? Focus on: user-facing critical paths, operations with known heavy computation or I/O, and any new or changed code on hot paths.

3. **Prepare realistic load profiles.** Real traffic is not uniform. Model at least three scenarios:
   - **Baseline** — normal expected load
   - **Peak** — expected maximum load (e.g. 2× baseline, or known seasonal peaks)
   - **Stress** — load beyond expected peak to find the breaking point
   Use production traffic patterns as the basis for the request distribution.

4. **Set up the test environment.** The test environment must match production in the dimensions being tested (CPU, memory, database size, network topology). A performance test on an undersized environment produces meaningless results.

5. **Execute and instrument.** Run each load scenario and collect:
   - Response time distributions (p50, p95, p99, max)
   - Throughput (requests/second)
   - Error rate
   - System resource utilisation (CPU, memory, I/O, connections)
   Identify the point at which performance degrades and the nature of the degradation.

6. **Compare against targets.** For each target, state explicitly: PASS or FAIL. Do not interpret performance results — measure them against the agreed target.

7. **Identify bottlenecks.** For any FAIL, identify where the bottleneck is: application code, database query, network, connection pool, external dependency. Provide enough data for an engineer to act on.

## Output

- **Test scenarios** — baseline, peak, stress with load profiles
- **Results table** — p50/p95/p99 latency, throughput, error rate for each scenario
- **Target comparison** — explicit PASS/FAIL for each defined target
- **Bottleneck analysis** — where performance degrades and what the limiting resource is
- **Recommendations** — specific changes to address any FAILs
