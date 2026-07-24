---
name: weekly-review
description: Weekly sweep — staleness, follow-ups, tracker hygiene, and CLAUDE.md rot check
---

Run every step read-only first; propose changes before making them. Skip any
step whose folder does not exist yet.

1. Aging sweep: items in `inbox.md` older than 7 days; any task file with
   `status: active` but `updated` more than 14 days ago; folders in `projects/`
   untouched for 30 days.
2. Per-area check: for each active area folder, list items whose frontmatter
   says something should have happened by now (`due` passed, `next_action`
   stale) and draft — never send — any follow-ups into the relevant files.
3. External task system (if one is connected via MCP): list overdue and
   this-week tasks; flag divergence between it and repo state.
4. Hygiene: propose moves to `archive/`; review CLAUDE.md, CLAUDE.local.md,
   and `.claude/rules/` for rules that were violated twice, stale references,
   or contradictions, and propose prunes.
5. Output: 3 wins, 3 stalls, and a suggested top-3 focus for next week. In
   private visibility mode (see `.gitignore` first line), ground this in
   `git log --since` of the last review — history is memory there. Offer to
   commit.
