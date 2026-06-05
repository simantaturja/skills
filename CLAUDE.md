Skills are organized into bucket folders under skills/:

- live/ — ready skills, grouped by category subfolders (e.g. live/productivity/<skill>/)
- in-progress/ — drafts not yet ready to ship
- deprecated/ — no longer used

Every skill in live/ must have an entry in .claude-plugin/plugin.json. Skills in in-progress/ and deprecated/ must not appear in plugin.json.

When a skill moves between buckets (e.g. in-progress → live), update plugin.json and the README skill tables to match.
