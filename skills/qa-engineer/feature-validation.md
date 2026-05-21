# Skill: feature-validation

**Type:** composite
**Sub-skills:** test-planning → test-writing → exploratory-testing → bug-report
**Phases:** Pre-work: test-planning | Execution: test-writing, exploratory-testing | Post-work: bug-report

## Purpose

End-to-end validation workflow for a feature or change before it ships. Covers planned testing (what we know to test), written tests (automated or manual), and exploratory testing (what we didn't think to test). Any defects found are reported in a structured, actionable format.

## When to Invoke

- A feature has been implemented and is ready for QA sign-off before release.
- A significant change needs structured validation before it merges.
- A regression needs to be ruled out after a large refactor or dependency update.

## Workflow

### Step 1 — Test Planning · Pre-work (@test-planning)

Before any tests are written or run:

1. Read the PRD, user stories, and acceptance criteria for the feature.
2. Run the test-planning skill: define scope, approach, coverage targets, and entry/exit criteria.
3. Identify risk areas — places where failure would have high impact — and weight coverage there.

**Gate:** A test plan exists with explicit in-scope and out-of-scope boundaries. Do not begin writing tests without one.

### Step 2 — Test Writing · Execution (@test-writing)

With the plan approved:

1. Run the test-writing skill to produce test cases or automated tests for each acceptance criterion.
2. Each test must encode WHY the behaviour matters, not just WHAT it does.
3. Tests that cannot fail when the relevant behaviour breaks are not tests — rewrite or discard them.

**Gate:** All acceptance criteria from the PRD have at least one corresponding test. Tests are passing on the implementation under review.

### Step 3 — Exploratory Testing · Execution (@exploratory-testing)

After planned tests pass:

1. Run the exploratory-testing skill with a time-boxed charter focused on edge cases and risk areas not covered by the plan.
2. Do not re-run planned tests — explore outside the spec.
3. Document findings as you go. Anything that looks wrong gets a bug report in Step 4.

**Gate:** The exploratory charter is complete. All blocking findings are documented.

### Step 4 — Bug Reporting · Post-work (@bug-report)

For every defect found in Steps 2 or 3:

1. Run the bug-report skill for each distinct defect.
2. Each report must include: reproduction steps, expected behaviour, actual behaviour, environment, and severity.
3. Link each bug report to the relevant acceptance criterion or exploratory charter finding.

## Output

A validation package containing:

- **Test plan** — scope, approach, coverage targets, risk areas, entry/exit criteria
- **Test suite** — automated or manual tests covering all acceptance criteria
- **Exploratory testing notes** — charter, findings, and time spent
- **Bug reports** — one per defect found, with severity and reproduction steps
- **Sign-off verdict** — PASS (ready to ship), PASS WITH CONDITIONS (minor bugs, shippable with workaround), or FAIL (blocking defects, do not ship)

This package is the handoff artifact for the Security Engineer to begin security review, or for the release decision if no security review is required.
