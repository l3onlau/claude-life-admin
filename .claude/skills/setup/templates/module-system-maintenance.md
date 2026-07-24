---
paths: ["system/**"]
---

<!--
Module template. When generating: fill {{shell_specifics}} from the
interview (OS + shell), and adapt the folder name in paths: if the user
named their area differently. Delete these comments in the generated file.
-->

# System-maintenance conventions

- Everything follows the framework's two-phase rule: audit (read-only) →
  report → approval → execute. The report IS the approval interface.
- Reports: `system/reports/YYYY-MM-DD-<topic>.md` — a findings table (item,
  size/impact, risk, recommendation) plus an empty `## Approved actions`
  section the user fills in. Execute ONLY items listed there.
- Runbooks: `system/runbooks/<name>.md` — reusable read-only discovery
  checklists (disk usage by folder, temp/cache sizes, startup apps, pending
  updates, disk health). Runbooks are data; never embed cleanup commands in
  them.
- Every executed action gets a dated entry in `system/maintenance-log.md`
  (what, why, result, space reclaimed) in the same session.
- Without an explicit request, never touch: registry or system config
  stores, drivers, disk encryption or restore settings, other users'
  folders.
- {{shell_specifics — e.g. "Discovery uses read-only PowerShell Get-*
  cmdlets" or the macOS/Linux equivalents}}
