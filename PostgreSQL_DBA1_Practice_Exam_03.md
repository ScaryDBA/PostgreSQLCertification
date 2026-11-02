# OAPE PostgreSQL DBA-1 — Practice Exam 03

40 multiple-choice questions, 5 per topic area, scattered randomly. Mirrors the OAPE DBA-1 scope: https://www.oapg-edu.org/certifications/

**How to take it:** Answer inline by putting your letter choice after each question (e.g. `Answer: B`). Don't look anything up — treat it like the real exam. When you're done, tell me and I'll grade it and log your results by topic.

---

**1.** In PostgreSQL 18, which server parameter selects the method used for the new asynchronous I/O subsystem (e.g. `sync`, `worker`, `io_uring`)?
A. `effective_io_concurrency`
B. `io_method`
C. `wal_sync_method`
D. `async_io_mode`

Answer: 

**2.** Starting in PostgreSQL 18, `pg_upgrade` preserves optimizer statistics by default so the new cluster doesn't start with an empty planner. Which statistics are the exception — NOT preserved, requiring a manual `ANALYZE` afterward?
A. Ordinary per-column statistics (most-common values, histograms) on regular tables
B. Extended statistics created via `CREATE STATISTICS`
C. All statistics — nothing is preserved unless `--no-statistics` is omitted
D. Statistics on system catalogs only

Answer: 

**3.** Which tool can add data checksums to an existing PostgreSQL cluster that was initialized without them, without requiring a fresh `initdb`?
A. `pg_checksums` (run offline, against a stopped cluster)
B. `pg_verifybackup`
C. `ALTER SYSTEM SET data_checksums = on;`
D. Checksums can never be added after `initdb`

Answer: 

**4.** What is the purpose of the `include_dir` directive inside `postgresql.conf`?
A. It sets the data directory location
B. It pulls in all `.conf` files from a specified directory, letting you split configuration across multiple files
C. It specifies where WAL files are archived
D. It defines a search path for extension shared libraries

Answer: 

**5.** You need the very latest PostgreSQL 18 minor release the day it ships, rather than waiting on your Linux distribution's default packages. What's the standard way to get it?
A. Add and use the PGDG (PostgreSQL Global Development Group) package repository
B. Recompile from a nightly git snapshot
C. Wait for the distribution's next major OS release
D. Use `pg_upgrade` to jump versions

Answer: 

**6.** Which authentication method, new in PostgreSQL 18, can be configured in `pg_hba.conf` and relies on an external identity provider plus a token validator library?
A. `scram-sha-256`
B. `oauth`
C. `gss`
D. `cert`

Answer: 

**7.** In PostgreSQL 18, `RETURNING` clauses in `UPDATE`/`INSERT`/`DELETE`/`MERGE` can reference which special aliases to return both prior and resulting row values?
A. `before` / `after`
B. `old` / `new`
C. `source` / `target`
D. `pre` / `post`

Answer: 

**8.** As of PostgreSQL 18, when you write `GENERATED ALWAYS AS (expr)` on a column without specifying `STORED`, what happens?
A. It raises a syntax error — `STORED` is mandatory
B. It creates a virtual generated column, computed at read time rather than materialized on write
C. It silently behaves exactly like a `DEFAULT` expression
D. It is stored on disk exactly as in PostgreSQL 17 and earlier

Answer: 

**9.** What is the key property of a `uuidv7()` value that distinguishes it from `gen_random_uuid()` (v4)?
A. It's shorter, at 64 bits instead of 128
B. It embeds a timestamp, making generated values roughly sortable by creation order
C. It is guaranteed globally unique across databases, unlike v4
D. It can only be used as a primary key, never a regular column

Answer: 

**10.** Which meta-command lists all schemas in the current database?
A. `\dn`
B. `\dt`
C. `\l`
D. `\z`

Answer: 

**11.** In modern PostgreSQL, `ALTER DEFAULT PRIVILEGES` applies to:
A. All objects ever created by any role, retroactively
B. Only objects created in the future, by a specified role, within a specified schema (or database-wide if no schema is given)
C. Only tables, never sequences or functions
D. Only the `public` schema

Answer: 

**12.** `REVOKE ... CASCADE` on a privilege will:
A. Fail with an error, since `REVOKE` never cascades
B. Also revoke privileges that were granted "downstream" by the role losing the privilege (via `WITH GRANT OPTION`)
C. Drop the underlying table
D. Only affect the current session

Answer: 

**13.** When `pg_hba.conf` is evaluated for an incoming connection, which rule applies?
A. All matching rules are combined and the most restrictive wins
B. The last matching rule in the file is used
C. The first matching rule (top to bottom) is used
D. Rules are evaluated alphabetically by database name

Answer: 

