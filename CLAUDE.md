Skills are organized into bucket folders under skills/, agents under agents/. Both use the same buckets:

- live/ — ready, grouped by category subfolders (e.g. skills/live/productivity/<skill>/, agents/live/backend/<agent>.md)
- in-progress/ — drafts not yet ready to ship
- deprecated/ — no longer used

Every skill and agent in live/ must have an entry in .claude-plugin/plugin.json (skills in the "skills" array, agents in the "agents" array). Items in in-progress/ and deprecated/ must not appear in plugin.json.

Skills are directories containing SKILL.md; agents are single .md files with name/description frontmatter.

When a skill or agent moves between buckets (e.g. in-progress → live), update plugin.json and the README tables to match.
