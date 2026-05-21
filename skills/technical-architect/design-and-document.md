# Skill: design-and-document

**Type:** composite
**Sub-skills:** system-design → adr-writing → technical-spec
**Phases:** Pre-work: feasibility-analysis (run before invoking this composite) | Execution: system-design, adr-writing, technical-spec | Post-work: architecture-review (run after)

## Purpose

End-to-end workflow for translating a signed-off PRD into a documented, decided, and implementation-ready technical design. Produces the artifacts that let an engineering team begin work without unresolved architectural questions.

## When to Invoke

- A PRD or equivalent requirements document has been signed off and engineering work is about to begin.
- A major architectural change needs to be designed, decided, and handed to implementers.
- Existing architecture needs to be revised and the decisions documented.

## Workflow

### Step 1 — System Design · Execution (@system-design)

Before any decisions are finalised:

1. Read the PRD and any existing architecture documentation.
2. Run the system-design skill: define components, interactions, data flows, and technology choices.
3. Produce at least one design option with tradeoffs documented. Non-obvious alternatives must be shown.

**Gate:** Do not proceed until there is a concrete design option — even a rough one — to react to.

### Step 2 — ADR Writing · Execution (@adr-writing)

For each significant design decision reached in Step 1:

1. Run the adr-writing skill for every decision that would be hard to reverse or that has meaningful alternatives.
2. Each ADR must document: context, options considered, decision, rationale, and consequences.
3. ADRs are written before the technical spec — the spec describes the decided design, not the alternatives.

**Gate:** Every hard-to-reverse decision has an ADR. The set of ADRs is complete when there are no undocumented "because we decided" statements in the design.

### Step 3 — Technical Spec · Execution (@technical-spec)

With the design decided and ADRs written:

1. Run the technical-spec skill to produce the implementation-ready spec.
2. The spec must be specific enough that an engineer can begin without asking architectural questions.
3. Include: component interfaces, data models, API contracts, sequencing, error handling approach, and open implementation questions.

**Gate:** At least one engineer has reviewed the spec and confirmed they could begin implementation without further design input.

## Output

A complete design package containing:

- **Design document** — components, interactions, data flows, technology choices, tradeoffs
- **ADR set** — one ADR per significant architectural decision
- **Technical spec** — implementation-ready: interfaces, contracts, data models, sequencing
- **Open implementation questions** — items deferred to the engineering team with guidance

This package is the handoff artifact for the Software Engineer to begin implementation.
