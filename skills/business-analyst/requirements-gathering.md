# Skill: requirements-gathering

**Type:** atomic

## Purpose

Extract, validate, and document requirements from stakeholders before any solution is designed. Produces a structured requirements document that captures goals, constraints, assumptions, and open questions — not a solution.

## When to Invoke

- A feature or initiative needs to be understood before a spec or PRD can be written.
- Stakeholders have a goal but it has not been turned into structured requirements.
- Conflicting requirements from different stakeholders need to be reconciled.

## Workflow

1. **Identify stakeholders.** List everyone who has a stake in the outcome: users, product owners, engineers, legal, operations. Missing a stakeholder at this stage means missing a requirement later.

2. **Prepare discovery sessions.** For each stakeholder group, prepare questions focused on goals and constraints — not solutions. Avoid "what should it do?" in favour of "what problem does this solve?" and "what does success look like?"

3. **Run discovery.** Conduct interviews, workshops, or async questionnaires. For each session:
   - Capture verbatim: what the stakeholder said they want
   - Capture interpreted: what you believe they actually need
   - Note conflicts between what different stakeholders want

4. **Consolidate.** Group findings by theme. Separate:
   - **Functional requirements** — what the system must do
   - **Non-functional requirements** — performance, security, compliance, availability
   - **Constraints** — things that cannot change (budget, timeline, existing systems)
   - **Assumptions** — things believed to be true but not confirmed
   - **Non-goals** — explicit list of what this will NOT address

5. **Identify open questions.** List every requirement that depends on an unanswered question. Assign each question an owner and a resolution deadline.

6. **Validate with stakeholders.** Share the consolidated requirements back. Get explicit confirmation or corrections. Do not proceed without at least one round of stakeholder validation.

## Output

A requirements document containing:
- Problem statement
- Functional requirements (numbered, testable)
- Non-functional requirements
- Constraints
- Assumptions
- Non-goals
- Open questions with owners and deadlines
- Stakeholder sign-off record
