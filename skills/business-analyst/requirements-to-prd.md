# Skill: requirements-to-prd

**Type:** composite
**Sub-skills:** requirements-gathering → user-story → prd-writing
**Phases:** Pre-work: requirements-gathering | Execution: user-story, prd-writing | Post-work: stakeholder sign-off (embedded in Step 3 gate)

## Purpose

End-to-end workflow for transforming a vague idea, stakeholder request, or problem statement into a signed-off PRD with well-formed user stories. Owns the full discovery-to-definition arc before any technical work begins.

## When to Invoke

- A new feature or initiative needs to be defined before architecture or engineering can start.
- Stakeholders have a goal but no structured requirements.
- A PRD is required as the formal handoff to the Technical Architect.

## Workflow

### Step 1 — Requirements Gathering · Pre-work (@requirements-gathering)

Before writing anything:

1. Identify the stakeholders and schedule discovery sessions.
2. Run the requirements-gathering skill: extract goals, constraints, assumptions, and non-goals.
3. Document open questions and resolve blocking ones before proceeding.

**Gate:** Do not proceed until at least one stakeholder session is complete and the problem statement is agreed.

### Step 2 — User Stories · Execution (@user-story)

With requirements in hand:

1. Convert each requirement into one or more user stories using the user-story skill.
2. Each story must have: a role, a goal, a reason, and GIVEN/WHEN/THEN acceptance criteria.
3. Review stories with a stakeholder representative. Stories that cannot be accepted as written are rewritten, not skipped.

**Gate:** All stories have acceptance criteria that a QA Engineer could test without asking for clarification.

### Step 3 — PRD Writing · Execution + Post-work (@prd-writing)

Compile everything into a PRD:

1. Run the prd-writing skill with the gathered requirements and validated user stories as input.
2. Ensure the PRD includes: problem statement, goals, success metrics, user stories, out-of-scope items, dependencies, open questions.
3. Circulate for stakeholder sign-off. Track feedback and revise until approved.

**Gate:** PRD has explicit sign-off from the product owner or sponsor before it is handed off.

## Output

A signed-off PRD document containing:

- **Problem statement** — what problem this solves and for whom
- **Goals and success metrics** — how success will be measured
- **User stories** — with full GIVEN/WHEN/THEN acceptance criteria
- **Out of scope** — explicit list of what this does NOT include
- **Dependencies** — systems, teams, or decisions this depends on
- **Open questions** — unresolved items with owners and deadlines
- **Sign-off record** — who approved and when

This document is the handoff artifact for the Technical Architect to begin system design.
