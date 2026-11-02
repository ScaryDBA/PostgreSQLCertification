# OAPE PostgreSQL DBA-1 — Study Guide 03

Built from Practice Exam 03 misses (29/40, 72.5%). Organized weakest topic first. All links verified against live postgresql.org/docs/18 pages on 2026-09-16 — section numbers and anchors confirmed, not guessed. Scope: PostgreSQL 18 only.

Exam 03 was intentionally tougher and leaned heavily on PostgreSQL 18's newest features. That shows in the results: 7 of the 11 misses were pure "did you know PG18 added this" questions rather than gaps in core DBA fundamentals. Good news — that's a fast kind of gap to close.

---

## T1 — Installation, Versioning & Basic Configuration (2/5 — weakest this round)

**Q1 missed — `io_method` (new in PG18).** PostgreSQL 18's asynchronous I/O subsystem is controlled by the `io_method` parameter (`sync`, `worker`, or `io_uring` on Linux), not `effective_io_concurrency` (that one only tunes *how much* prefetching happens, not the underlying I/O mechanism).
Read: [19.4. Resource Consumption — io_method](https://www.postgresql.org/docs/18/runtime-config-resource.html#GUC-IO-METHOD)

**Q2 missed — `pg_upgrade` now preserves optimizer statistics (new in PG18), except extended statistics.** Since PG18, `pg_upgrade` transfers most planner statistics automatically (Step 15), sparing you a full re-`ANALYZE`. The exception: statistics from `CREATE STATISTICS` (extended statistics), custom extension statistics, and cumulative-stats-system data are *not* transferred — you still need to regenerate those.
Read: [pg_upgrade — Step 15, Statistics](https://www.postgresql.org/docs/18/pgupgrade.html)

**Q3 missed — `pg_checksums` adds checksums to an existing (offline) cluster.** Checksums don't have to be set at `initdb` time. `pg_checksums -e` (or `--enable`) can enable them later, but the cluster must be shut down cleanly first — there's no `ALTER SYSTEM` equivalent.
Read: [pg_checksums](https://www.postgresql.org/docs/18/app-pgchecksums.html)

**Q4 missed — `include_dir` in `postgresql.conf`.** `include_dir 'directory'` pulls in every `*.conf` file in that directory, processed in filename order — useful for splitting shared vs. per-server config. This is unrelated to extension library search paths.
Read: [19.1.5. Managing Configuration File Contents](https://www.postgresql.org/docs/18/config-setting.html#CONFIG-INCLUDES)

Q5 (PGDG repository) was correct — no action needed, but for reference: [PostgreSQL Linux downloads](https://www.postgresql.org/download/linux/)

---

## T2 — Connecting to PostgreSQL, Database Objects & Basic SQL (2/5 — tied weakest)

**Q7 missed — `RETURNING old`/`new` (new in PG18).** `INSERT`/`UPDATE`/`DELETE`/`MERGE` can now use the special aliases `old` and `new` inside `RETURNING` to get pre- and post-change row values in one statement (previously you only got new values for INSERT/UPDATE and old values for DELETE).
Read: [6.4. Returning Data from Modified Rows](https://www.postgresql.org/docs/18/dml-returning.html)
*T-SQL comparison:* this is conceptually similar to referencing the `inserted`/`deleted` pseudo-tables inside a SQL Server trigger's `OUTPUT` clause, except in Postgres it's a plain clause on the DML statement itself — no trigger required.

**Q8 missed — virtual generated columns are now the default (new in PG18).** Writing `GENERATED ALWAYS AS (expr)` without `STORED` now creates a *virtual* generated column — computed on read, not materialized on write. To get the pre-18 behavior (computed and stored on write), you must now explicitly add `STORED`.
Read: [CREATE TABLE — Generated Columns](https://www.postgresql.org/docs/18/sql-createtable.html#SQL-CREATETABLE-PARMS-GENERATED-STORED)

**Q9 missed — `uuidv7()` (new in PG18).** Unlike `gen_random_uuid()`/`uuidv4()`, a `uuidv7()` value embeds a timestamp in its high-order bits, so generated values are roughly sortable by creation time — useful for primary keys where index locality matters (avoids the random-insert-pattern problem UUIDv4 causes on B-tree indexes).
Read: [9.45. UUID Generation Functions](https://www.postgresql.org/docs/18/functions-uuid.html#FUNC_UUID_GEN_TABLE)

Q6 (`oauth` in `pg_hba.conf`, new in PG18) and Q10 (`\dn`) were correct — no action needed, but for reference: [20.15. OAuth Authorization/Authentication](https://www.postgresql.org/docs/18/auth-oauth.html)

---

## T7 — VACUUM, ANALYZE & Autovacuum (3/5)

**Q31 missed — `VACUUM (SKIP_LOCKED)` is a real, longstanding option.** It tells `VACUUM` to skip a relation it can't lock immediately rather than waiting, so a multi-table vacuum run isn't stalled by one busy table. (Note it can still block briefly on the relation's indexes.)
Read: [VACUUM — Parameters](https://www.postgresql.org/docs/18/sql-vacuum.html)

**Q34 missed — per-table autovacuum overrides use `ALTER TABLE ... SET (storage_parameter = value)`, not session `SET`.** Nearly every `autovacuum_*` GUC (scale factors, thresholds, cost delay/limit, freeze ages) can be overridden per table as a storage parameter, e.g. `ALTER TABLE big_table SET (autovacuum_vacuum_scale_factor = 0.01);`. A session-level `SET` only changes the setting for your own session and has no effect on autovacuum's behavior for that table.
Read: [19.10.1. Automatic Vacuuming](https://www.postgresql.org/docs/18/runtime-config-vacuum.html#RUNTIME-CONFIG-AUTOVACUUM)

---

## T5 — Server Architecture & Background Processes (3/5)

**Q25 missed — `pg_aios` (new in PG18).** This new system view lists every in-flight asynchronous I/O handle (one row per handle), including its state (`STAGED`, `SUBMITTED`, `COMPLETED_IO`, etc.) and target. It's the AIO-specific view — `pg_stat_io` gives you aggregate I/O *statistics*, not a live list of in-flight operations.
Read: [53.2. pg_aios](https://www.postgresql.org/docs/18/view-pg-aios.html)

**Q21 missed — IO Worker processes, with one caveat worth knowing.** When `io_method = worker`, PostgreSQL runs dedicated IO Worker background processes (the wait event table documents `IoWorkerMain` for their main loop). I marked "IO Worker" as the intended answer over "background writer" (which is a distinct, pre-existing process type that does *not* handle the new AIO queue). That said, when I checked the current `pg_stat_activity.backend_type` documentation directly, its explicit list of values doesn't yet name an IO-worker type by that exact string — so treat the *concept* (a new dedicated backend type for AIO workers, distinct from the background writer) as solid, but don't bank on the literal casing "IO Worker" appearing verbatim in `pg_stat_activity` without checking a live PG18 instance.
Read: [27.2.3. pg_stat_activity](https://www.postgresql.org/docs/18/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)

Q22–24 (logical replication launcher, bgwriter vs. checkpointer, postmaster startup) were correct — no action needed.

---

## T6 — MVCC & Transaction Management (4/5)

**Q30 missed — READ COMMITTED takes a new MVCC snapshot at the start of *every statement*, not once at `BEGIN`.** This is the defining difference from REPEATABLE READ, which takes one snapshot at the start of the transaction's first statement and reuses it throughout. Worth a clean re-read since you've scored 100% on T6 in both prior exams — this looks like a one-off slip rather than a pattern.
Read: [13.2.1. Read Committed Isolation Level](https://www.postgresql.org/docs/18/transaction-iso.html#XACT-READ-COMMITTED)

---

## T3, T4, T8 — no action needed

All three topics scored 5/5 this round. T4 (Backup & Recovery) in particular is worth noting: it was the weakest topic on both Exam 01 and Exam 02, and is now fully solid.

---

*Next step: whenever you're ready, say the word and I'll generate Practice Exam 04 — happy to dial the difficulty back toward the Exam 01/02 level, or keep pushing PG18-specific material, your call.*
