# skills

Personal Claude Code plugin — custom skills for use in Claude Code sessions.

## Structure

```
skills/
  live/          # ready skills (must be in plugin.json)
  in-progress/   # drafts (must NOT be in plugin.json)
  deprecated/    # retired skills
.claude-plugin/
  plugin.json    # skill registry
.mcp.json        # MCP server config
```

## Skills

### Live

| Skill | Description |
|-------|-------------|
| `turja-skills:ticket-refiner` | Refine a vague Jira/ClickUp ticket — interviews user, rewrites with title, problem, scope, and acceptance criteria |

### In Progress

| Skill | Description |
|-------|-------------|
| `code-review` | Code review skill (WIP) |

## Adding a Skill

1. Create `skills/in-progress/<name>/SKILL.md` with frontmatter (`name`, `description`) and instructions.
2. Test until ready.
3. Move to `skills/live/<category>/<name>/`.
4. Add entry to `.claude-plugin/plugin.json`.

## MCP Servers

| Server | Purpose |
|--------|---------|
| ClickUp | Ticket read/write for `ticket-refiner` |

## Usage

Open any project in Claude Code. Skills registered in `plugin.json` are available automatically via the `turja-skills:` namespace.
