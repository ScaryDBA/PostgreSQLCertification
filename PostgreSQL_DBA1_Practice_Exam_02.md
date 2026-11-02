# OAPE PostgreSQL DBA-1 — Practice Exam 02

40 multiple-choice questions, 5 per topic area, scattered randomly. Mirrors the OAPE DBA-1 scope: https://www.oapg-edu.org/certifications/

**How to take it:** Answer inline by putting your letter choice after each question (e.g. `Answer: B`). Don't look anything up — treat it like the real exam. When you're done, tell me and I'll grade it and log your results by topic.

---

**1.** Which statement removes a privilege that was previously granted?
A. REVOKE
B. DENY
C. ALTER DEFAULT PRIVILEGES
D. DROP GRANT

Answer: 

**2.** What does `autovacuum_freeze_max_age` control?
A. The maximum table age, in transactions, before an aggressive autovacuum is forced to freeze old tuples and avoid wraparound
B. The maximum CPU cost autovacuum may accumulate before pausing
C. The amount of memory autovacuum workers may use
D. How often the autovacuum launcher wakes up to check tables

Answer: 

**3.** Which command initializes a new PostgreSQL data directory?
A. `initdb`
B. `pg_ctl init`
C. `createdb`
D. `pg_config --init`

Answer: 

**4.** Which background process sends WAL to a connected streaming replica?
A. walreceiver
B. A walsender process
C. The checkpointer
D. The autovacuum launcher

Answer: 

**5.** Which data type stores a JSON document while also supporting binary storage and efficient indexing/querying?
A. JSON
B. JSONB
C. TEXT
D. XML

Answer: 

**6.** Which parameter controls whether all, none, DDL-only, or modification-only statements get logged?
A. `log_statement`
B. `log_min_duration_statement`
C. `log_destination`
D. `log_checkpoints`

Answer: 

**7.** Which parameter, set in `postgresql.conf`, specifies the point in time to recover to during Point-in-Time Recovery?
A. `archive_timeout`
B. `recovery_min_apply_delay`
C. `recovery_target_time`
D. `checkpoint_timeout`

Answer: 

**8.** What does `REPEATABLE READ` isolation guarantee that `READ COMMITTED` does not?
A. That writers are blocked from modifying any table for the transaction's duration
B. That the transaction sees one consistent snapshot for its whole duration, rather than a new snapshot per statement
C. That DDL statements can run concurrently without locking
D. Nothing — the two levels behave identically in PostgreSQL

Answer: 

**9.** In PostgreSQL's versioning scheme (used since v10), what does moving from 17.x to 18.0 represent?
A. A minor bugfix release
B. A patch release that only affects extensions
C. A beta release
D. A major release, identified by a single number before the dot

Answer: 

**10.** Which role attribute allows a role to bypass all permission checks entirely?
A. `CREATEDB`
B. `REPLICATION`
C. `BYPASSRLS`
D. `SUPERUSER`

Answer: 

**11.** Which two parameters together determine the dead-tuple threshold at which autovacuum triggers a vacuum on a table?
A. `maintenance_work_mem` alone
B. `autovacuum_max_workers` alone
C. `autovacuum_vacuum_threshold` and `autovacuum_vacuum_scale_factor` together
D. `autovacuum_naptime` alone

Answer: 

**12.** Which psql meta-command lists all databases in the cluster?
A. `\l`
B. `\dt`
C. `\d`
D. `\c`

Answer: 

**13.** What is the role of the WAL writer background process?
A. It writes WAL records only at COMMIT time
B. It only runs at checkpoint time, alongside the checkpointer
C. It periodically flushes WAL buffers to disk even between commits and checkpoints
D. It handles client authentication before a backend process is forked

Answer: 

**14.** Which extension automatically logs execution plans for slow queries, without needing to run `EXPLAIN` manually?
A. `pg_stat_statements`
B. `auto_explain`
C. `pgcrypto`
D. `pg_buffercache`

Answer: 

**15.** If you back up with `pg_dump` in its default plain-text SQL format, which tool do you use to restore it?
A. `pg_restore`
B. `psql`
C. `pg_receivewal`
D. `pg_verifybackup`

Answer: 

**16.** Which isolation level in PostgreSQL can produce serialization failures that force the application to retry the transaction?
A. READ UNCOMMITTED
B. READ COMMITTED
C. REPEATABLE READ
D. SERIALIZABLE

Answer: 

**17.** What is the default port PostgreSQL listens on?
A. 1433
B. 3306
C. 5432
D. 5433

Answer: 

**18.** Which clause added to a `GRANT` statement lets the grantee, in turn, grant that same privilege to other roles?
A. `WITH ADMIN OPTION`
B. `CASCADE`
C. `WITH GRANT OPTION`
D. `WITH INHERIT TRUE`

Answer: 

**19.** Why can a long-running open transaction prevent `VACUUM` from reclaiming dead tuples?
A. It holds an exclusive lock that blocks VACUUM from starting
B. Those dead tuples might still be visible to that transaction's snapshot, so VACUUM can't remove them yet
C. It consumes CPU that autovacuum workers need
D. Open transactions automatically disable autovacuum

Answer: 

**20.** Which command-line utility connects interactively to a PostgreSQL database?
A. pgcli only
B. `psql`
C. `sqlplus`
D. `pg_connect`

Answer: 

