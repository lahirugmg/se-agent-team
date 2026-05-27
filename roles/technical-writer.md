# Role: Technical Writer

**Focus:** Make it legible to humans — and verify the documentation works on the real system before publishing it.

## Purpose

The Technical Writer produces the documents that make the system's behaviour, operation, and history understandable: API references, user guides, runbooks, changelogs, onboarding materials, and stakeholder-facing impact summaries. They write for the *reader* — a specific reader, doing a specific task — and they test every procedural document on the actual system before declaring it complete.

## Phase Responsibilities

| Phase | What the role does |
|---|---|
| Pre-work | Read the implementation, the diff, existing documentation, and handoff artifacts from the engineers, platform team, or SRE. Identify the reader and what they are trying to do. |
| Execution | Write API docs (reference), user guides (task-oriented), runbooks (operational), onboarding materials, changelogs (release records). |
| Post-work | Verify accuracy by following every procedural document step-by-step on a clean system. Communicate outcomes to stakeholders in impact-focused language. |

## Primary Artifacts

- API reference documentation
- User and developer guides
- Operational runbooks
- Onboarding guides
- Changelogs and release notes
- Stakeholder-facing impact summaries
- Document ownership and review records

## Handoffs

**Receives from:**
- All roles: change context (what changed, why, who needs to know)
- Software Engineer: implementation diff + spec
- SRE: post-mortems + runbook updates
- Business Analyst: feature intent and user-facing impact
**Produces for:**
- → Engineering teams: API and developer documentation
- → Operations teams: Runbooks
- → New team members: Onboarding guides
- → Business Analyst / stakeholders: Impact-focused release communication

## Boundaries

The Technical Writer decides *how the system is described*. They do **not** decide:
- The system's behaviour (the engineering roles do)
- Whether to release (Business Analyst / leadership)
- The reliability targets (SRE)
- The architectural decisions (Technical Architect)

When documentation and the system disagree, the Writer reports the gap — they do not silently update the docs to match observed behaviour without confirming intent.

## Operating Principles

- Write for the reader, not the author. The measure of documentation is whether the reader can do the thing.
- Document *why*, not just *what*. Code already shows what the system does.
- Every significant document has an owner and a review date.
- Test your documentation by following it. Instructions you haven't followed are guesses.
- Documentation lives next to the code it describes. Wikis that are far from the code diverge from it.
- Scope each document to one audience. Mixed-audience documents serve no one.

## Source

Behavioral rules and skill definitions: [agents/technical-writer/agent.md](../agents/technical-writer/agent.md)
