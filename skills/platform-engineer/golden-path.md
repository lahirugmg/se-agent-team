# Skill: golden-path

**Type:** atomic

## Purpose

Design and document an opinionated, supported workflow for teams to follow for a specific task — from "I need to do X" to "X is done" — without requiring platform team involvement or tribal knowledge. A golden path is not a policy. It is a product: it should be so good that teams choose it without being required to.

## When to Invoke

- A new platform capability has a defined developer contract (idp-design complete) and needs a concrete workflow.
- Teams are inconsistently approaching the same task and standardisation would reduce fragility.
- An existing path is stale — it no longer reflects the actual infrastructure or tooling.
- A new team is onboarding and there is no documented path for them to follow.

**Do not invoke** before the IDP design is complete — a golden path that doesn't reflect the actual developer contract will mislead teams.

## Workflow

1. **State the task the path solves.** One sentence: "A team that needs to [do X] follows this path." If you cannot write that sentence, the path scope is undefined. Define it first.

2. **Walk the path as a team would.** Before writing documentation, perform or simulate every step as if you are a new team following the path for the first time. Identify every point where a team would need information not in the path, need to ask someone, or need to make a non-obvious decision. These are gaps — fix them before documenting, not after.
   **Gate:** Every step in the path must be executable by someone unfamiliar with the platform internals. If a step requires knowledge the team doesn't have, the path is not ready.

3. **Write the path document.** Structure:
   ```
   ## Task
   [What the team is trying to accomplish]

   ## Prerequisites
   [What the team must have or know before starting]

   ## Steps
   1. [Concrete, executable action]
      Expected outcome: [what the team observes when this step succeeds]
   2. ...

   ## Verification
   [How the team confirms the task is complete]

   ## What to do when things go wrong
   [The two or three most common failure modes and how to recover]

   ## Off this path
   [What this path does not cover — and where to go instead]
   ```

4. **Validate with someone who did not write it.** Have a team member follow the path on a real or representative task without help from the path author. Observe every point of confusion. Update the path based on what was observed, not on what was intended.
   **Gate:** The path must be completed by someone who did not write it, without platform team intervention, before it is published. A path validated only by its author is not validated.

5. **Publish and set a review date.** A golden path without a review date is a path on its way to being wrong. Set a review trigger: the next major version of the underlying tool, the next significant infrastructure change, or a fixed calendar interval — whichever comes first.

## Output

- **Golden path document** — task statement, prerequisites, numbered steps with expected outcomes, verification, failure recovery, and off-path scope.
- Validated by at least one team member who did not write it.
- Review date or trigger set at publication.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "Teams will figure it out" | They will — but inconsistently, with tribal knowledge, and by asking the platform team repeatedly. The path exists to prevent that. |
| "We'll validate it once teams start using it" | Validation after publication means teams hit the gaps first. Validate before publishing. |
| "The path is obvious if you understand the infrastructure" | Teams should not need to understand the infrastructure. That is the whole point of the self-service boundary. |
| "We don't need a review date, we'll update it when it changes" | Changes to underlying infrastructure rarely trigger path updates unless a review is scheduled. Schedule it. |

## Red Flags

- Path steps that require knowing platform internals to execute
- No expected outcome for individual steps — teams can't tell if they succeeded
- "What to do when things go wrong" section missing — paths fail and teams need to recover
- Path validated only by the author
- No review date or trigger set at publication
- Off-path scope not defined — teams will assume the path covers more than it does

## Verification

Before publishing:

- [ ] Task statement in one sentence
- [ ] Every step is concrete and executable without platform internals knowledge
- [ ] Every step has an expected outcome the team can observe
- [ ] "What to do when things go wrong" covers the most common failure modes
- [ ] Off-path scope is explicitly defined
- [ ] A team member who did not write the path completed it without platform team assistance
- [ ] Review date or trigger is set
