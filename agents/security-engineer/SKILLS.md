# Security Engineer — Available Skills

Skills are invoked on demand. Each skill file is self-contained and can be composed into larger workflows. Every workflow follows three phases: **Pre-work** (model threats before auditing), **Execution** (audit and assess vulnerabilities), **Post-work** (verify compliance and sign off).

## Pre-work Skills

| Skill | File | When to use |
|---|---|---|
| threat-modeling | @core/skills/security-engineer/threat-modeling.md | Identify assets, threat actors, attack surface, and trust boundaries for a system |

## Execution Skills

| Skill | File | When to use |
|---|---|---|
| security-audit | @core/skills/security-engineer/security-audit.md | Review a system, codebase, or configuration for security vulnerabilities |
| vulnerability-assessment | @core/skills/security-engineer/vulnerability-assessment.md | Assess and prioritise known vulnerabilities in a system or dependency set |
| dependency-vulnerability | @core/skills/security-engineer/dependency-vulnerability.md | Identify and triage security vulnerabilities in project dependencies |

## Post-work Skills

| Skill | File | When to use |
|---|---|---|
| compliance-review | @core/skills/security-engineer/compliance-review.md | Assess a system against a compliance framework (SOC 2, GDPR, PCI-DSS, etc.) to verify findings are resolved and standards are met |

## Composite Workflows

Composite skills chain pre-work, execution, and post-work into a single invocable workflow.

| Skill | File | Phase chain |
|---|---|---|
| security-review | @core/skills/security-engineer/security-review.md | threat-modeling (pre-work) → security-audit → vulnerability-assessment (execution; compliance-review follows as post-work) |
