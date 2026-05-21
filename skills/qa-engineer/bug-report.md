# Skill: bug-report

**Type:** atomic

## Purpose

Produce a well-formed bug report that gives a developer everything they need to reproduce, understand, and fix a defect — without asking for clarification. A bug report is a communication artifact; its quality determines how quickly the defect is fixed.

## When to Invoke

- A defect has been found during testing, exploratory testing, or production monitoring.
- An existing bug report is too vague or incomplete to act on.
- A user has reported a problem that needs to be translated into a structured report.

## Workflow

1. **Reproduce the defect.** Before writing anything, confirm you can reproduce the defect consistently. A defect that cannot be reproduced cannot be fixed. If reproduction is intermittent, document the reproduction rate and the conditions under which it occurs.

2. **Isolate the defect.** Find the minimal set of steps that triggers it. Remove any steps that are not necessary. A simpler reproduction path is faster to diagnose and confirm as fixed.

3. **Write the title.** One sentence that names the defect without mentioning the steps or the fix:
   - Good: "Payment confirmation email not sent when order amount is zero"
   - Bad: "Bug in email system" or "Fix the checkout"

4. **Write reproduction steps.** Numbered list. Each step is a single, specific action. Include:
   - Starting state (environment, user role, data state)
   - Each action taken in sequence
   - The result at each step that deviates from expected behaviour

5. **State expected vs. actual behaviour.**
   - **Expected:** what should happen according to the spec or reasonable user expectation
   - **Actual:** what actually happens
   These two fields are the core of the report — everything else supports them.

6. **Capture evidence.** Attach screenshots, screen recordings, logs, or network traces that demonstrate the defect. Evidence reduces back-and-forth and makes the report self-contained.

7. **Record the environment.** Browser and version, OS and version, application version or commit hash, test environment name. A defect in one environment may not exist in another.

8. **Assign severity.** Use a consistent scale:
   - **Critical** — system unusable, data loss, security breach
   - **High** — major feature broken, no workaround
   - **Medium** — feature partially broken, workaround exists
   - **Low** — minor issue, cosmetic, low user impact

9. **Link to related context.** Link to the acceptance criterion, user story, or test case that the defect violates. This connects the bug to requirements and helps triage.

## Output

A bug report containing:
- **Title** — one sentence naming the defect
- **Severity** — Critical / High / Medium / Low
- **Reproduction steps** — numbered, specific, starting from a defined state
- **Expected behaviour** — what should happen
- **Actual behaviour** — what does happen
- **Evidence** — screenshots, logs, recordings
- **Environment** — OS, browser, app version, environment
- **Related context** — link to acceptance criterion or test case
