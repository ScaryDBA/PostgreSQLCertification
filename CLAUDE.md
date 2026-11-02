# OAPE PostgreSQL DBA-1 Certification Prep

**Goal:** Prep Grant for the OAPE PostgreSQL DBA-1 exam via repeated practice tests, grading, and targeted study guides.

**Scope source:** https://www.oapg-edu.org/certifications/ — 8 topic areas (T1–T8):
1. Installation, Versioning & Basic Configuration
2. Connecting to PostgreSQL, Database Objects & Basic SQL
3. Roles & Privileges
4. Backup & Recovery
5. Server Architecture & Background Processes
6. MVCC & Transaction Management
7. VACUUM, ANALYZE & Autovacuum
8. Monitoring & Logging

**Version constraint:** PostgreSQL 18 only. Never include PostgreSQL 19 content — exam is scoped to v18.

## Workflow (repeat each session)

1. **Generate a practice exam:** 40 multiple-choice questions, 5 per topic, scattered (not grouped by topic). Save as `PostgreSQL_DBA1_Practice_Exam_NN.md` in this folder — question + A/B/C/D choices + blank `Answer:` line, no visible answer key. Number sequentially (02, 03, ...).
2. **Keep the answer key private only until grading** — do not save it into this folder or otherwise expose it before Grant has taken the exam. Grant fills in `Answer: X` inline in the exam file and says when he's done. This secrecy is temporary, not permanent: once grading (step 3) is complete, the key gets published as the shareable answer file in step 5 — there's no need to keep it hidden after that point.
3. **Grade:** Read his filled-in exam, compare to the key, report overall score + per-topic breakdown (X/5 per topic), and list which question numbers were missed with a short explanation of the correct answer.
4. **Update `DBA1_Score_Log.md`:** append a row to the session table (date, exam name, overall, T1–T8 scores, missed question numbers) and refresh the weak-topic ranking.
5. **Generate a study guide and answer key together:** `DBA1_Study_Guide_NN.md`, organized by topic (weakest first), each with official PostgreSQL 18 doc links (bias strongly toward postgresql.org/docs/18/...) plus vetted third-party articles/videos only where they add real value. Tie each link back to the specific missed question. At the same time, generate `PostgreSQL_DBA1_Practice_Exam_NN_Answer_Key.md` — a standalone Q#/letter key (compact table, no full question text) for the exam just graded, so the graded exam + its key can be shared with others.
6. **Validate every link before including it** — fetch or search for each URL (official docs and third-party) to confirm it actually resolves, and confirm any chapter/section number cited is correct rather than guessed. If a link can't be verified or no good supplementary source exists, skip it rather than include a fabricated or unverified one — an official-docs-only entry is fine; a guessed link is not.
7. **Strip Grant's filled-in answers from the exam file** once it's graded and logged (blank each `Answer: X` back to `Answer: `) — the score log and the new answer key are now the record, so the quiz file stays shareable without exposing his personal results.

## Existing files in this folder
- `PostgreSQL_DBA1_Practice_Exam_01.md` — completed, 34/40 (85%)
- `DBA1_Score_Log.md` — running per-topic score history
- `DBA1_Study_Guide_01.md` — reading list for T2/T4 (weakest) and T1/T6 (single-miss)

## Standing preferences
- Grant works daily with SQL Server and PostgreSQL, on containers and AWS/Azure — flag T-SQL-vs-Postgres syntax gotchas when relevant (e.g., `||` vs `+` for concatenation).
- Keep grading reports concise: score table, missed questions, brief correct-answer explanation.
- Don't run a new practice exam until Grant confirms he's ready.