**14.** To enforce row-level security policies on a table, which two things must both be true?
A. Row-level security must be enabled with `ALTER TABLE ... ENABLE ROW LEVEL SECURITY`, and at least one `CREATE POLICY` must apply (or no rows are visible/writable by non-owners)
B. Only a policy needs to exist; enabling RLS is optional
C. Only `ENABLE ROW LEVEL SECURITY` is needed; policies are generated automatically
D. RLS is enforced automatically on every table with no configuration

Answer: 

**15.** A role has `BYPASSRLS`. What does that mean?
A. The role is exempt from all row-level security policies, regardless of table settings
B. The role can bypass `pg_hba.conf` authentication
C. The role can bypass ordinary `GRANT`/`REVOKE` privilege checks
D. The role cannot be granted membership in other roles

Answer: 

**16.** What is the fundamental difference between what `pg_dump` and `pg_basebackup` each capture?
A. `pg_dump` produces a logical, portable export of database contents; `pg_basebackup` copies the physical data directory
B. Both produce identical output in different file extensions
C. `pg_dump` can only back up roles; `pg_basebackup` only backs up table data
D. `pg_basebackup` requires the server to be stopped; `pg_dump` does not

Answer: 

**17.** Which minimum `wal_level` setting is required before continuous WAL archiving (`archive_mode = on`) can function?
A. `minimal`
B. `replica` (or `logical`)
C. `logical` only — `replica` is not sufficient
D. WAL archiving does not depend on `wal_level`

Answer: 

**18.** During recovery, what does `recovery_target_action = 'promote'` do once the specified recovery target is reached?
A. Pauses recovery indefinitely, waiting for manual confirmation
B. Shuts the server down immediately
C. Automatically promotes the server out of recovery and opens it for read/write connections
D. Restarts recovery from the beginning of the WAL archive

Answer: 

**19.** What does `pg_verifybackup` do?
A. It validates a `pg_basebackup`-produced backup against its manifest, checking for missing or corrupted files
B. It restores a backup automatically if corruption is found
C. It compresses an existing backup to save space
D. It verifies role passwords stored in a backup

Answer: 

**20.** PostgreSQL's incremental backup feature (`pg_basebackup --incremental`, combined later with `pg_combinebackup`) requires which of the following from the prior backup?
A. Nothing — it can be based on any arbitrary prior backup, even from a different cluster
B. A backup manifest from the previous full or incremental backup, referenced when taking the incremental one
C. The previous backup must have been taken with `pg_dump`, not `pg_basebackup`
D. `wal_level = minimal`

Answer: 

**21.** In `pg_stat_activity`, what `backend_type` value would you expect to see for a process handling asynchronous I/O requests when `io_method = worker` is set?
A. `client backend`
B. `IO Worker`
C. `checkpointer`
D. `background writer`

Answer: 

**22.** What is the role of the logical replication launcher background process?
A. It performs the actual row-by-row decoding of WAL for a subscription
B. It starts and manages the per-subscription logical replication worker processes
C. It only runs on the subscriber, never the publisher
D. It replaces the WAL sender entirely

Answer: 

**23.** What is the key architectural difference between the background writer and the checkpointer?
A. They are the same process under two names
B. The background writer incrementally flushes some dirty buffers between checkpoints to smooth I/O; the checkpointer performs the full, periodic checkpoint flush of all dirty buffers as of a point in time
C. The checkpointer only runs once at server startup
D. The background writer handles WAL, and the checkpointer handles table data exclusively

Answer: 

**24.** What does the postmaster do with shared memory and background processes at server startup?
A. It allocates shared memory (e.g. `shared_buffers`) and starts the fixed set of background processes (checkpointer, background writer, WAL writer, autovacuum launcher, stats/logging infrastructure, etc.) before accepting connections
B. It creates shared memory fresh for every new client connection
C. It delegates shared memory allocation to the first connecting backend
D. Shared memory is only used for replication, not for normal backends

Answer: 

**25.** Which system view would show you the list of active asynchronous I/O handles when the new AIO subsystem is in use?
A. `pg_stat_bgwriter`
B. `pg_aios`
C. `pg_stat_io`
D. `pg_buffercache`

Answer: 

**26.** What mechanism does `SERIALIZABLE` isolation use, beyond ordinary row locks, to detect unsafe concurrent access patterns?
A. Table-level exclusive locks on every table touched
B. Predicate (SIREAD) locks that track which data a transaction's queries depended on, to detect dangerous serialization anomalies
C. It relies solely on `SELECT FOR UPDATE`
D. It disables MVCC entirely for the transaction

Answer: 

**27.** Why can transaction ID wraparound become dangerous if left unmanaged?
A. It cannot happen — PostgreSQL transaction IDs are unbounded
B. Transaction IDs are a finite 32-bit counter; without freezing, old rows could eventually appear to be from the future once the counter wraps, risking data becoming invisible or corrupted
C. It only affects logical replication, never normal queries
D. It is purely a cosmetic issue tracked in `pg_stat_bgwriter`

