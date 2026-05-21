# Technical Architect — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (assess feasibility before designing), **Execution** (produce the architecture artifacts), **Post-work** (review the design against requirements).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| feasibility-analysis | @core/skills/technical-architect/feasibility-analysis.md | Assess whether a proposed approach is technically achievable within given constraints |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| system-design | @core/skills/technical-architect/system-design.md | Design the architecture for a new system or major component |
| adr-writing | @core/skills/technical-architect/adr-writing.md | Document an architectural decision with context, alternatives, and rationale |
| technical-spec | @core/skills/technical-architect/technical-spec.md | Write a detailed technical specification for implementation teams |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| architecture-review | @core/skills/technical-architect/architecture-review.md | Review an existing or proposed architecture against requirements and constraints |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| design-and-document | @core/skills/technical-architect/design-and-document.md | system-design → adr-writing → technical-spec (execution; feasibility-analysis precedes, architecture-review follows) |
