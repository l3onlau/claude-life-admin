# claude-life-admin

**A Claude Code starter for everything except code.**

A minimal workspace template for running your life admin with
[Claude Code](https://code.claude.com): chores and errands, machine
maintenance, personal projects, and an optional job-search module. Markdown
files in, useful work out — no build step, no daemon, no plugins.

The core promise: **the framework is committed, your life is gitignored.**
The same clone is both a publishable repo and your private working
workspace, and the two can never mix.

## Why this one

- **Interview-driven setup.** `/setup` interviews you and *generates* your
  personal layer — a `CLAUDE.local.md` describing who you are, how you work,
  and which tools you use, plus optional domain modules. No hand-editing
  `YOURNAME` placeholders.
- **A real enforcement layer.** `.claude/settings.json` ships deny rules
  (Claude can never read `private/` or `.env` files, never force-pushes) and
  a fail-closed `.gitignore` where *everything is personal by default* —
  only whitelisted framework files can be committed. Instructions ask;
  permissions enforce.
- **Genuinely cross-platform.** Works on Windows (PowerShell quirks and
  long-path setup included), macOS, and Linux. Most templates in this space
  assume zsh and Homebrew.
- **Two visibility modes.** `/visibility` flips the workspace between
  publish-safe (framework only, fail-closed) and private-journal (your life
  is versioned too — git history becomes memory), with a history audit
  guarding the road back to public.

## Quick start

Two ways in:

1. **Use this template** (green button above) — clean start, your own
   history.
2. **Clone it** — keeps the ability to `git pull` framework updates:

   ```
   git clone https://github.com/<you>/claude-life-admin my-life
   cd my-life
   ```

Then:

```
claude
/setup
```

`/setup` runs a ~5-minute interview and generates your gitignored personal
layer. Use `/setup`, not `/init` — `/init` is Claude Code's built-in
*codebase* analyzer and will generate the wrong kind of CLAUDE.md for a
life-admin workspace.

On Windows, also run once: `git config core.longpaths true`

## Privacy model

| Committed (framework) | Gitignored (your life) |
| --- | --- |
| `CLAUDE.md` — generic conventions | `CLAUDE.local.md` — who you are, your tools |
| `.claude/settings.json` — enforcement | `.claude/settings.local.json` — your allowlist |
| `.claude/skills/` — setup, weekly-review, visibility | `.claude/rules/` — your generated modules |
| `README`, `LICENSE`, git config | `inbox.md` and every area folder |
|  | `artifacts/`, `tmp/`, `private/` |

The `.gitignore` is a whitelist: `/*` ignores everything, then framework
files are explicitly re-included. A new file you create anywhere is
untracked by default — publishing your workspace can never leak your life.

That table describes the default **public** mode. If you keep your
workspace private, run `/visibility private` to version your life content
too — weekly reviews then get git history as memory. `private/`, secrets,
`artifacts/`, and `tmp/` stay ignored in both modes, and switching back to
public runs a history audit before ever calling the repo publishable.

## How it works day to day

- **Capture** anything into `inbox.md`; ask Claude to process it and each
  item gets filed to its home and removed.
- **Areas** are plain folders (`admin/`, `system/`, `projects/<name>/`)
  created on first use — structure materializes, it is never pre-built. One
  markdown file per matter, with YAML frontmatter for status.
- **`artifacts/`** holds finished generated deliverables (exports, PDFs);
  **`tmp/`** is disposable scratch; **`private/`** is off-limits to Claude
  entirely.
- **`/weekly-review`** sweeps for stale items, drafts follow-ups, proposes
  archive moves — and reviews the instruction files themselves for rot.
- **Modules** add domain conventions on demand — `/setup job-search`,
  `/setup system-maintenance`, `/setup finance` — and load only when you
  work in matching folders.

## Philosophy

Every documented system in this niche that died, died of overfit: shipped
structure for an aspirational self, rotting instructions, fifty skills
nobody ran. So this template ships almost nothing: three skills, one
config, one CLAUDE.md under 80 lines. Every line must earn its place;
specifics are generated for *you* on demand, never shipped for everyone.
Safety-critical behavior lives in permissions, which enforce, rather than
instructions, which request.

This template is a best-effort personal artifact, not a supported product:
issues and ideas are welcome, fast responses are not guaranteed.

## Extending

- New domain conventions → `.claude/rules/<topic>.md` with `paths:`
  frontmatter (loads only when relevant).
- New procedures → `.claude/skills/<name>/SKILL.md`.
- Corrected Claude twice on the same thing? It should propose a one-line
  edit to CLAUDE.md — that feedback loop is in the framework.

## License

Not affiliated with Anthropic. Claude is a trademark of Anthropic, PBC.

MIT — see [LICENSE](LICENSE).