Answer: 

**28.** Creating a very large number of subtransactions (e.g. via nested `SAVEPOINT`s in a loop) within one long transaction can cause what kind of problem?
A. No issue — subtransactions are free
B. It can degrade performance cluster-wide, since other backends must check growing subtransaction ID lists (and it can pressure the subtransaction SLRU cache)
C. It automatically triggers `VACUUM FULL`
D. It silently promotes the transaction to `SERIALIZABLE`

Answer: 

**29.** What's the difference between `SELECT ... FOR UPDATE` and `SELECT ... FOR SHARE` on the rows they return?
A. They are identical in locking behavior
B. `FOR UPDATE` takes an exclusive row lock (blocking other `FOR UPDATE`/`FOR SHARE` and writers); `FOR SHARE` takes a shared row lock (blocks writers, but allows other `FOR SHARE` readers)
C. `FOR SHARE` locks the whole table; `FOR UPDATE` locks only one row
D. `FOR UPDATE` is read-only and never actually locks anything

Answer: 

**30.** Under `READ COMMITTED` isolation, when does a transaction take a new MVCC snapshot?
A. Once, at `BEGIN`, and never again
B. At the start of every individual statement within the transaction
C. Only when `COMMIT` is issued
D. Never — it always sees the exact same snapshot as `REPEATABLE READ`

Answer: 

**31.** `VACUUM (SKIP_LOCKED)` does what?
A. Skips relations that cannot be locked immediately, instead of waiting, so the vacuum run can continue with other tables
B. Skips all locked rows permanently, never vacuuming them
C. Disables page-level locking for the duration of the vacuum
D. Is not a real `VACUUM` option

Answer: 

**32.** What does `pg_stat_progress_vacuum` let you observe?
A. Historical vacuum runs from the last 30 days
B. Real-time progress of currently running vacuum operations (phase, blocks scanned vs. total, etc.)
C. Only autovacuum, never a manually issued `VACUUM`
D. Disk space reclaimed by `VACUUM FULL` only

Answer: 

**33.** What does `vacuum_freeze_min_age` control?
A. The minimum row-version age (in transactions) before `VACUUM` is allowed to freeze a tuple's `xmin`
B. How often autovacuum runs, in seconds
C. The maximum number of dead tuples tolerated per table
D. The amount of memory `VACUUM` may use

Answer: 

**34.** How can you override `autovacuum_vacuum_scale_factor` for one specific large, high-churn table without changing the cluster-wide default?
A. It cannot be overridden per table
B. `ALTER TABLE mytable SET (autovacuum_vacuum_scale_factor = 0.01);`
C. `SET autovacuum_vacuum_scale_factor = 0.01;` in a session
D. Edit `postgresql.conf` and restart the server

Answer: 

**35.** What additional planner-facing task does `ANALYZE` perform that plain `VACUUM` does not?
A. It reclaims dead tuple space
B. It updates the query planner's statistics (row count estimates, most-common values, histograms) used for query plans
C. It rewrites the table into a new physical file
D. It freezes all tuples unconditionally

Answer: 

**36.** `pg_stat_io` provides I/O statistics broken down by which dimensions?
A. Only total server-wide I/O with no breakdown
B. Backend type, I/O object, and I/O context (e.g. shared buffer hits/reads/writes, per process type)
C. Only WAL I/O, not table/index I/O
D. Only per-database totals

Answer: 

**37.** Which two parameters primarily control PostgreSQL's built-in log file rotation (when `logging_collector` is on)?
A. `log_rotation_size` and `log_rotation_age`
B. `log_statement` and `log_min_duration_statement`
C. `log_destination` and `log_line_prefix`
D. `checkpoint_timeout` and `checkpoint_completion_target`

Answer: 

**38.** In `pg_stat_statements`, which column reports the average execution time per call of a normalized statement?
A. `total_exec_time`
B. `calls`
C. `mean_exec_time`
D. `rows`

Answer: 

**39.** Enabling `track_io_timing` primarily allows you to see:
A. How long client authentication takes
B. Actual timing of read/write I/O operations, surfaced in views like `pg_stat_database` and in `EXPLAIN (ANALYZE, BUFFERS)` output
C. Wall-clock time since the server was last restarted
D. Replication lag in milliseconds

Answer: 

**40.** When `log_destination` includes `csvlog`, what do you get that plain `stderr` logging doesn't easily give you?
A. Structured, comma-separated fields (timestamp, user, database, error severity, query, etc.) that are easy to load into a table for analysis
B. Faster log writes with no disk overhead at all
C. Automatic log shipping to a remote server
D. JSON-formatted output identical to `jsonlog`

Answer: 

---

*When finished, let Claude know — grading and a per-topic score log will follow.*
