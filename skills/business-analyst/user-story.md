# Skill: user-story

**Type:** atomic

## Purpose

Convert a requirement into one or more well-formed user stories with testable acceptance criteria. A user story is not a feature description — it is a commitment to deliver value to a specific role.

## When to Invoke

- A requirement exists and needs to be expressed in a form an engineering team can estimate and test.
- Acceptance criteria for an existing story are missing, vague, or untestable.
- A story needs to be split into smaller deliverable units.

## Workflow

1. **Identify the role.** Name the specific person who benefits — not "the user" or "the system." If multiple roles benefit differently, write separate stories.

2. **State the goal.** What does this role want to accomplish? Express it as an outcome, not a feature. "Be notified when X happens" not "receive an email."

3. **State the reason.** Why does this role want this? The reason is what makes the story testable — if the implementation achieves the reason, it passes.

4. **Write the story.**
   ```
   As a <role>,
   I want to <goal>,
   so that <reason>.
   ```

5. **Write acceptance criteria.** Use GIVEN/WHEN/THEN format. Each criterion must be independently testable:
   ```
   GIVEN <precondition>
   WHEN <action>
   THEN <observable outcome>
   ```
   Write at least one criterion for the happy path and one for a failure or edge case.

6. **Apply INVEST.** Verify the story is:
   - **Independent** — can be delivered without depending on another incomplete story
   - **Negotiable** — the how is open; only the what and why are fixed
   - **Valuable** — delivers something a stakeholder cares about on its own
   - **Estimable** — a developer can size it
   - **Small** — completable within one sprint
   - **Testable** — every acceptance criterion can be confirmed true or false

7. **Split if needed.** If a story fails INVEST (too large, too vague, too dependent), split it. Common split patterns: by user role, by data type, by happy/error path, by CRUD operation.

## Output

For each story:
- Story statement (As / I want / So that)
- Acceptance criteria (GIVEN/WHEN/THEN, minimum two per story)
- Definition of done (any additional conditions beyond acceptance criteria)
- Story size estimate (if requested)
- Split rationale (if the original story was split)
