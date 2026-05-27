# AGENTS.md — How an agent host uses this repo

This repo defines a software engineering team as **eight role orchestrators plus their micro-agent skills**. It is tool-agnostic markdown. An agent host (Claude Code, Cursor, Aider, custom runner, or a human team lead) reads this file to know how to pick up a task and route it through the team.

> Full design rationale: [README.md](README.md). This file is the operating manual.

## 1. Pick the role that owns the task

Eight roles cover the SDLC end-to-end. Match the task to the stage it belongs to:

| Stage | Role | Orchestrator |
|---|---|---|
| requirements | Business Analyst | [agents/business-analyst/agent.md](agents/business-analyst/agent.md) |
| architecture | Technical Architect | [agents/technical-architect/agent.md](agents/technical-architect/agent.md) |
| implementation | Software Engineer | [agents/software-engineer/agent.md](agents/software-engineer/agent.md) |
| testing | QA Engineer | [agents/qa-engineer/agent.md](agents/qa-engineer/agent.md) |
| security | Security Engineer | [agents/security-engineer/agent.md](agents/security-engineer/agent.md) |
| deployment | Platform Engineer | [agents/platform-engineer/agent.md](agents/platform-engineer/agent.md) |
| operations | SRE | [agents/sre/agent.md](agents/sre/agent.md) |
| documentation | Technical Writer | [agents/technical-writer/agent.md](agents/technical-writer/agent.md) |

Scope per role and what each role *does not* decide: [docs/ROLES.md](docs/ROLES.md). Charters in [roles/](roles/).

## 2. Load the orchestrator, then read its SKILLS.md

The orchestrator file at `agents/<role>/agent.md` holds the role's **behavioral rules**. It inherits the universal rules from [agents/COMMON.md](agents/COMMON.md) — load that file alongside the role's orchestrator. Both are required reading before any skill runs. They are not optional.

The skill index at `agents/<role>/SKILLS.md` lists the micro-agents available to that orchestrator, grouped by phase. Each row has a one-line "When to use" trigger. The same trigger appears as a `**Trigger:**` line inside the skill file itself — both sources are kept in sync. Use either to pick the right skill for the current task.

## 3. Run the three-phase workflow

Every role works in three sequential phases. Concurrency inside each phase is fixed:

| Phase | Concurrency | Why |
|---|---|---|
| **Pre-work** | Sequential, single sub-agent | One spec / plan / model must converge before execution starts |
| **Execution** | **Parallel across independent slices** | The work is naturally divisible; fan out one sub-agent per slice |
| **Post-work** | Sequential, single sub-agent | One verdict / review aggregates the parallel output |

Each phase has a **gate** named in the orchestrator file. Do not move to the next phase until the gate is satisfied. Skipping a gate is the defect mode the workflow is designed to prevent.

## 4. Dispatch a micro-agent

To run a skill, load its file at `skills/<role>/<skill>.md` into a fresh sub-agent context. Each skill file is self-contained: read its **When to Invoke**, **Inputs**, **Procedure**, **Output**, and **Verification** sections, then execute against them.

- **Atomic** skills: one phase, one responsibility.
- **Composite** skills: chain atomics across phases. The file names the sub-skills and the gates between them.

A micro-agent's context should not extend beyond its single skill. If a skill needs another skill's output, the orchestrator passes the artifact in — the micro-agent does not load sibling skills itself.

## 5. Hand off across roles

A task that spans the SDLC moves between role orchestrators per the handoff table in [docs/ROLES.md](docs/ROLES.md#handoffs) and the stage flow in [docs/SDLC.md](docs/SDLC.md). The receiving role's gate is the *prior* role's definition of done. Loop back to the owning role on gate failure — do not skip forward.

**Cross-role conducting** is the human user's job (or a thin wrapper above this repo). This repo does not define a 9th "program manager" agent: the SDLC document is the routing table.

## 6. What an agent host MUST NOT do

- **Do not skip the orchestrator file** and run a skill directly. Skills assume the role's behavioral rules and phase gates are in force.
- **Do not blend skills from two roles** inside one micro-agent. Cross-role work moves between orchestrators, not inside one sub-agent's context.
- **Do not parallelise pre-work or post-work.** The concurrency contract above is part of the design.
- **Do not edit a skill file from inside a skill-running sub-agent.** Skill authoring is a meta-task and belongs to a separate session.

## 7. Where to look when stuck

| Need | Read |
|---|---|
| "What does this role own?" | [docs/ROLES.md](docs/ROLES.md) |
| "Which role hands off to which?" | [docs/ROLES.md](docs/ROLES.md#handoffs), [docs/SDLC.md](docs/SDLC.md) |
| "What are the standing rules every role follows?" | [agents/COMMON.md](agents/COMMON.md) |
| "What are the role-specific rules on top of those?" | `agents/<role>/agent.md` — Behavioral Rules section |
| "Which skill do I run?" | `agents/<role>/SKILLS.md` — the trigger column |
| "How do I run this skill?" | `skills/<role>/<skill>.md` — Procedure section |
| "Why is the team shaped this way?" | [README.md](README.md) |