**21.** Since PostgreSQL 15, where does the cumulative statistics system (feeding views like `pg_stat_all_tables`) store its data?
A. In per-table files on disk, written by a dedicated stats collector process
B. Only in the WAL stream
C. Computed on demand with no persistence between queries
D. In shared memory, with no separate stats collector process needed

Answer: 

**22.** Which command shows the actual execution plan and runtime statistics for a query, rather than just the estimated plan?
A. `EXPLAIN` (without `ANALYZE`)
B. `pg_stat_statements`
C. `SELECT * FROM pg_stat_activity`
D. `EXPLAIN ANALYZE`

Answer: 

**23.** In PostgreSQL 12 and later, how do you tell a starting server to enter standby/recovery mode?
A. By setting `recovery_target = standby` in `postgresql.conf`
B. By creating a `recovery.conf` file
C. By running `pg_ctl standby`
D. By creating a `standby.signal` file in the data directory

Answer: 

**24.** What do the hidden `xmin` and `xmax` system columns on a row represent?
A. The row's physical block and offset on disk
B. A checksum used to detect data corruption
C. The transaction IDs that created (`xmin`) and, if applicable, deleted or updated (`xmax`) that row version
D. The role currently holding a lock on that row

Answer: 

**25.** Which configuration file sets server-wide parameters like `shared_buffers` and `max_connections`?
A. `pg_hba.conf`
B. `postgresql.conf`
C. `pg_ident.conf`
D. `recovery.conf`

Answer: 

**26.** Which command sets privileges that will automatically apply to objects created in the future within a schema?
A. `CREATE POLICY`
B. `ALTER DEFAULT PRIVILEGES`
C. `GRANT ... ON SCHEMA`
D. `ALTER SCHEMA ... OWNER TO`

Answer: 

**27.** Which combined command both reclaims dead tuple space and updates planner statistics in one pass?
A. `VACUUM FULL`
B. `REINDEX`
C. `CLUSTER`
D. `VACUUM (ANALYZE)`

Answer: 

**28.** Which SQL clause filters groups after aggregation, as opposed to filtering individual rows before aggregation?
A. `WHERE`
B. `GROUP BY`
C. `HAVING`
D. `FILTER` (used inside an aggregate expression)

Answer: 

**29.** Architecturally, how does PostgreSQL handle each new client connection?
A. The postmaster forks a dedicated backend process to handle that connection
B. It spawns a new thread inside one shared process
C. It assigns the connection to a thread from a fixed internal thread pool
D. It always requires an external connection pooler like PgBouncer

Answer: 

**30.** Which view provides cluster-wide statistics about checkpoints and buffer writes performed by background processes?
A. `pg_stat_activity`
B. `pg_stat_user_tables`
C. `pg_stat_bgwriter`
D. `pg_locks`

Answer: 

**31.** What is a replication slot primarily used to guarantee?
A. That WAL segments are retained on the primary until the replica or consumer has received them
B. Zero replication lag between primary and replica
C. Automatic compression of WAL segments before they're sent
D. Encryption of WAL traffic between primary and replica

Answer: 

**32.** Which command creates a named point inside a transaction that you can later roll back to, without aborting the whole transaction?
A. `SAVEPOINT`
B. `BEGIN`
C. `COMMIT AND CHAIN`
D. `ROLLBACK PREPARED`

Answer: 

**33.** Which command reloads the server configuration without a full restart, for parameters that support it?
A. `pg_ctl restart`
B. `SELECT pg_reload_conf();`
C. `ALTER SYSTEM APPLY;`
D. `systemctl reload postgresql --hard`

Answer: 

**34.** Which system view lists all roles in the cluster along with their attributes (login, superuser, etc.)?
A. `pg_roles`
B. `pg_shadow`
C. `pg_group`
D. `pg_authid`

Answer: 

**35.** What does freezing a tuple during `VACUUM` accomplish?
A. It permanently deletes the tuple
B. It compresses the tuple's storage footprint
C. It marks the tuple visible to all current and future transactions, preventing wraparound issues
D. It converts the tuple into an index-only entry

Answer: 

**36.** Which constraint ensures a column's value can never be NULL?
A. CHECK constraint
B. UNIQUE constraint
C. DEFAULT constraint
D. NOT NULL constraint

Answer: 

**37.** What does the background writer do, distinct from the checkpointer?
A. It incrementally writes some dirty shared buffers to disk between checkpoints, smoothing out I/O
B. It performs the exact same full checkpoint work, just more often
C. It only writes dirty buffers during VACUUM
D. It manages WAL archiving via `archive_command`

Answer: 

**38.** Besides `stderr` and `csvlog`, which structured log format did PostgreSQL add as a `log_destination` option (introduced in v15, still available in v18)?
A. `jsonlog`
B. `xmllog`
C. `binarylog`
D. `syslog-json`

Answer: 

**39.** What must exist alongside your base backup for Point-in-Time Recovery to work?
A. A second base backup taken immediately afterward
B. An active logical replication subscription
C. A populated `pg_stat_archiver` view
D. A continuous, unbroken sequence of archived WAL segments covering the recovery window

Answer: 

**40.** Which statement explicitly locks an entire table in a specified mode?
A. `SELECT ... FOR UPDATE`
B. `ALTER TABLE ... SET LOCK`
C. `TABLE LOCK ON tablename`
D. `LOCK TABLE tablename IN <mode> MODE`

Answer: 

---

*When finished, let Claude know — grading and a per-topic score log will follow.*
