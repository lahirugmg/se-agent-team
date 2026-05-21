# Skill: prd-writing

**Type:** atomic

## Purpose

Produce a Product Requirements Document (PRD) that serves as the authoritative reference for what is being built, why, and how success is measured. The PRD is the primary handoff artifact from the Business Analyst to the Technical Architect.

## When to Invoke

- A feature or initiative has been through requirements gathering and has validated user stories.
- A formal written record of requirements is needed before design or engineering begins.
- A previously informal or verbal agreement needs to be committed to writing.

## Workflow

1. **Gather inputs.** Collect: requirements document, validated user stories, any prior discussions, competitive or market context. Do not write the PRD from memory or inference — every claim must trace to an input.

2. **Write the problem statement.** In two to four sentences: what problem exists, who has it, and what the cost of not solving it is. Avoid mentioning the solution.

3. **State goals and success metrics.** List two to five measurable goals. Each goal has a metric and a target:
   - "Reduce checkout abandonment from 12% to under 8% within 60 days of launch"
   - "All payment errors surfaced to the user within 500ms"
   Metrics without targets are not measurable.

4. **List requirements.** Include all validated functional and non-functional requirements. Number them. Each requirement must be testable — if you cannot write a test for it, rewrite it.

5. **Embed user stories.** Include all validated user stories with their acceptance criteria. Link each story to the requirement it satisfies.

6. **Define out of scope.** Explicitly list what this PRD does NOT address. An item is only out of scope if it has been consciously deferred — "we haven't thought about it" is not out of scope.

7. **Document dependencies.** List other systems, teams, or decisions that must be resolved before or during delivery. Each dependency has an owner.

8. **List open questions.** Questions that are unresolved but not blocking initial design. Each has an owner and a deadline.

9. **Circulate for sign-off.** Share with product owner, key stakeholders, and the lead engineer. Resolve feedback in the document, not in email. Track who approved and when.

## Output

A PRD document containing:
- Problem statement
- Goals with measurable success metrics
- Numbered, testable requirements (functional and non-functional)
- User stories with acceptance criteria
- Out of scope section
- Dependencies with owners
- Open questions with owners and deadlines
- Sign-off record (name, role, date)
