# Skill: intrapreneur-workflow

**Type:** composite
**Sub-skills:** discovery → spec-writing → build (ship-feature) → agent-output-review → stakeholder communication
**Phases:** Pre-work: discovery, spec-writing | Execution: build (ship-feature) | Post-work: agent-output-review, stakeholder communication

## Purpose

Full lifecycle workflow for internally-driven improvements: ideas that originate within the engineering team rather than from a product backlog. Covers the full arc from unspoken need to shipped code to stakeholder trust.

This skill is for changes where the engineer identifies the problem, builds the case, implements the solution, and communicates the outcome — without waiting for a ticket.

## When to Invoke

- You've identified a recurring pain point, performance issue, or missing capability that has no ticket.
- You want to build something that isn't on the roadmap and need a structured approach to validate and ship it.
- A team process is causing drag and you want to fix it without convening a committee.

## Workflow

### Phase 1 — Discovery · Pre-work

Before writing a line of code or a line of spec:

1. **Name the problem precisely.** "The auth module is slow" is not a problem statement. "Login takes 4s on the /token endpoint because we make 3 serial DB calls where 1 would do" is.

2. **Quantify the impact.** Time saved, errors reduced, incidents avoided, velocity gained. An improvement you can't quantify is harder to justify and harder to prioritise.

3. **Check if this is already being solved.** Search the issue tracker, ask in the relevant channel, check recent PRs. Don't build what's already in flight.

4. **Assess scope honestly.** Small improvements ship fast and build credibility. Large improvements need stakeholder buy-in. Know which this is before you start.

**Gate:** Can you state the problem, its measurable impact, and a proposed fix in three sentences? If not, keep discovering.

### Phase 2 — Spec · Pre-work (@spec-writing)

Write a lightweight spec:
- Problem statement (one paragraph)
- Proposed solution (one paragraph)
- Scope: what's in, what's out
- GIVEN/WHEN/THEN cases for the key behaviour changes
- Estimated effort

Keep it short. This is an internal improvement, not a product feature. A one-page spec is sufficient for most intrapreneur work.

Share the spec with one or two colleagues before building. The goal is to surface the "have you considered X?" before you've invested implementation time.

**Gate:** One technical peer has reviewed the spec and has no blocking objections.

### Phase 3 — Build · Execution (@ship-feature)

Follow the ship-feature workflow:
- Implement against the spec.
- Use AI agents where appropriate — this is exactly the kind of bounded, well-specified task where agents excel.
- Apply agent-output-review if agents were used.

Keep the PR small. A focused change ships faster, reviews easier, and rolls back cleanly.

### Phase 4 — Agent Output Review · Post-work (@agent-output-review)

If AI agents produced any of the implementation, apply agent-output-review before the PR is merged. Do not skip this step — intrapreneur work often has lighter oversight than ticket-driven work, which makes the review more important, not less.

### Phase 5 — Stakeholder Communication · Post-work

After the change ships:

1. **Write a brief summary.** What changed, why, what the measured impact was. Three to five bullet points.

2. **Send it to the right people.** The team lead, the relevant product or business stakeholder, anyone who would want to know. Don't assume people noticed the merge.

3. **Close the loop on the original problem.** Did the change solve it? If not fully, say so. What would address the remainder?

4. **Document if the change affects how others work.** Update runbooks, READMEs, or onboarding docs before announcing the change.

## Output

- Discovery summary (problem + impact + proposed solution).
- Spec document.
- Merged PR.
- Post-ship communication: what changed, measured impact, what's next.
