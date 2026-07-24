---
name: setup
description: Interviews the user about their life-admin workflow and generates the gitignored personal layer — CLAUDE.local.md, inbox.md, and optional domain modules. Use when the user asks to set up, initialize, personalize, or onboard this workspace, or when CLAUDE.local.md is missing.
argument-hint: "[module]"
---

# Setup — generate the personal layer

This workspace splits into a committed generic framework (CLAUDE.md,
settings, skills) and a gitignored personal layer. This skill generates the
personal layer: `CLAUDE.local.md`, `inbox.md`, and optional domain modules
in `.claude/rules/`. It never edits committed framework files.

## Before anything

1. If `$ARGUMENTS` names a module (e.g. `job-search`), skip to **Modules**.
2. If `CLAUDE.local.md` already exists, do not overwrite it. Ask whether to:
   review and improve it, add a module, or start fresh (start fresh requires
   explicit confirmation).
3. Otherwise print a short plain-text primer: what will be generated, that
   every generated file is gitignored (stays on this machine, never published),
   and that the interview takes about five minutes. Then interview.

## Interview

Use AskUserQuestion, ONE question per call — later questions depend on
earlier answers. Give every option a one-line description. Never mark an
option "(Recommended)": these are questions about the user's life, not best
practices. The tool adds an "Other" free-text option automatically.

1. **Name and address.** How they want to be addressed, plus (open) anything
   Claude should know about how they like to work.
2. **Machine and shell.** Detect the OS and shell yourself first; confirm
   rather than ask. Record only quirks that change behavior (e.g. Windows
   PowerShell 5.1: no `&&`, no ternary).
3. **Active life areas** (multiSelect): life admin/chores, machine
   maintenance, personal projects, plus free text for others. Only areas
   selected here go in CLAUDE.local.md; folders materialize on first use.
4. **Connected tools.** Check which MCP servers are actually available in
   this session (task managers, web search, browser automation, etc.).
   Propose a one-line routing for each (what it owns, when to use it) and
   confirm. If none are connected, skip — never invent tool routing.
5. **Working style.** How proactive should Claude be (chief-of-staff who
   pushes back vs. does what is asked), commit cadence, anything to never do.
6. **Optional modules.** Offer each template in `templates/` whose domain
   matched an active area or was asked for (currently: job-search,
   system-maintenance, finance). Generate only what the user opts into.

## Generate

1. Draft `CLAUDE.local.md` from `templates/claude-local.md`; a filled example
   is in `examples/sample-claude-local.md`. Keep it under 40 lines — only
   facts that change Claude's behavior. Show the complete draft as normal
   text and gate on approval before writing anything.
2. Write `inbox.md`: a short capture header plus any actionable items that
   surfaced during the interview.
3. For each opted-in module, generate `.claude/rules/<module>.md` from its
   template, adapted to the interview answers.
4. If tool routing was confirmed, offer to add the read-only tools of those
   MCP servers to the `allow` list in `.claude/settings.local.json` so they
   stop prompting. Write tools stay on ask.
5. Verify privacy: run `git check-ignore` on every file written; if any file
   is NOT ignored, stop and warn loudly before continuing.
6. Summarize what was written where, and suggest running /weekly-review once
   a week.

## Modules

Templates in `templates/`:

- `module-job-search.md` — honest-resume rules, application pipeline,
  fit-gate, ATS formatting conventions.
- `module-system-maintenance.md` — audit → report → approve → execute
  machine maintenance, runbooks, maintenance log.
- `module-finance.md` — privacy-tiered money tracking: sensitive documents
  in `private/`, aggregates and subscription inventory in tracked files.

Add one later with `/setup <module>`. Adapt the template to the user's
answers and area folder names; write to `.claude/rules/<module>.md`
(gitignored). Modules use `paths:` frontmatter so they only load when
working in matching folders.
