# Skill: test-writing

**Type:** atomic

## Purpose

Write test cases or automated tests that verify specific behaviour, encode why that behaviour matters, and fail when the behaviour breaks. A test that passes regardless of the implementation is not a test.

## When to Invoke

- A test plan exists and test cases need to be produced for the planned scope.
- An acceptance criterion needs to be translated into an executable test.
- An existing test suite needs to be extended for a new feature or code path.

## Workflow

1. **Read the acceptance criteria.** Each GIVEN/WHEN/THEN criterion maps to at least one test. Begin there — test writing that doesn't start from requirements produces tests that verify implementation, not intent.

2. **Write tests in GIVEN/WHEN/THEN structure.** Even for automated tests, the test name and body should communicate the precondition, action, and expected outcome:
   - Test name: `returns_error_when_payment_amount_exceeds_limit`
   - Setup: GIVEN a user with a standard account
   - Action: WHEN they submit a payment of $10,001
   - Assertion: THEN the response is HTTP 422 with error code `AMOUNT_EXCEEDS_LIMIT`

3. **Write the happy path first.** The primary success scenario must be covered before edge cases. If the happy path test fails, edge case tests have no baseline.

4. **Cover key error paths.** For each operation, identify:
   - Invalid inputs (type mismatch, out of range, missing required fields)
   - Missing preconditions (unauthenticated, insufficient permissions, resource not found)
   - System failures (downstream service unavailable, timeout, concurrent modification)
   Each error path that has defined behaviour in the spec must have a test.

5. **One assertion per test.** Tests with multiple unrelated assertions are hard to diagnose when they fail. If a test needs to assert multiple things, they should be parts of one coherent behaviour.

6. **Make tests independent.** Each test must be runnable in isolation without depending on the execution order of other tests. Shared state between tests is the most common cause of flaky tests.

7. **Make test failure messages readable.** When a test fails, the failure message should say what was expected and what was received — not just "assertion failed." Use assertion libraries that produce readable diffs.

8. **Do not mock what you can use directly.** Prefer integration tests for code paths where the integration is the risk (e.g. database queries, external API calls in a test environment). Only mock at system boundaries that are too costly or unstable to call in tests.

## Output

- **Test suite** — tests covering all acceptance criteria and key error paths
- **Test coverage summary** — which acceptance criteria are covered and by which tests
- **Test data notes** — what data is assumed, created, or required for the tests to run
