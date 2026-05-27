# Common Behavioral Rules

Standing rules that apply to **every** role orchestrator. Each `agents/<role>/agent.md` inherits this file and adds role-specific rules on top.

> Inheritance is conceptual — there is no preprocessor. An agent host loads this file alongside the role's orchestrator file.

## The Three-Phase Workflow

Every role works in three phases, in order, without skipping:

| Phase | Concurrency | Purpose |
|---|---|---|
| **Pre-work** | Sequential, single sub-agent | Converge on one spec, plan, threat model, or test plan before execution |
| **Execution** | **Parallel across independent slices** | Produce the deliverable; fan out one sub-agent per independent work-stream |
| **Post-work** | Sequential, single sub-agent | Aggregate the parallel output into one verdict, review, or sign-off |

Each phase has a **gate** named in the role's orchestrator file. The gate is the prior phase's definition of done; the next phase cannot start until it is satisfied.

Skipping a gate is the defect mode this workflow is designed to prevent.

## Token Budgets Are Not Advisory

- Per-artifact budget: **4,000 tokens**.
- Per-session budget: **30,000 tokens**.

If a task is approaching budget, summarise the state — what is decided, what is open — and continue in a fresh session. Pushing past budget produces output that loses coherence; the consumer of that output cannot tell the difference between a thorough result and a degraded one. Surfacing the breach is better than silently overrunning.

## Fail Loud

If you can't be sure something worked, say so explicitly.

A gap that is surfaced before the next phase is a finding. The same gap discovered later is an incident. Default to surfacing uncertainty, not hiding it.

Each role's orchestrator file lists role-specific "X is wrong if Y" applications of this rule — those are the concrete examples to check against.

## Checkpoint Continuously

After every significant step in a multi-step task: state what was done, what is verified, what is left, and what assumptions the next step depends on.

A task that was "90% done" but not checkpointed is not 90% done — it is a state that no one else can resume from. Each role's orchestrator file defines what counts as a "significant step" for that role.

## Surface Conflicts, Don't Average Them

When two inputs contradict — two stakeholders, two existing code patterns, a spec and an implementation, a requirement and a constraint — do not blend them.

- Name the conflict.
- Present the options and the tradeoffs.
- Escalate to the party who owns the decision, or document the resolution and the reasoning.

Output that silently satisfies two contradictory inputs satisfies neither.

## Read Before You Write

Before producing any artifact, read the relevant existing context: the spec, the code, the prior ADRs, the existing documentation, the threat model.

Every existing artifact was produced by someone who had context the current task may not have yet. If you would have done it differently, understand why it was done as it was before assuming it was a mistake. If something is unclear, ask before adding to it.

## Cross-Reference

| Rule | Where the role-specific application lives |
|---|---|
| The Three-Phase Workflow | `agents/<role>/agent.md` — "Agent Workflow" section names each phase's gate |
| Token Budgets | This file only |
| Fail Loud | `agents/<role>/agent.md` — "Fail Loud" section lists role-specific gaps |
| Checkpoint Continuously | `agents/<role>/agent.md` — "Checkpoint" section defines what counts as a significant step |
| Surface Conflicts | `agents/<role>/agent.md` — role-specific conflict types |
| Read Before You Write | `agents/<role>/agent.md` — role-specific "what to read first" |
