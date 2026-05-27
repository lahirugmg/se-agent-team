# Roles Matrix

The team is eight roles, each scoped narrowly so that no responsibility is shared and no responsibility is missing. This document is the single-page reference for *who owns what*.

## Summary

| Role | Owns | Cannot Decide |
|---|---|---|
| Business Analyst | Requirements, user stories, PRDs, scope, prioritisation | How something is built; whether it is secure; how it is operated |
| Technical Architect | System design, ADRs, technical specs, feasibility | What to build; whether the spec was implemented correctly |
| Software Engineer | Implementation, debugging, refactoring, code review | What to build; whether the system meets reliability targets |
| QA Engineer | Test plans, test execution, bug reports, sign-off verdict | Whether a defect should be fixed; how it gets fixed |
| Security Engineer | Threat models, audits, vulnerability triage, compliance verdict | Whether to ship; how to architect around a risk |
| Platform Engineer | Internal developer platform, golden paths, CI/CD, IaC standards | Application logic; what product teams build on top |
| SRE | SLOs, observability, incident response, post-mortems, toil reduction | Feature scope; architectural rewrites |
| Technical Writer | API docs, user guides, runbooks, changelogs, onboarding | The behaviour itself; whether to release |

## Phase Responsibilities

What each role does at each phase of its own work.

| Role | Pre-work | Execution | Post-work |
|---|---|---|---|
| Business Analyst | Interview stakeholders, refine ideas, gather requirements, map processes | Write user stories, PRDs, roadmap items | Estimate, sprint-plan, capture sign-off |
| Technical Architect | Feasibility analysis against hard constraints | System design, ADRs, technical specification | Architecture review against requirements |
| Software Engineer | Spec-writing, tech-debt assessment | Incremental implementation, debugging, refactoring, migrations, perf work | Code review, simplification, agent-output review |
| QA Engineer | Test planning, risk identification | Test writing, browser testing, performance testing, exploratory testing | Defect reports, sign-off verdict (PASS / PASS WITH CONDITIONS / FAIL) |
| Security Engineer | Threat modeling (STRIDE) | Security audit, vulnerability assessment, dependency-vulnerability triage | Compliance review, accepted-risk register |
| Platform Engineer | IDP design, golden-path definition | Infrastructure-as-code, containerization, pipeline design, build optimisation | Deployment, platform observability, developer-experience measurement |
| SRE | SLO definition, observability setup, alerting, capacity planning, runbooks | Incident response, root-cause analysis | Post-mortem with owned action items |
| Technical Writer | Read implementation, identify reader and task | Write API docs, user guides, runbooks, onboarding, changelogs | Verify by following the doc on a clean system; communicate to stakeholders |

## Handoffs

Each row is an artifact that flows from one role to another. The receiving role cannot start without it.

| From → To | Artifact | What it must contain |
|---|---|---|
| Business Analyst → Technical Architect | PRD + user stories | Business problem, actors, acceptance criteria, hard constraints, out-of-scope list |
| Business Analyst → Software Engineer | User stories with acceptance criteria | A testable outcome the engineer can implement against |
| Technical Architect → Software Engineer | Technical spec + ADRs | Component design, interfaces, sequence flows, decisions with rationale |
| Technical Architect → Security Engineer | System design + trust boundaries | What components exist, how data flows, where trust changes |
| Software Engineer → QA Engineer | Implementation + commit history | What changed, where, against which spec cases |
| Software Engineer → Technical Writer | Implementation diff + spec | What the system now does; what the user-visible change is |
| QA Engineer → Software Engineer | Bug reports | Reproducible steps, expected vs actual, severity |
| Security Engineer → Software Engineer | Findings with severity, exploit path, fix guidance | What is vulnerable, why, how an attacker exploits it, how to remediate |
| Platform Engineer → Software Engineer | Golden path documentation | Supported deploy / CI / IaC workflow with self-service interface |
| Software Engineer → Platform Engineer | Service manifest | Service definition that fits the golden path |
| Platform Engineer → SRE | Deployable artifact + pipeline records | What was shipped, how to roll back, what telemetry is wired in |
| SRE → Software Engineer | Post-mortem action items | Root cause, contributing factors, owned and dated remediation |
| All roles → Technical Writer | Change context | What changed, why, who needs to know |
| Technical Writer → Business Analyst | Stakeholder communication | Impact-focused summary for non-technical audiences |

## Boundaries

Failures of role boundary are the most common failures in human teams and AI agent teams alike. Each role's charter calls out explicitly what it does *not* decide; see the **Boundaries** section in each role file under [roles/](../roles/).

## Source of Behavior

Every role here corresponds to an orchestrator in [agents/](../agents/), with its skill set declared in `agents/<role>/SKILLS.md` and individual micro-agents under [skills/](../skills/). This file describes *scope* — what each role owns and where its work hands off; the orchestrator file describes *execution* — the behavioral rules and workflow gates the role operates under.
