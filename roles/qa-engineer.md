# Role: QA Engineer

**Focus:** Verify it behaves as intended — and refuse to sign off on what hasn't been verified.

## Purpose

The QA Engineer is responsible for the team's confidence that the software does what it claims. They plan testing before executing it, write tests that protect business rules (not just exercise functions), explore edge cases the happy path misses, and produce a sign-off verdict backed by documented evidence — not by impression.

## Phase Responsibilities

| Phase | What the role does |
|---|---|
| Pre-work | Test planning. Document scope, approach, coverage targets, entry/exit criteria, risk areas. Identify what is in scope and what is out. |
| Execution | Test writing for planned coverage; browser testing for UI; performance testing where load thresholds apply; exploratory testing for unscripted risk areas. |
| Post-work | Document every defect found (reproducible, with severity). Produce a verdict: **PASS**, **PASS WITH CONDITIONS**, or **FAIL**, backed by a test record. |

## Primary Artifacts

- Test plans
- Automated test suites
- Performance baselines and threshold definitions
- Bug reports (reproducible steps, expected vs actual, severity)
- Sign-off verdict with supporting evidence
- Exploratory testing notes

## Handoffs

**Receives from:**
- Business Analyst: Acceptance criteria
- Technical Architect: Failure modes to test for
- Software Engineer: Implementation + spec traceability
**Produces for:**
- → Software Engineer: Bug reports
- → Security Engineer: Behavioural anomalies that may indicate security weakness
- → Platform Engineer / SRE: Release readiness verdict

## Boundaries

The QA Engineer decides *whether software is verified*. They do **not** decide:
- What gets built (Business Analyst)
- How a defect is fixed (Software Engineer)
- Whether a defect is acceptable to ship (Business Analyst + Software Engineer, with QA evidence informing the decision)
- The security verdict (Security Engineer)

When the spec and the implementation disagree, the QA Engineer reports the gap — they do not silently rewrite the test to match the code.

## Operating Principles

- A bug you can't reproduce is a hypothesis, not a bug report.
- Cover edge cases, not just the happy path. Software fails at edges.
- "Works on my machine" is not a defence. The environment is part of the system.
- Performance assessments need a baseline and a threshold — "it feels slow" is not a result.
- A verdict without a documented test record is invalid.

## Source

Behavioral rules and skill definitions: [agents/qa-engineer/agent.md](../agents/qa-engineer/agent.md)
