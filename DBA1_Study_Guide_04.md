# OAPE PostgreSQL DBA-1 — Study Guide 04

Light-touch guide for Practice Exam 04 (75/80, 93.75%). No conceptual gaps this round — the five misses (Q3, Q17, Q25, Q53, Q55) are all syntax/naming recall slips spread across five different topics, not a weak topic. So this is a quick-reference list tied to each missed question, plus an extra deep-dive on locks per your request. All links below were fetched and confirmed live against the PostgreSQL 18 docs before inclusion.

---

## T3 — Roles & Privileges (weakest this round, 4/5)

**Missed: Q55** — `GRANT SELECT, INSERT ON mytable TO myrole;` — privileges come first, then `ON object`, then `TO role`. `GRANT myrole SELECT, INSERT ON mytable;` isn't valid syntax (that word order is only used for the *role membership* form of GRANT, e.g. `GRANT admins TO joe;`, which is a different variant of the command).

- [GRANT — full synopsis and both variants (object privileges vs. role membership)](https://www.postgresql.org/docs/18/sql-grant.html)

---

## T4 — Backup & Recovery (6/7)

**Missed: Q17** — pg_dump's `-F c` (custom) format is compressed by default and is one of the two most flexible formats (along with `-F d` directory) — both allow selection/reordering of items and parallel restore. `-F t` (tar) is explicitly *not* compressed and can't reorder items on restore.

**How common is this, really?** Fairly fundamental — not obscure trivia. It's one of the first decisions in the pg_dump docs' own options list, and in real-world practice it's the default choice you make on essentially every production logical backup (you'd almost always reach for `-F c`, rarely `-F t`). Worth solidifying since it's likely to reappear in some form on the actual exam.

- [pg_dump — `-F`/`--format` option, quoting the exact custom vs. tar tradeoff](https://www.postgresql.org/docs/18/app-pgdump.html)

---

## T6 — MVCC & Transaction Management (6/7) — includes the deeper locks reading you asked for

**Missed: Q53** — `pg_locks` is the view for currently held/waiting locks and blocking relationships; `pg_stat_activity` shows session/query state (what's running, since when) but not lock detail on its own. In practice you join the two on `pid` — `pg_stat_activity` tells you *who*, `pg_locks` tells you *what they're waiting on*.

Since you flagged this as a bit of a gap, here's a deeper set of readings beyond just the one missed question:

- [Chapter 13.3, Explicit Locking — table-level lock modes and what acquires each, row-level lock modes (`FOR UPDATE`/`FOR NO KEY UPDATE`/`FOR SHARE`/`FOR KEY SHARE`), deadlock example and detection, advisory locks](https://www.postgresql.org/docs/18/explicit-locking.html)
- [53.13. `pg_locks` — the view's columns, and why joining against `pg_stat_activity` (not trying to self-join `pg_locks`) is the recommended way to find blockers](https://www.postgresql.org/docs/18/view-pg-locks.html)
- [PostgreSQL wiki: Lock Monitoring — practical, ready-to-run queries for finding exactly which session is blocking which, plus a query that also shows how long a lock has been waited on](https://wiki.postgresql.org/wiki/Lock_Monitoring)

The wiki page's blocked/blocking query is the practical version of what `pg_blocking_pids()` does under the hood (which the `pg_locks` doc explicitly recommends over hand-rolling a self-join, since getting the conflict logic right by hand is genuinely tricky). Good one to actually run against a test database a couple of times so the pg_locks/pg_stat_activity join becomes muscle memory rather than something to reason through under exam pressure.

---

## T2 — Connecting, Objects & SQL (11/12)

**Missed: Q3** — psql/libpq connection URIs use the `postgresql://` or `postgres://` scheme (e.g. `postgresql://user:password@host:5432/dbname`), not JDBC-style `jdbc:postgres://...` — that prefix is a Java-ecosystem convention, not something libpq/psql recognizes.

- [32.1.1.2. Connection URIs — exact syntax and valid examples](https://www.postgresql.org/docs/18/libpq-connect.html#LIBPQ-CONNSTRING-URIS)

---

## T8 — Monitoring & Logging (17/18)

**Missed: Q25** — `pg_table_size()` returns a table's on-disk size in bytes directly; `pg_stat_user_tables` is a statistics *view* (rows, scans, vacuum history, etc.), not a size function — it doesn't return size at all.

- [9.28.7. Database Object Management Functions, Table 9.102 — `pg_table_size()`, `pg_relation_size()`, `pg_database_size()` side by side](https://www.postgresql.org/docs/18/functions-admin.html#FUNCTIONS-ADMIN-DBSIZE)

---

## T1, T5, T7 — clean sweep (15/15, 9/9, 7/7)

Nothing to add here. Worth noting: all four questions that revisited your Exam 03 gaps (READ COMMITTED snapshot timing, VACUUM SKIP_LOCKED, per-table autovacuum overrides, IO worker backend_type) were answered correctly — those are closed for good.
