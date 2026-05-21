# Skill: document-release

**Type:** composite
**Sub-skills:** api-docs → changelog → stakeholder-trust
**Phases:** Pre-work: read implementation, git diff, and existing docs (inherent, no dedicated skill) | Execution: api-docs, changelog | Post-work: stakeholder-trust

## Purpose

End-to-end post-ship documentation workflow for a release. Covers the technical reference (API docs), the structured change record (changelog), and the stakeholder-facing communication (what changed and why it matters). Ensures that every shipped change leaves the system more understandable than before.

## When to Invoke

- A feature or change has shipped and documentation needs to be updated.
- A release is being prepared and the changelog and stakeholder communication must be ready before announcement.
- API changes need to be reflected in reference documentation before external consumers are affected.

## Workflow

### Step 1 — API Docs · Execution (@api-docs)

Before writing any user-facing documentation:

1. Read the implementation, `git diff` since the last release, and any existing API reference.
2. Run the api-docs skill: update or create reference documentation for every changed endpoint, parameter, or response shape.
3. Verify accuracy against the running implementation — documentation that contradicts the code is worse than no documentation.

**Gate:** API docs reflect the current implementation exactly. No deprecated behaviour is documented as current.

### Step 2 — Changelog · Execution (@changelog)

With API docs complete:

1. Run the changelog skill: produce a structured changelog entry for this release.
2. Group changes by type (Added, Changed, Fixed, Removed, Deprecated, Security).
3. Each entry must be meaningful to the reader — "various bug fixes" is not an entry.
4. Breaking changes are called out explicitly with migration notes.

**Gate:** Every significant change in this release has a changelog entry. Breaking changes have migration guidance.

### Step 3 — Stakeholder Communication · Post-work (@stakeholder-trust)

With technical docs and changelog done:

1. Run the stakeholder-trust skill: translate the changelog into a communication suitable for non-technical stakeholders.
2. Focus on impact (what users can now do, what improved, what to watch for) rather than implementation detail.
3. Match the format and channel to the audience: executive summary, product announcement, or user notification as appropriate.

**Gate:** Stakeholder communication reviewed by a non-technical reader for clarity before distribution.

## Output

A release documentation package containing:

- **Updated API reference** — accurate, complete, reflecting the current implementation
- **Changelog entry** — structured, grouped, with migration notes for breaking changes
- **Stakeholder communication** — impact-focused, audience-appropriate, reviewed for clarity
- **Distribution record** — where the communication was sent and when

This package closes the documentation loop on a shipped release and serves as the historical record for future writers.
