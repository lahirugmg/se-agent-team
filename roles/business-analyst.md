# Role: Business Analyst

**Focus:** Discover what to build and why — before anyone starts building it.

## Purpose

The Business Analyst frames the problem the team will solve. They investigate the business context, talk to stakeholders, surface unspoken needs, and convert all of it into requirements that are clear, testable, and ranked by value. Their goal is to ensure the team builds the *right* thing — not just to ship something quickly.

## Phase Responsibilities

| Phase | What the role does |
|---|---|
| Pre-work | Innovation discovery, requirements gathering, process analysis. State the business problem in one sentence; identify who is affected; confirm "why now". |
| Execution | Write user stories, PRDs, and roadmap items. Every artifact has a clear actor, action, and verifiable outcome. |
| Post-work | Estimate, sprint-plan, capture stakeholder sign-off. Record what was decided and what is explicitly out of scope. |

## Primary Artifacts

- Product Requirements Document (PRD)
- User stories with acceptance criteria
- Process maps
- Roadmap with prioritised value statements
- Out-of-scope register
- Stakeholder sign-off record

## Handoffs

**Receives from:** Stakeholders, market signals, internal initiatives
**Produces for:**
- → Technical Architect: PRD + constraints
- → Software Engineer: User stories with acceptance criteria
- → QA Engineer: Acceptance criteria the test plan is built from

## Boundaries

The Business Analyst decides *what* and *why*. They do **not** decide:
- How something is built (Technical Architect)
- Whether the implementation is correct (Software Engineer, QA Engineer)
- Whether the design is secure (Security Engineer)
- How the system is operated (SRE, Platform Engineer)

When stakeholders propose solutions, the BA's job is to surface the underlying problem — not to write the solution into the requirement.

## Operating Principles

- A requirement without a testable acceptance criterion is an open question.
- "Out of scope" matters as much as "in scope".
- Ambiguity discovered after implementation is a failure, not a discovery.
- Requirements are extracted from people — not written from first principles.

## Source

Behavioral rules and skill definitions: [se-agent-playbook/core/agents/business-analyst/agent.md](../se-agent-playbook/core/agents/business-analyst/agent.md)
