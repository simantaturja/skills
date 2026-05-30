---
name: ticket-splitter
description: Split a large Jira or ClickUp ticket into smaller, independently reviewable sub-tasks with clear scope and acceptance criteria.
---

# Ticket Splitter

Use when the user asks to split, break down, decompose, or carve up a large ticket into sub-tasks.

## Process

1. **Fetch ticket** — title, description, comments, linked issues. Use MCP to fetch.
2. **Pull context only if needed** — CLAUDE.md, linked docs, referenced code paths. Ask first.
3. **Evaluate scope** — stop and say so if ticket is already a single slice: <1 day, 1 PR, single concern, single owner.
4. **Ask targeted questions** — only for gaps not in ticket + context. Interview relentlessly until you get enough info.
5. **Draft sub-tasks** using the template.
6. **Confirm assignees, priority, tags** per sub-task.
7. **Write back** to the source platform. Link sub-tasks to parent.

## Output Template

Repeat per sub-task. Number them.

```
### Sub-task N: [Action + Object]

**Description:** 1–2 sentences.

**Acceptance Criteria:**
- [ ] Given [context] / When [action] / Then [outcome]

**Dependencies:** (optional — list other sub-task numbers)
```

## Rules

- One question per turn. Wait for answer.
- Never ask for info already in ticket + context.
- Each sub-task must be independently mergeable, or declare its dependency.
- No sub-task larger than parent's hardest slice — if one stays huge, split again.
- Each subtask should have a clear outcome and easily reviewable scope.

## Usage

**User:** Break down FTF-288 into sub-tasks. / Split this ClickUp ticket into smaller PRs.
