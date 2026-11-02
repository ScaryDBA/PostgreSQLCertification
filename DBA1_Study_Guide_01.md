# OAPE DBA-1 Study Guide — Practice Exam 01 Follow-Up

Scoped to what you missed on Practice Exam 01 (34/40). Everything below targets PostgreSQL 18 — no v19 content included, since the exam is oriented to v18. Weakest topics first.

---

## Topic 2: Connecting to PostgreSQL, Database Objects & Basic SQL (3/5)

Missed: Q6 (`\dt` vs `\d+`), Q10 (string concatenation).

**Official docs**
- [psql — full reference, including the `\d` meta-command family](https://www.postgresql.org/docs/18/app-psql.html) — read the section on `\d`, `\dt`, `\d+` carefully; `\dt` lists only tables, while `\d`/`\d+` with no argument lists *all* relations (tables, views, sequences, etc.)
- [9.4. String Functions and Operators](https://www.postgresql.org/docs/18/functions-string.html) — confirms `||` as the concatenation operator; `+` is arithmetic-only in Postgres, unlike T-SQL

**Supplementary**
- [Crunchy Data — Quickly Document Your Postgres Database Using psql Meta-Commands](https://www.crunchydata.com/blog/d-meta) — good walkthrough of the `\d` family and why `\dt` is the narrower, more specific command
- [database.guide — PostgreSQL \dt Command Explained](https://database.guide/postgresql-dt-command-explained/) — short, example-driven
- [PopSQL — How to Concatenate Strings in PostgreSQL](https://popsql.com/learn-sql/postgresql/how-to-concatenate-strings-in-postgresql) — covers `||`, `CONCAT()`, and `CONCAT_WS()` side by side, useful since you're context-switching from SQL Server's `+`

---

## Topic 4: Backup & Recovery (3/5)

Missed: Q16 (logical vs. physical backup concept), Q17 (`pg_dumpall` vs. `pg_basebackup`).

**Official docs**
- [Chapter 25. Backup and Restore](https://www.postgresql.org/docs/18/backup.html) — read straight through once; it lays out SQL dump, file-system-level backup, and continuous archiving/PITR as three distinct strategies
- [pg_dump](https://www.postgresql.org/docs/18/app-pgdump.html) — single database, no roles/tablespaces
- [pg_dumpall](https://www.postgresql.org/docs/18/app-pg-dumpall.html) — confirms it "dumps global objects... namely database roles, tablespaces, and privilege grants," calling `pg_dump` per database internally
- [pg_basebackup](https://www.postgresql.org/docs/18/app-pgbasebackup.html) — physical, whole-cluster only, can't target individual databases

**Supplementary**
- [CYBERTEC — pg_basebackup: Creating Self-Sufficient Backups](https://www.cybertec-postgresql.com/en/pg_basebackup-creating-self-sufficient-backups/) — CYBERTEC is one of OAPE's supporting companies, and this walks through practical `pg_basebackup` use for PITR
- [Medium — pg_dump vs. pg_basebackup vs. pg_dumpall: Which Backup Tool Should You Use?](https://medium.com/@ajaymaurya73130/pg-dump-vs-pg-basebackup-vs-pg-dumpall-which-postgresql-backup-tool-should-you-use-46fafedc440d) — exactly the three-way comparison this pair of questions tested

---

## Topic 1: Installation, Versioning & Basic Configuration (4/5)

Missed: Q2 (`pg_isready` vs. `pg_ctl status`).

**Official docs**
- [pg_isready](https://www.postgresql.org/docs/18/app-pg-isready.html) — a real connection-availability probe; exit codes distinguish "accepting connections" / "rejecting" / "no response" / "no attempt made"
- [pg_ctl](https://www.postgresql.org/docs/18/app-pg-ctl.html) — `status` mode just checks whether the postmaster process is running (reads the PID file), not whether it's accepting client connections

No strong third-party resource needed here — the two doc pages side by side make the distinction clear in a couple of minutes.

---

## Topic 6: MVCC & Transaction Management (4/5)

Missed: Q29 (`pg_locks`, not `information_schema.locks`, which doesn't exist in Postgres).

**Official docs**
- [Chapter 13. Concurrency Control](https://www.postgresql.org/docs/18/mvcc.html) — the whole MVCC/isolation/locking chapter; if you have time, also read 13.2 (Transaction Isolation) and 13.3 (Explicit Locking) since they're adjacent exam territory
- [53.13. pg_locks](https://www.postgresql.org/docs/18/view-pg-locks.html) — the actual system view; note the tip on joining `pg_locks` to `pg_stat_activity` on `pid`, and using `pg_blocking_pids()` instead of self-joining `pg_locks`

**Supplementary**
- [CYBERTEC — PostgreSQL: Understanding Deadlocks](https://www.cybertec-postgresql.com/en/postgresql-understanding-deadlocks/) — plain-language deadlock walkthrough from an OAPE supporting company
- [CYBERTEC — Row Locks in PostgreSQL](https://www.cybertec-postgresql.com/en/row-locks-in-postgresql/) — how row-level locking actually works under the hood
- [YouTube — How Does PostgreSQL Use MVCC and Locks in Read Committed?](https://www.youtube.com/watch?v=IRRYaIAM1Zw) — video walkthrough if you'd rather watch than read

---

## Suggested order

1. Topic 4 (Backup & Recovery) — biggest conceptual gap, most likely to resurface in different question phrasing
2. Topic 2 (SQL/psql) — quick fixes, mostly muscle-memory corrections
3. Topic 1 and Topic 6 — single-question gaps, light review

Once you've worked through these, let Claude know and we'll run Practice Exam 02 to check retention before moving on to the topics you already scored 100% on.
