# Skill: test-planning

**Type:** atomic

## Purpose

Define the scope, approach, coverage targets, and entry/exit criteria for a testing effort before any tests are written or executed. A test plan is the difference between structured verification and ad hoc checking.

## When to Invoke

- A feature or change is ready for testing and the scope has not been defined.
- A release is approaching and the team needs to agree on what "done" means for QA.
- A large or risky change needs a risk-based testing strategy before resources are committed.

## Workflow

1. **Read the requirements.** Collect the PRD, user stories, and acceptance criteria. Identify every behaviour that was specified — these form the baseline for planned tests.

2. **Define the scope.** Explicitly state:
   - **In scope** — what will be tested in this effort
   - **Out of scope** — what will not be tested and why (not covered by this change, tested elsewhere, deferred)
   Scope boundaries prevent scope creep during execution and set honest expectations.

3. **Identify risk areas.** Not all features carry equal risk. Assess each area by:
   - **Impact** — how bad is a failure here? (user-facing, financial, data integrity, security)
   - **Likelihood** — how likely is a defect here? (complex logic, new code, integration points)
   Rank risk areas. High-risk areas get deeper coverage; low-risk areas get lighter coverage.

4. **Define the testing approach.** For each scope area, specify:
   - Test level: unit, integration, system, end-to-end
   - Test type: functional, non-functional (performance, security, accessibility), regression
   - Execution method: automated or manual
   Match the approach to the risk level — automated regression for stable, high-risk paths; exploratory for edge cases.

5. **Define coverage targets.** Coverage targets must be specific and measurable:
   - "All acceptance criteria covered by at least one automated test"
   - "Happy path and top 3 error paths covered for the payment flow"
   - "Load test to 2× expected peak throughput"
   Vague targets ("good coverage") cannot be verified.

6. **Define entry and exit criteria.**
   - **Entry** — conditions that must be true before testing begins (e.g. build passing, test environment stable, test data loaded)
   - **Exit** — conditions that define completion (e.g. all planned tests executed, no open Critical or High bugs, coverage targets met)

7. **Identify test data and environment requirements.** What environments, configurations, and data sets are needed? Who is responsible for providing them?

## Output

- **Test scope** — explicit in-scope and out-of-scope list
- **Risk-based coverage plan** — areas ranked by risk with corresponding depth of coverage
- **Testing approach** — levels, types, and execution methods per scope area
- **Coverage targets** — specific and measurable
- **Entry and exit criteria**
- **Environment and data requirements**
