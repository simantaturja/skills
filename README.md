# skills

Personal Claude Code plugin — custom skills and agents for use in Claude Code sessions.

## Structure

```
skills/
  live/          # ready skills, grouped by category (must be in plugin.json)
    productivity/
  in-progress/   # drafts (must NOT be in plugin.json)
  deprecated/    # retired skills
agents/
  live/          # ready agents, grouped by category (must be in plugin.json)
    backend/
  in-progress/   # drafts (must NOT be in plugin.json)
  deprecated/    # retired agents
.claude-plugin/
  plugin.json    # skill + agent registry
.mcp.json        # MCP server config
```

## Skills

### Live

| Skill | Description |
|-------|-------------|
| `turja-skills:ticket-refiner` | Refine a vague Jira/ClickUp ticket — interviews user, rewrites with title, problem, scope, and acceptance criteria |
| `turja-skills:ticket-splitter` | Split a large Jira/ClickUp ticket into smaller, independently reviewable sub-tasks with clear scope and acceptance criteria |
| `turja-skills:teach-me-crazy` | Teacher persona — explains concepts clearly with engaging analogies |

### In Progress

| Skill | Description |
|-------|-------------|
| `code-review` | Code review skill (WIP) |

## Agents

### Live

| Agent | Description |
|-------|-------------|
| `turja-skills:Test Auditor — Java Spring Boot` | Read-only audit of test coverage, test quality, and architecture for a Spring Boot service — prioritized report of missing/weak tests ranked by production risk |

## Adding a Skill

1. Create `skills/in-progress/<name>/SKILL.md` with frontmatter (`name`, `description`) and instructions.
2. Test until ready.
3. Move to `skills/live/<category>/<name>/`.
4. Add entry to `.claude-plugin/plugin.json`.

## Adding an Agent

1. Create `agents/in-progress/<name>.md` with frontmatter (`name`, `description`) and instructions.
2. Test until ready.
3. Move to `agents/live/<category>/<name>.md`.
4. Add entry to the `agents` array in `.claude-plugin/plugin.json`.

## MCP Servers

| Server | Purpose |
|--------|---------|
| ClickUp | Ticket read/write for `ticket-refiner` and `ticket-splitter` |

## Usage

Open any project in Claude Code. Skills and agents registered in `plugin.json` are available automatically via the `turja-skills:` namespace.
