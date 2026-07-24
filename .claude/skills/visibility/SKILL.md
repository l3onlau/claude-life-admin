---
name: visibility
description: Switches the workspace between public mode (only framework files tracked — safe to publish) and private mode (life content versioned too — git history becomes memory). Use when the user wants to share or publish the repo, make it private, commit more of their content, or check whether the repo is safe to publish.
argument-hint: "[public|private|status]"
---

# Visibility — govern what git is allowed to see

Two modes, defined by which `.gitignore` is active. The templates live in
`templates/`; the first line of the active `.gitignore` names the current
mode.

- **public** (default): fail-closed whitelist — only framework files can be
  committed. Safe to attach a public remote.
- **private**: life content (area folders, `inbox.md`, `CLAUDE.local.md`,
  `.claude/rules/`) is versioned too, so git history becomes memory.
  `private/`, secrets, `artifacts/`, `tmp/`, and
  `.claude/settings.local.json` stay ignored in BOTH modes.

`$ARGUMENTS` is `public`, `private`, or `status`. With no argument, report
status and ask which mode the user wants.

## status

Report: current mode (first line of `.gitignore`), `git remote -v`, and the
history audit result (see below). Recommend nothing unless asked.

## Switching to private

1. Check remotes first. If any remote could be public (for GitHub remotes
   verify with `gh repo view --json visibility` when available), STOP and
   warn: private mode must never feed a public remote. Proceed only after
   the user confirms the remote is private or removes it.
2. Copy `templates/gitignore-private` over `.gitignore`.
3. Show what would now be tracked (`git status --short`) and offer to commit
   the personal layer.
4. If no remote exists, suggest — do not create unasked — a PRIVATE GitHub
   remote as an off-machine backup.

## Switching to public

1. Copy `templates/gitignore-public` over `.gitignore`.
2. Re-apply ignores to the index: `git rm -r --cached .` then `git add .`
   (files stay on disk). Show the resulting status before any commit.
3. HISTORY AUDIT — the step that keeps this safe. List every path ever
   committed (`git log --all --diff-filter=A --name-only --pretty=format:`)
   and compare against the framework whitelist in the public template. If
   personal paths appear in ANY commit, say clearly:
   - This branch's HISTORY still contains personal content. Untracking does
     not remove it from history. This branch must never be pushed anywhere
     public.
   - The safe publish path is an orphan branch holding only framework files
     (`git checkout --orphan public` → commit framework → publish that),
     while the full-history branch stays private. Offer it; never rewrite
     history unasked.
4. Report "safe to publish" ONLY when the audit finds framework-only
   history.

## Rules

- Never push, change a remote's visibility, or rewrite history without
  explicit confirmation — show every irreversible step before taking it.
- If the current `.gitignore` matches neither template, the mode is unknown:
  show the diff against the nearest template and ask before overwriting.
