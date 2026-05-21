# Claude Code — MCP Tool Configuration

This document explains which capabilities require MCP servers, which servers are available
for each, and how to configure them. It is a living catalogue — add entries as your team
adopts new MCP servers.

---

## Quick orientation

Agent tool access splits into two groups:

### Group A — Built-in (zero configuration)

These map directly to Claude Code built-in tools and are declared in the agent's YAML
frontmatter. They work the moment you copy the adapter files into `.claude/agents/`.

| Capability | Claude Code built-ins |
|---|---|
| File reads, writes, edits | `Read`, `Write`, `Edit` |
| Shell commands, git, scripts | `Bash` |
| Web search | `WebSearch` |
| Fetch URLs, scrape pages | `WebFetch` |

### Group B — MCP-backed (requires configuration)

These require an MCP server to be running and declared in your project's `.mcp.json`.
The specific server you choose is a project decision — the framework lists the options.

| Abstract tool | What it does | Agents that use it |
|---|---|---|
| issue-tracker | Read/write issues, PRs, tickets | business-analyst, technical-architect |
| database | Query structured data stores | security-engineer, platform-engineer, sre |
| communication | Send messages and notifications | business-analyst, sre |

---

## How to configure an MCP-backed tool

**Step 1** — Choose an MCP server from the catalogue below.

**Step 2** — Add it to `.mcp.json` in your project root. See `examples/mcp.json` for a
complete file you can copy and edit.

**Step 3** — Add the MCP tool names to the relevant agent files in `.claude/agents/`. Each
agent file has a comment showing where to add them.

```yaml
# In .claude/agents/software-engineer.md
---
name: software-engineer
tools: Read, Write, Edit, Bash, WebSearch
# Add MCP tools below, e.g.:
# mcp__github__create_issue, mcp__github__get_issue
---
```

**Step 4** — Add secrets to your environment (never in `.mcp.json` directly). The examples
below use environment variable references — set those in your shell or CI secrets store.

---

## issue-tracker

Agents that use it: `business-analyst`, `technical-architect`

Capabilities needed: read issues, search issues, create issues, create PRs, add comments.

---

### Option 1 — GitHub (recommended for GitHub-hosted projects)

**MCP server:** `@modelcontextprotocol/server-github`
**Source:** https://github.com/modelcontextprotocol/servers/tree/main/src/github

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

Tool names to add to agent frontmatter:
```
mcp__github__create_issue
mcp__github__get_issue
mcp__github__list_issues
mcp__github__update_issue
mcp__github__add_issue_comment
mcp__github__create_pull_request
mcp__github__get_pull_request
mcp__github__list_pull_requests
mcp__github__merge_pull_request
mcp__github__search_repositories
mcp__github__search_code
```

Required token scopes: `repo` (for private repos), `public_repo` (for public repos).

---

### Option 2 — Linear (for teams using Linear)

**MCP server:** `@modelcontextprotocol/server-linear` *(community)*
**Source:** https://github.com/modelcontextprotocol/servers

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "linear": {
      "command": "npx",
      "args": ["-y", "@linear/mcp-server"],
      "env": {
        "LINEAR_API_KEY": "${LINEAR_API_KEY}"
      }
    }
  }
}
```

Tool names to add to agent frontmatter:
```
mcp__linear__create_issue
mcp__linear__get_issue
mcp__linear__list_issues
mcp__linear__update_issue
mcp__linear__search_issues
```

---

### Option 3 — Jira (for teams using Atlassian)

**MCP server:** `@modelcontextprotocol/server-atlassian` *(community)*
**Source:** https://github.com/sooperset/mcp-atlassian

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "jira": {
      "command": "npx",
      "args": ["-y", "@sooperset/mcp-atlassian"],
      "env": {
        "JIRA_URL": "${JIRA_URL}",
        "JIRA_EMAIL": "${JIRA_EMAIL}",
        "JIRA_API_TOKEN": "${JIRA_API_TOKEN}"
      }
    }
  }
}
```

Tool names to add to agent frontmatter:
```
mcp__jira__create_issue
mcp__jira__get_issue
mcp__jira__search_issues
mcp__jira__update_issue
mcp__jira__add_comment
```

