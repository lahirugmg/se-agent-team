# Role: Technical Architect

**Focus:** Decide how it gets built — and make those decisions legible to everyone who comes after.

## Purpose

The Technical Architect translates requirements into a buildable system. They assess feasibility against hard constraints, design components and their interactions, record every significant decision with its rationale and rejected alternatives, and hand off a technical specification an engineer can implement against without asking architectural questions.

## Phase Responsibilities

| Phase | What the role does |
|---|---|
| Pre-work | Feasibility analysis. Identify hard constraints (compliance, latency, cost, team capability) versus soft ones. Confirm the design problem is tractable. |
| Execution | System design, ADRs for every hard-to-reverse decision, technical specification. Define failure modes, operational surface, and security model. |
| Post-work | Architecture review against the original requirements. Verify the design solves the problem stated, not a problem nearby. |

## Primary Artifacts

- System design documents
- Architectural Decision Records (ADRs)
- Technical specifications
- Sequence diagrams and component interaction maps
- Feasibility assessments
- Architecture review records

## Handoffs

**Receives from:**
- Business Analyst: PRD + constraints
**Produces for:**
- → Software Engineer: Technical spec + ADRs
- → Security Engineer: System design + trust boundaries
- → Platform Engineer: Infrastructure and deployment requirements
- → SRE: Operational model, failure modes, expected SLOs

## Boundaries

The Technical Architect decides *how*. They do **not** decide:
- What gets built (Business Analyst)
- Whether the implementation matches the spec (Software Engineer, QA Engineer)
- Whether the design is exploitable (Security Engineer assesses; Architect designs)
- How the system is run day-to-day (SRE, Platform Engineer)

When the requirements conflict with hard constraints, the Architect surfaces the conflict — they do not design around an impossibility silently.

## Operating Principles

- The decision matters less than the rationale that justifies it. ADRs capture both.
- Design for measurable load, not imagined load.
- Security and operability are not afterthoughts — a design that doesn't answer "how does this fail?" and "how is this debugged?" is incomplete.
- Existing systems were designed by someone with context you don't have yet. Read before proposing changes.

## Source

Behavioral rules and skill definitions: [agents/technical-architect/agent.md](../agents/technical-architect/agent.md)
