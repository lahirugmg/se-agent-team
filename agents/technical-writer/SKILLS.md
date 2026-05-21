# Technical Writer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (understand what changed and what needs to be documented — inherited from other agents' artifacts), **Execution** (produce the documentation), **Post-work** (communicate outcomes to stakeholders and verify accuracy).

## Pre-work

The Technical Writer's pre-work is inherent: read the implementation, PRD, changelog, and existing docs to understand what changed before writing anything. No dedicated pre-work skill is needed — the inputs arrive as handoff artifacts from the Software Engineer, Platform Engineer, and SRE.

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| api-docs | @core/skills/technical-writer/api-docs.md | Write or update reference documentation for an API |
| user-guide | @core/skills/technical-writer/user-guide.md | Produce a task-oriented guide for end users or operators |
| runbook-writing | @core/skills/technical-writer/runbook-writing.md | Write a runbook for a recurring operational procedure |
| onboarding-guide | @core/skills/technical-writer/onboarding-guide.md | Create onboarding documentation for a new engineer or user joining a system |
| changelog | @core/skills/technical-writer/changelog.md | Write a structured changelog entry for a release or significant change |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| stakeholder-trust | @core/skills/technical-writer/stakeholder-trust.md | Communicate outcomes and system changes to non-technical stakeholders after agent work ships |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| document-release | @core/skills/technical-writer/document-release.md | api-docs → changelog (execution) → stakeholder-trust (post-work) |