---

## database

Agents that use it: `security-engineer`, `platform-engineer`, `sre`

Capabilities needed: run read queries for investigation; run write queries (with confirmation) for operational tasks.

---

### Option 1 — PostgreSQL

**MCP server:** `@modelcontextprotocol/server-postgres`
**Source:** https://github.com/modelcontextprotocol/servers/tree/main/src/postgres

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${DATABASE_URL}"]
    }
  }
}
```

`DATABASE_URL` format: `postgresql://user:password@host:5432/dbname`

Tool names to add to agent frontmatter:
```
mcp__postgres__query
```

The `query` tool accepts any SQL. For production use, connect with a read-only database
user by default. Create a separate read-write user for operational tasks that require
data changes, and document which agents receive that user's credentials.

---

### Option 2 — SQLite (for local or embedded databases)

**MCP server:** `@modelcontextprotocol/server-sqlite`
**Source:** https://github.com/modelcontextprotocol/servers/tree/main/src/sqlite

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "sqlite": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sqlite", "--db-path", "${SQLITE_DB_PATH}"]
    }
  }
}
```

Tool names to add to agent frontmatter:
```
mcp__sqlite__read_query
mcp__sqlite__write_query
mcp__sqlite__list_tables
mcp__sqlite__describe_table
mcp__sqlite__create_table
mcp__sqlite__append_insight
```

---

### Option 3 — MySQL / MariaDB

**MCP server:** `mysql-mcp-server` *(community)*
**Source:** https://github.com/benborla/mcp-server-mysql

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": ["-y", "mcp-server-mysql"],
      "env": {
        "MYSQL_HOST": "${MYSQL_HOST}",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "${MYSQL_USER}",
        "MYSQL_PASSWORD": "${MYSQL_PASSWORD}",
        "MYSQL_DATABASE": "${MYSQL_DATABASE}"
      }
    }
  }
}
```

Tool names to add to agent frontmatter:
```
mcp__mysql__query
mcp__mysql__execute
mcp__mysql__list_tables
mcp__mysql__describe_table
```

---

## communication

Agents that use it: `business-analyst`, `sre`

Capabilities needed: send messages to channels, post status updates, notify stakeholders.

---

### Option 1 — Slack

**MCP server:** `@modelcontextprotocol/server-slack`
**Source:** https://github.com/modelcontextprotocol/servers/tree/main/src/slack

Add to `.mcp.json`:
```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "${SLACK_BOT_TOKEN}",
        "SLACK_TEAM_ID": "${SLACK_TEAM_ID}"
      }
    }
  }
}
```

To get a `SLACK_BOT_TOKEN`:
1. Create a Slack app at https://api.slack.com/apps
2. Add OAuth scopes: `channels:read`, `chat:write`, `users:read`
3. Install the app to your workspace and copy the Bot User OAuth Token

Tool names to add to agent frontmatter:
```
mcp__slack__list_channels
mcp__slack__post_message
mcp__slack__reply_to_thread
mcp__slack__get_channel_history
mcp__slack__get_thread_replies
mcp__slack__get_users
mcp__slack__get_user_profile
```

**Important:** Messages sent via MCP are visible to the entire channel. The SRE and
Business Analyst agents treat the `communication` tool as a write-to-shared-space
operation — always confirm the target channel before posting during an incident.

---

### Option 2 — No communication tool (acceptable default)

If your team does not need agents to post messages autonomously, omit the `communication`
tool entirely. The `business-analyst` and `sre` agents will still function fully — they
will produce stakeholder communications as document outputs rather than sending them
directly.

This is the safer default. Add Slack when you have established guardrails around which
channels agents can post to and under what conditions.

---

## Adding a new MCP server to this catalogue

When your team adopts a new MCP server, add an entry to the relevant section above:

1. Name the abstract tool it serves (`issue-tracker`, `database`, or `communication`)
2. Link to the MCP server source
3. Show the `.mcp.json` configuration block with environment variable placeholders (never real values)
4. List the tool names that appear in Claude Code once the server is configured
5. Note any credential setup steps

Keep real credentials out of this file. All secrets are environment variable references.
