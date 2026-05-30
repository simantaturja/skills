---
name: ticket-refiner
description: Refine a vague Jira or ClickUp ticket by interviewing the user and rewriting it with a clear title, problem statement, scope, and acceptance criteria.
---

# Ticket Refiner

Use when the user asks to refine, rewrite, clarify, or improve a ticket.

## Process

1. **Fetch ticket** — title, description, comments, linked issues.
2. **Pull context if necessary** — CLAUDE.md, linked docs, related code if paths are mentioned. Ask before accessing since it's not always needed.
3. **Evaluate completeness** — if ticket is already well-defined, say so and stop.
4. **Identify gaps** — problem statement, scope, acceptance criteria, edge cases, non-goals.
5. **Ask targeted questions** — one per turn, only for gaps that cannot be inferred from ticket + context.
6. **Draft ticket** using the output template below.
7. **Confirm assignee + priority + tag** — Ask whom to assign and what priority level and tags to set.
8. **Write ticket back** to the platform.

## Output Template

```
**Title:** [Action + Object + Context]

**Problem:** 2–3 sentences. What breaks or is missing, and who is affected.

**Scope:**
- **In scope:** What will be included in the solution.
- **Out of scope:** What will not be included, to prevent scope creep.

**Acceptance Criteria:**
- [ ] Given [context] / When [action] / Then [outcome]

**Edge Cases:** (optional)

**Dependencies:** (optional)
```

## Rules

- Ask one question per turn. Wait for response before asking next.
- Never ask for information already available in the ticket or context.
- If user provides incomplete info, ask one targeted follow-up.

## Usage

**User:** Can you refine this ticket for me? [link] or Rewrite the clickup ticket FTF-288.
