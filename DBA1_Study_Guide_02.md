# OAPE DBA-1 Study Guide — Practice Exam 02 Follow-Up

Scoped to what you missed on Practice Exam 02 (31/40, 77.5%). Everything below targets PostgreSQL 18 — no v19 content. Weakest topics first.

---

## Topic 5: Server Architecture & Background Processes (2/5) — new weak spot this round

Missed: Q13 (WAL writer's job), Q21 (where stats live since PG15), Q29 (process-per-connection model).

**Official docs**
- [28.5. WAL Configuration](https://www.postgresql.org/docs/18/wal-configuration.html) and [Chapter 28. Reliability and the Write-Ahead Log](https://www.postgresql.org/docs/18/wal.html) — the WAL writer flushes buffered WAL to disk on a periodic cycle (`wal_writer_delay`), independent of both COMMIT and checkpoints; this smooths I/O rather than gating it to transaction boundaries
- [28.6. WAL Internals](https://www.postgresql.org/docs/18/wal-internals.html) — background writer vs. WAL writer vs. checkpointer, side by side
- [27.2. The Cumulative Statistics System](https://www.postgresql.org/docs/18/monitoring-stats.html) — as of PostgreSQL 15, the separate stats collector process is gone; statistics live in shared memory and are written to permanent storage only at shutdown. This is exactly what Q21 tested
- [19.3. Connections and Authentication](https://www.postgresql.org/docs/18/runtime-config-connection.html) and [Chapter 51. Overview of PostgreSQL Internals](https://www.postgresql.org/docs/18/overview.html) — PostgreSQL is process-based: the postmaster forks one dedicated backend process per client connection. This is a real architectural difference from SQL Server's thread-based model, which is likely why Q29 tripped you up — bring your SQL Server intuition in cautiously here

**Supplementary**
- [Hironobu Suzuki — Process and Memory Architecture (The Internals of PostgreSQL)](https://www.interdb.jp/pg/pgsql02.html) — a well-regarded deep-dive with diagrams of the postmaster → backend-per-connection model and the background processes (WAL writer, background writer, checkpointer, autovacuum launcher/workers)

*(I'd previously listed a second CYBERTEC/Percona link here — both URLs turned out to be dead when I checked them just now. Rather than guess again, I'm leaving this to the one verified source above.)*

---

## Topic 4: Backup & Recovery (3/5) — persistent weak spot across both exams

Missed: Q15 (`pg_dump` plain-format restore tool), Q23 (how to trigger standby mode in PG12+).

**Official docs**
- [pg_dump](https://www.postgresql.org/docs/18/app-pgdump.html) — read the "Notes" section on output formats: only the plain-text format is restored with `psql`; the custom, directory, and tar formats require `pg_restore`. You picked `pg_restore` for a plain-text dump on Q15 — that's the reverse of the rule
- [pg_restore](https://www.postgresql.org/docs/18/app-pg-restore.html) — explicitly states it only works on non-plain-text `pg_dump` output
- [26.2. Log-Shipping Standby Servers](https://www.postgresql.org/docs/18/warm-standby.html) — since PostgreSQL 12, `recovery.conf` no longer exists at all. A standby is signaled by placing an empty `standby.signal` file in the data directory, with the connection/recovery settings living in regular `postgresql.conf` GUCs (`primary_conninfo`, `restore_command`, etc.). There's no `recovery_target = standby` setting — that was the trap in Q23
- [25.3. Continuous Archiving and Point-in-Time Recovery (PITR)](https://www.postgresql.org/docs/18/continuous-archiving.html) — worth a full re-read since T4 keeps costing you points across both exams; this chapter ties together base backups, WAL archiving, and recovery targets in one place

**Supplementary**
- [CYBERTEC — recovery.conf is gone in PostgreSQL v12](https://www.cybertec-postgresql.com/en/recovery-conf-is-gone-in-postgresql-v12/) — covers the `recovery.conf` → `standby.signal` change and why it happened, directly relevant to Q23

*(The two supplementary links I originally listed here — a CYBERTEC "backup and recovery basics" post and a Crunchy Data "Postgres 12 recovery changes" post — didn't check out as real URLs. Replaced with a verified one above.)*

---

## Topic 1: Installation, Versioning & Basic Configuration (4/5)

Missed: Q33 (reloading config without a restart).

**Official docs**
- [pg_ctl](https://www.postgresql.org/docs/18/app-pg-ctl.html) — `pg_ctl reload` is one valid option, but the exam question's correct answer was the SQL-callable equivalent: `SELECT pg_reload_conf();`. There is no `ALTER SYSTEM APPLY` command — `ALTER SYSTEM` only writes to `postgresql.auto.conf`; it still needs a reload (or restart, for restart-only parameters) to take effect
- [19.1. Setting Parameters](https://www.postgresql.org/docs/18/config-setting.html) — see the distinction between parameters that take effect on reload (`SIGHUP`/`pg_reload_conf()`) versus ones needing a full restart

No strong third-party resource needed — this is a one-line correction once you see it side by side with `ALTER SYSTEM`.

---

## Topic 3: Roles & Privileges (4/5)

Missed: Q1 (removing a granted privilege).

**Official docs**
- [GRANT](https://www.postgresql.org/docs/18/sql-grant.html) and [REVOKE](https://www.postgresql.org/docs/18/sql-revoke.html) — PostgreSQL has no `DENY` statement; that's SQL Server syntax. To remove a privilege you've granted, you always use `REVOKE`, never a negative grant

**Supplementary**
- Worth a mental note since you work in both engines daily: SQL Server's three-state model (GRANT/DENY/REVOKE, where DENY overrides everything) has no equivalent in Postgres — Postgres only has GRANT and REVOKE, and privilege resolution is purely additive across role membership.

---

## Topic 7: VACUUM, ANALYZE & Autovacuum (4/5)

Missed: Q19 (why a long-running transaction blocks tuple reclamation).

**Official docs**
- [24.1. Routine Vacuuming](https://www.postgresql.org/docs/18/routine-vacuuming.html) — see the "Preventing Transaction ID Wraparound Failures" subsection. A long-running transaction doesn't hold a lock that blocks VACUUM from running; VACUUM can still start. The issue is visibility: VACUUM can't remove a dead tuple if it might still be needed by an older transaction's snapshot (this is the same MVCC mechanism you already know well from Q26–28, which you aced)

**Supplementary**
- [CYBERTEC — Monitoring: Keeping an eye on old transactions](https://www.cybertec-postgresql.com/en/monitoring-keeping-an-eye-on-old-transactions/) — practical, matches exactly what Q19 was testing, and gives you queries to spot long-running transactions blocking cleanup in production

---

## Topic 8: Monitoring & Logging (4/5)

Missed: Q14 (which extension auto-logs slow query plans).

**Official docs**
- [F.3. auto_explain](https://www.postgresql.org/docs/18/auto-explain.html) — logs execution plans automatically for statements exceeding a duration threshold, no manual `EXPLAIN` needed
- [F.32. pg_stat_statements](https://www.postgresql.org/docs/18/pgstatstatements.html) — tracks aggregate execution statistics (calls, total/mean time) per normalized query, but does *not* capture execution plans. Easy pair to mix up since both are "slow query" tools loaded via `shared_preload_libraries` — the distinguishing feature is that only `auto_explain` gives you the plan itself

---

## Suggested order

1. Topic 5 (Server Architecture) — biggest gap this round, and conceptually foundational (process model, WAL writer, stats system)
2. Topic 4 (Backup & Recovery) — still your most persistent weak spot across both exams; worth a full chapter re-read, not just patching the two missed questions
3. Topics 1, 3, 7, 8 — single-question gaps, quick review
4. Topics 2 and 6 — solid this round (100% each); light maintenance only

Once you've worked through Topic 5 and Topic 4 in particular, let Claude know and we'll run Practice Exam 03.
