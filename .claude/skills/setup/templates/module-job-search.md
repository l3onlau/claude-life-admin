---
paths: ["job-search/**"]
---

<!--
Module template. When generating: adapt the folder name in paths: and the
paths below if the user named their area differently, and set the fit
threshold with the user. Delete these comments in the generated file.
-->

# Job-search conventions

- NEVER invent experience, skills, or metrics in job documents — every claim
  traces to `job-search/profile/master-resume.md` or `brag-document.md`.
- NEVER automate logged-in LinkedIn (scraping, connecting, Easy Apply) — ban
  risk. Job discovery: public ATS career pages (Greenhouse/Lever/Ashby)
  first, web search second, LinkedIn last — read-only and manual, always.
- Master → variant, one-way: tailored resumes are generated FROM
  `profile/master-resume.md`. Never edit master during tailoring; new facts
  get folded back into master deliberately, in their own step.
- Fit gate before tailoring: score the posting 1–5 against
  `profile/preferences.md` and record the score in the application folder.
  Below the threshold set in preferences.md, stop after scoring.
- Application folders: `applications/YYYY-MM-DD-company-role/` containing
  `jd.md` (verbatim snapshot with URL and retrieval date — postings vanish),
  `resume.md`, and `notes.md` with frontmatter:
  `company, role, url, status, applied, last_touch, next_action`.
- Status pipeline: researching → tailoring → applied → screen → interview-N →
  offer | rejected | ghosted.
- Resume format: single column, no tables, text boxes, or images, standard
  section headers — the dominant ATS failure is a broken text layer.
- Cover letters ≤250 words, problem–solution–impact, seeded with a real
  anecdote supplied by the user. Banned: "leveraged", "spearheaded",
  "I am excited to", motivational-poster tone.
- Generated PDF/DOCX go to `artifacts/`.
- Once ~5 applications exist, maintain `applications-index.md` as a table
  GENERATED from notes.md frontmatter — regenerate it, never hand-edit it.
