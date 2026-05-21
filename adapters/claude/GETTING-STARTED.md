# Getting Started — Claude Code Adapter

This guide is for a developer adopting the playbook in a real project using Claude Code. It covers initial setup, day-to-day workflows, multi-role usage (one developer, many hats), and customizing the knowledge files for your team.

---

## How the Adapter Works

Agent files in `.claude/agents/` import from `core/` using `@`-references. Those references resolve from the repository root — the directory where Claude Code is running. This means `core/` must be present at the root of your working tree alongside `.claude/`.

---

## Setup

### Option A — Fork this repo (recommended for new projects)

Fork or clone this repository. Your project code lives inside the same checkout.

```
your-project/          ← repo root (fork of software-company-skills)
  core/                ← playbook core (already here)
  adapters/            ← playbook adapters (already here)
  .claude/
    agents/            ← copy adapters/claude/ here
  src/                 ← your project code
  CLAUDE.md            ← your project instructions (create this)
  .mcp.json            ← optional MCP config (copy from adapters/claude/examples/mcp.json)
```

Steps:
1. Fork or clone this repo.
2. Copy `adapters/claude/` into `.claude/agents/`.
3. Create a `CLAUDE.md` at the repo root (see [Writing Your CLAUDE.md](#writing-your-claudemd) below).
4. Optionally copy `adapters/claude/examples/mcp.json` to `.mcp.json` and configure the servers you need.

### Option B — Add as a submodule to an existing project

Add this repo as a Git submodule, then symlink `core/` to the project root so `@`-import paths resolve correctly.

```
your-project/
  skills/              ← submodule: software-company-skills
    core/
    adapters/
  core -> skills/core  ← symlink so @core/... resolves from project root
  .claude/
    agents/            ← copy skills/adapters/claude/ here
  CLAUDE.md
```

Steps:
1. `git submodule add <repo-url> skills`
2. `ln -s skills/core core`
3. `cp -r skills/adapters/claude/ .claude/agents/`
4. Add `core` symlink to `.gitignore` or commit it depending on team preference.

> If you later update the submodule (`git submodule update --remote`), re-copy the adapter files to pick up any changes.

---

## Writing Your CLAUDE.md

`CLAUDE.md` is how you give agents project-specific context. It tells agents where things live in *your* repository — architecture docs, runbooks, dashboards, tickets. Without it, agents fall back to pattern-matching common directory names.

Minimum useful CLAUDE.md:

```markdown
# Project: <name>

## Architecture
- Design docs: docs/architecture/
- ADRs: docs/adr/
- API spec: docs/openapi.yaml

## Requirements
- Issues: GitHub — use `gh issue list` and `gh issue view <n>`
- PRDs: docs/product/

## Operations (SRE / DevOps)
- Runbooks: docs/runbooks/
- Dashboards: <url-to-grafana-or-datadog>
- Alerts: <url-to-alerting-console>
- On-call: <pagerduty-or-opsgenie-url>

## Testing
- Unit tests: src/**/__tests__/
- Integration tests: tests/integration/
- Run tests: `npm test` (or equivalent)

## Deployment
- Infrastructure: infra/
- CI config: .github/workflows/
- Staging: <staging-env-url>
- Production: <prod-env-url>
```

Add only paths that exist. Agents use this to locate resources rather than searching blindly.

---

## Multi-Role Usage

Most developers work across more than one role in the same codebase — software engineer for feature work, SRE during incidents, or security engineer during a compliance review. All eight agents are installed at once; you invoke the right one for the task.

Claude Code auto-selects an agent based on your request and each agent's `description:` field. You can also invoke an agent explicitly:

```
@software-engineer implement the payment retry logic in src/payments/
@sre we have a latency spike on the checkout service, help me investigate
@security-engineer review the authentication changes in this PR
```

### Multi-Role CLAUDE.md

When you wear multiple hats, include sections in your CLAUDE.md for each role's resources. Agents read only what's relevant to their task.

```markdown
## Development
- Architecture: docs/architecture/
- API spec: docs/openapi.yaml

## Operations
- Runbooks: docs/runbooks/
- Metrics: https://grafana.example.com/d/checkout-latency
- Alerts: https://alerts.example.com

## Security
- Threat models: docs/security/threat-models/
- Compliance requirements: docs/security/compliance.md
```

An SRE agent working an incident will read the Operations section and ignore the rest. A software engineer implementing a feature will read Development. Neither needs the other's resources loaded.

---

## Role Selection Guide

Not sure which agent to invoke? Use this table.

| I want to… | Use this agent | Key skill(s) |
|---|---|---|
| Implement a feature end-to-end | `software-engineer` | `ship-feature` (composite) |
| Review a PR | `software-engineer` | `code-review` |
| Verify AI-generated code before merging | `software-engineer` | `agent-output-review` |
| Debug a production or test defect | `software-engineer` | `debugging` |
| Refactor a module | `software-engineer` | `refactoring` |
| Assess and reduce tech debt | `software-engineer` | `tech-debt` |
| Update a dependency safely | `software-engineer` | `dependency-update` |
| Design a new system or service | `technical-architect` | `system-design` |
| Write an Architecture Decision Record | `technical-architect` | `adr-writing` |
| Review existing architecture | `technical-architect` | `architecture-review` |
| Write test plans and tests | `qa-engineer` | `test-writing`, `feature-validation` (composite) |
| File or triage a bug report | `qa-engineer` | `bug-report` |
| Run a security review | `security-engineer` | `security-review` (composite) |
| Model threats for a new feature | `security-engineer` | `threat-modeling` |
| Audit dependencies for CVEs | `security-engineer` | `dependency-vulnerability` |
| Design an internal developer platform | `platform-engineer` | `idp-design` |
| Define a golden path for teams | `platform-engineer` | `golden-path` |
| Design a CI/CD pipeline | `platform-engineer` | `pipeline-design` |
| Write infrastructure as code | `platform-engineer` | `infrastructure-as-code` |
| Ship a platform capability end-to-end | `platform-engineer` | `build-platform` (composite) |
| Measure developer experience | `platform-engineer` | `developer-experience` |
| Respond to an incident | `sre` | `incident-to-action` (composite) |
| Set up monitoring or alerting | `sre` | `observability`, `alerting` |
| Write a post-mortem | `sre` | `post-mortem` |
| Write or update a runbook | `sre` | `runbook` |
| Write or update API documentation | `technical-writer` | `api-docs` |
| Produce a release changelog | `technical-writer` | `document-release` (composite) |
| Gather requirements for a feature | `business-analyst` | `requirements-to-prd` (composite) |
| Write a PRD | `business-analyst` | `prd-writing` |
| Plan a sprint | `business-analyst` | `sprint-planning` |

### Composite skills

Composite skills orchestrate several atomic skills in sequence. Invoke them when you want the full workflow rather than a single step:

- `ship-feature` → spec-writing → code-review → test-writing
- `feature-validation` → test-planning → test-writing → exploratory-testing → bug-report
- `security-review` → threat-modeling → security-audit → vulnerability-assessment
- `build-platform` → idp-design → golden-path → infrastructure-as-code → containerization → pipeline-design → deployment → platform-observability
- `incident-to-action` → incident-response → root-cause-analysis → post-mortem
- `requirements-to-prd` → requirements-gathering → user-story → prd-writing

---

## Customizing the Knowledge Files

`core/knowledge/` has two files that agents consult during execution. They ship as templates — you fill them in with your team's actual standards.

### development-best-practices.md

Add your team's agreed conventions in the **Coding Standards** section. Common things to add:

- Language or framework conventions ("we use async/await, never callbacks")
- Naming conventions ("React components are PascalCase, utilities are camelCase")
- Test strategy ("unit test pure functions, integration test DB queries, skip e2e for internal services")
- PR norms ("PRs target `main`, one logical change per PR, squash before merge")
- Commit message format ("`type(scope): message` — types are feat, fix, chore, docs, test")
- Error handling ("always return typed errors from service boundaries, never throw strings")
- State management conventions (if applicable)

Example addition:

```markdown
## Team Conventions

### Commit Format
`type(scope): short description` — types: feat, fix, chore, docs, test, refactor.
Body is optional. Reference the issue: `Closes #123`.

### Branch Naming
`<type>/<short-description>` — e.g. `feat/payment-retry`, `fix/auth-timeout`.

### Testing Strategy
Unit tests for all pure functions. Integration tests for database queries and external API calls.
No e2e tests for internal services — integration coverage is sufficient.
```

### security-guidelines.md

Add rules specific to your stack and threat model. Common things to add:

- Auth and session rules ("JWT expiry max 1 hour, refresh tokens rotated on use")
- Data classification ("PII fields are encrypted at rest using AES-256")
- Input validation rules ("all user input sanitized before DB write")
- Secrets policy ("no secrets in code or logs — use environment variables or secrets manager")
- Dependency policy ("no packages with known critical CVEs in `npm audit`")

Agents read these files during code review, security audits, and any task where security is relevant. Keep them concise and actionable — long lists of vague rules are ignored.

---

## Day-to-Day Workflow

**Starting a feature:**
```
@software-engineer I need to add rate limiting to the /api/payments endpoint. 
Start from the spec and take it through to a reviewable PR.
```
The agent runs the `ship-feature` composite skill: writes a spec, implements, reviews its own output.

**Reviewing a PR:**
```
@software-engineer review PR #142 — focus on the auth middleware changes
```

**During an incident:**
```
@sre p95 latency on checkout jumped from 80ms to 4s at 14:30 UTC. 
Last deploy was 13:45. Help me investigate.
```
The agent follows `incident-to-action`: triage → root cause → post-mortem draft.

**After the incident:**
```
@sre the incident is resolved. Write the post-mortem from our investigation notes.
```

**Switching roles mid-task:** Just change the agent you invoke. There is no mode or session to switch — each `@agent` call is independent. Your CLAUDE.md provides the shared context both agents read.
