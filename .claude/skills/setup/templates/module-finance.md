---
paths: ["finance/**"]
---

<!--
Module template. When generating: fill {{currency_and_locale}} and adapt
the folder name in paths: if needed. Delete these comments in the
generated file.
-->

# Finance conventions

- Privacy tiering is the whole game: statements, tax documents, and
  anything bearing account or card numbers go to `private/` (Claude never
  reads it). Tracked files carry categories, dates, merchant names, and
  amounts only — NEVER account numbers, card numbers, or credentials, in
  any visibility mode.
- `finance/subscriptions.md` — one table: service, cost, billing cycle,
  renewal date, cancel-by date, last reviewed. Swept during /weekly-review.
- Recurring obligations (bills, renewals) belong in the external task
  system if one is connected; the repo keeps the inventory and the history.
- Answer money questions from tracked aggregates. If the answer would
  require a document in `private/`, ask the user to extract the numbers
  themselves.
- {{currency_and_locale}}
