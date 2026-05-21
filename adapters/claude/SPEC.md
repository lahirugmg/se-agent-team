# Claude Code Adapter — Specification

See [GETTING-STARTED.md](GETTING-STARTED.md) for setup instructions, day-to-day workflows, and multi-role usage.

## Architecture Decisions

### 1A — Deployment model: whole-repo

Users clone or fork the entire repository. The adapter files at `adapters/claude/` are
copied to `.claude/agents/` within that same checkout. All `@`-import paths resolve from
the repository root, so `core/` is always present alongside the adapter files.

Do not distribute adapter files independently of the repository — the `@`-imports will
break without `core/`.

### 1B — Skill invocation: on-demand file loading

Skills are workflow documents. When a task matches a skill in the agent's SKILLS.md, the
agent reads the skill file using the Read tool and follows the workflow defined there.
Composite skills orchestrate sub-skills in sequence — the agent reads each sub-skill file
when that step begins.

There are no separate slash command files. The agent self-directs based on its SKILLS.md
index and the task it receives.

### 1C — Behavioral rules: agent.md is canonical for machines, root .md files for humans

`core/agents/*/agent.md` is the machine-readable definition each adapter imports.
Root-level `.md` files (e.g. `developer.md`, `business-analyst.md`) are the human-readable
companion documents — the narrative form of the same behavioral rules. Both must be kept
in sync when rules change. The root files are the authoring source; agent.md embeds the
rules directly for machine consumption.

### 1D — Cross-agent handoff: structured output in composite skills

Each agent's primary composite skill defines a standard handoff output. The Output section
of a composite skill specifies the artifact the next agent in the SDLC chain consumes.
This is documented in the skill file itself rather than a separate protocol document.

---

## Agent File Format

Each adapter file uses Claude Code's subagent format with YAML frontmatter:

```
---
name: <agent-name>
description: <one sentence — what this agent does and when Claude Code should spawn it>
model: claude-opus-4-7
tools: <comma-separated Claude Code tool names>
color: <color>
---
```

The body imports the agent's core definition via `@`-reference. The imported `agent.md`
contains the role definition, behavioral rules, and a pointer to SKILLS.md.

---

## Tool Mapping

Tools split into two groups. Built-in tools require no setup. MCP-backed tools require
an MCP server to be configured in the project's `.mcp.json`.

### Built-in tools (work immediately)

Declared in agent YAML frontmatter — active with no additional configuration.

| Capability | Claude Code tool | Declare in frontmatter |
|---|---|---|
| Read/write/search files | `Read`, `Write`, `Edit` | `Read, Write, Edit` |
| Shell commands, git, scripts | `Bash` | `Bash` |
| Web search | `WebSearch` | `WebSearch` |
| Fetch URLs, scrape pages | `WebFetch` | `WebFetch` |

### MCP-backed tools (require project configuration)

These require an MCP server running and declared in `.mcp.json`. The tool names that
appear in Claude Code depend on which MCP server the project uses and what it is named
in the config.

| Capability | Served by | Tool name pattern | Setup guide |
|---|---|---|---|
| GitHub / Linear / Jira issues | GitHub / Linear / Jira MCP | `mcp__<server>__<operation>` | See `MCP.md` |
| Database queries | PostgreSQL / SQLite / MySQL MCP | `mcp__<server>__query` | See `MCP.md` |
| Slack messaging | Slack MCP | `mcp__slack__post_message` | See `MCP.md` |

**Adding MCP tools to an agent:**

1. Configure the MCP server in `.mcp.json` (copy from `examples/mcp.json`)
2. Add the resulting tool names to the agent's YAML frontmatter:

```yaml
---
name: business-analyst
tools: WebSearch, Bash, mcp__github__create_issue, mcp__github__list_issues, mcp__github__get_issue
---
```

The `mcp__<server-name>__` prefix matches whatever name you gave the server in `.mcp.json`.
If you named it `"github"` in your config, the tools are `mcp__github__*`. If you named
it `"gh"`, they would be `mcp__gh__*`.

See `MCP.md` for the full catalogue of available MCP servers, their tool names, and
step-by-step setup instructions.

---

## Skill Invocation

When asked to perform a task that maps to a skill in SKILLS.md, the agent:

1. Reads the skill file using the Read tool (`@core/skills/<agent>/<skill>.md`)
2. Follows the workflow defined in that file step by step
3. Produces the output described in the skill's Output section

Composite skills orchestrate sub-skills — the agent reads each sub-skill file as that
step begins, following the same pattern.

---

## Knowledge Access

Two guideline files ship with the repo and are always available:

| File | What it contains |
|---|---|
| `core/knowledge/development-best-practices.md` | Design principles, coding standards, team conventions |
| `core/knowledge/security-guidelines.md` | Developer-facing rules for writing secure code |

All other knowledge (codebase, architecture, runbooks, metrics, requirements) is
project-specific. Agents access it using their built-in tools:

| What | How |
|---|---|
| Codebase | Read files directly; `git log`, `git diff`, `git blame` via Bash |
| Architecture docs | Read — look for `docs/`, `architecture/`, `adr/`, `design/` |
| API docs | Read — look for `openapi.yaml`, `docs/api/`, inline comments |
| Runbooks | Read — look for `runbooks/`, `ops/`, `docs/runbooks/` |
| Metrics | WebFetch or Bash — dashboard URLs or `kubectl top` |
| Requirements | Bash (`gh issue list`) or Read — tickets, PRDs, stories |

Project-specific paths should be declared in the project's `CLAUDE.md`.

---

## Agent Colours

| Agent | Color |
|---|---|
| business-analyst | yellow |
| technical-architect | purple |
| software-engineer | blue |
| qa-engineer | green |
| security-engineer | red |
| platform-engineer | orange |
| sre | cyan |
| technical-writer | white |
