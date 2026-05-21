# Skill: sprint-planning

**Type:** atomic

## Purpose

Prepare and facilitate a sprint planning session that produces a committed sprint goal, a selected and estimated backlog, and a shared understanding of what the team is delivering. The output is a plan the team owns — not a list handed down from management.

## When to Invoke

- A sprint is about to begin and the team needs to select and commit to work.
- A sprint planning session needs facilitation or structure.
- The backlog is not ready for planning and needs to be triaged before the session.

## Workflow

1. **Verify backlog readiness.** Before planning begins, confirm that the top items in the backlog meet the team's Definition of Ready:
   - Story is written with acceptance criteria
   - Dependencies are identified and resolved or explicitly accepted
   - Story is estimated (or small enough to not need estimation)
   - Any design or spec needed for implementation is available
   Items that are not ready are moved down. Do not plan unready work.

2. **Confirm sprint goal.** The sprint goal is one sentence that describes what the team is trying to achieve — not a list of tickets. A good sprint goal can be used to decide whether to include or drop a story at the margin. Agree on the goal before selecting stories.

3. **Select stories.** Starting from the top of the backlog, pull in stories that serve the sprint goal until the team's capacity is reached. Capacity is based on historical velocity or available person-days, minus planned absences and ceremony time.

4. **Clarify stories.** For each selected story, confirm the team understands:
   - The acceptance criteria
   - Any technical approach or constraints
   - Who is likely to work on it
   If a story generates significant technical discussion, timebox the discussion and flag the story for a follow-up spike if unresolved.

5. **Identify risks.** Flag any story that depends on an external team, a production system access, or an unresolved design decision. These are risks to the sprint — name them, don't ignore them.

6. **Confirm commitment.** The team — not the product owner — commits to the sprint. The commitment is to the sprint goal, not to delivering every ticket. Record the committed stories and the sprint goal.

## Output

- **Sprint goal** — one sentence, agreed by the team
- **Committed backlog** — list of selected stories with estimates
- **Risk register** — stories with external dependencies or unresolved questions
- **Capacity summary** — how team capacity was calculated and used
