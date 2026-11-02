# OAPE PostgreSQL DBA-1 — Practice Exam 05

80 multiple-choice questions, 10 per topic (T1–T8), scattered (not grouped by topic). Scoped to PostgreSQL 18 only.

**How to take it:** Answer inline by putting your letter choice after each question (e.g. `Answer: B`). Do not look anything up — treat it like the real exam. When done, tell Claude and it will grade it and log your results by topic.

---

**1.** What does `idle_in_transaction_session_timeout` do?
A. Sets the lock wait timeout
B. Terminates sessions that sit idle inside an open transaction longer than the timeout
C. Closes idle connections that have no transaction
D. Cancels queries running longer than the timeout

Answer: 

**2.** What is the main trade-off of running `pg_upgrade --link`?
A. It is slower than copy mode but safer
B. It is very fast because no data is copied, but once the new cluster has been started the old cluster can no longer be safely used
C. It requires logical replication to be configured first
D. It only works within the same major version

Answer: 

**3.** What does `ROLLBACK TO SAVEPOINT sp1` do?
A. Rolls back the entire transaction
B. Commits work up to the savepoint
C. Deletes the savepoint and keeps the changes
D. Undoes work done since the savepoint without aborting the whole transaction

Answer: 

**4.** What is the default value of `listen_addresses`?
A. 0.0.0.0 and ::
B. * (all interfaces)
C. An empty string
D. localhost

Answer: 

**5.** Where do checkpoint statistics live in PostgreSQL 17 and later?
A. pg_stat_archiver
B. pg_stat_wal
C. pg_stat_checkpointer
D. pg_stat_bgwriter only

Answer: 

**6.** Which view, queried on a primary, shows the state and lag of connected standbys?
A. pg_stat_database
B. pg_stat_replication
C. pg_stat_wal_receiver
D. pg_stat_archiver

Answer: 

**7.** What is the default WAL segment size?
A. 64 MB
B. 1 MB
C. 16 MB
D. 256 MB

Answer: 

**8.** Why does PostgreSQL write WAL?
A. To hold temporary sort files
B. Changes are logged before data files are modified, enabling crash recovery and replication
C. To store old row versions for MVCC
D. To cache query plans

Answer: 

**9.** How does psql's `\copy` differ from the SQL `COPY` command?
A. \copy bypasses WAL so it is faster
B. They are identical aliases
C. \copy reads/writes files on the client machine with the client's permissions; COPY reads/writes files on the server
D. \copy only works with CSV

Answer: 

**10.** Which setting must be on to take incremental backups (PG17+), and which tool reconstructs a full backup from them?
A. wal_level = logical; pg_upgrade
B. track_commit_timestamp = on; pg_resetwal
C. summarize_wal = on; pg_combinebackup
D. archive_mode = always; pg_restore

Answer: 

**11.** What does `pg_restore --clean --if-exists` do?
A. Restores only objects that already exist
B. Cleans WAL files after restore
C. Drops existing objects before recreating them, without erroring if they don't exist
D. Deletes the dump file after restore

Answer: 

**12.** What does `pg_stat_io` (PostgreSQL 16+) report?
A. Network I/O per connection
B. I/O statistics broken down by backend type, object, and context
C. Disk space used per table
D. Only WAL write statistics

Answer: 

**13.** Which are the valid values of `log_statement`?
A. none, read, write, admin
B. off, ddl, dml, all
C. none, select, write, all
D. none, ddl, mod, all

Answer: 

**14.** What does ANALYZE do?
A. Rebuilds indexes
B. Removes dead tuples
C. Checks the table for corruption
D. Collects column statistics (stored in pg_statistic) for the query planner

Answer: 

**15.** What is the default value of `password_encryption` in modern PostgreSQL (including 18)?
A. md5
B. scram-sha-256
C. plain
D. crypt

Answer: 

**16.** Which system column holds the ID of the transaction that created a row version?
A. xmin
B. ctid
C. tableoid
D. xmax

Answer: 

**17.** Which pg_dump output format supports parallel dump with `-j`?
A. Tar (-F t)
B. Plain (-F p)
C. Custom (-F c)
D. Directory (-F d)

Answer: 

**18.** You ran `CREATE TABLE "Orders" (id int);` and later `SELECT * FROM Orders;` fails with 'relation does not exist'. Why?
A. Table names cannot start with a capital letter
B. You need square brackets around the name
C. The table is in a different database
D. Quoted identifiers preserve case, while the unquoted Orders is folded to lowercase (orders), which doesn't match

Answer: 

**19.** What does `SELECT 'abc' || NULL;` return in PostgreSQL?
A. 'abc'
B. An error
C. An empty string
D. NULL

Answer: 

**20.** What is the difference between `pg_cancel_backend(pid)` and `pg_terminate_backend(pid)`?
A. Cancel works only on idle sessions
B. Cancel interrupts the backend's current query; terminate closes the whole connection
C. Cancel closes the connection; terminate cancels the query
D. They are identical

Answer: 

**21.** What is a key benefit of the visibility map?
A. It lets index-only scans skip heap fetches for all-visible pages and lets vacuum skip those pages
B. It maps tables to tablespaces
C. It stores row statistics for the planner
D. It records which transactions hold locks

Answer: 

**22.** How does `CREATE USER` differ from `CREATE ROLE`?
A. CREATE ROLE cannot own objects
B. CREATE USER is equivalent to CREATE ROLE ... LOGIN; CREATE ROLE defaults to NOLOGIN
C. CREATE USER creates a superuser
D. They are different catalog objects stored in different tables

Answer: 

**23.** Which of these parameters requires a full server restart (not just a reload) to change?
A. work_mem
B. search_path
C. log_min_duration_statement
D. shared_buffers

Answer: 

**24.** A column is defined `GENERATED ALWAYS AS IDENTITY`. An INSERT supplies an explicit value for it. What happens?
A. The table is locked until the sequence is reset
B. An error, unless OVERRIDING SYSTEM VALUE is specified
C. The value is accepted silently
D. The value is ignored and the sequence is used

Answer: 

**25.** What is the minimum `wal_level` that supports WAL archiving and streaming replication?
A. replica
B. minimal
C. logical
D. archive

Answer: 

**26.** How do you find which sessions are blocking a given backend?
A. pg_stat_database
B. pg_blocking_pids(pid), alongside pg_locks and pg_stat_activity
C. pg_stat_user_tables
D. pg_stat_bgwriter

Answer: 

**27.** What does `SELECT ... FOR UPDATE SKIP LOCKED` do?
A. Locks the whole table
B. Skips rows that have been updated
C. Raises an error if any row is locked
D. Skips rows locked by other transactions instead of waiting, useful for job queues

Answer: 

**28.** In a REPEATABLE READ transaction you try to update a row another transaction changed and committed after your snapshot. What happens?
A. You wait indefinitely
B. Error 'could not serialize access due to concurrent update' (SQLSTATE 40001); the application should retry
C. A deadlock is always reported
D. Your update silently overwrites the other one

Answer: 

**29.** How do you start archive recovery (PITR) on a server?
A. Delete the backup_label file and restart
B. Create a standby.signal file only
C. Run pg_restore against the data directory
D. Create a recovery.signal file in the data directory and configure restore_command and a recovery target

Answer: 

**30.** What is required to use pg_stat_statements?
A. Installing a separate monitoring daemon
B. Add it to shared_preload_libraries (restart required) and run CREATE EXTENSION in the database
C. Only setting track_activities = on
D. Only CREATE EXTENSION; no restart or preload

Answer: 

**31.** What is the default value of `autovacuum_vacuum_cost_delay`?
A. 100 ms
B. 20 ms
C. 2 ms
D. 0 ms

Answer: 

**32.** Why does PostgreSQL need to freeze old rows?
A. Transaction IDs are 32-bit and wrap around; freezing marks old rows as visible to everyone to prevent wraparound problems
B. To prevent deadlocks
C. To move rows to a cold tablespace
D. To compress old rows

Answer: 

**33.** What does the predefined role `pg_read_all_data` provide?
A. Permission to read server log files only
B. SELECT limited to the public schema
C. Superuser privileges
D. Read access (SELECT) to all tables, views, and sequences, plus USAGE on schemas, without individual grants

Answer: 

**34.** DROP ROLE fails because the role owns objects. What is the cleanest fix?
A. DROP ROLE old_role FORCE;
B. REASSIGN OWNED BY old_role TO new_role; DROP OWNED BY old_role; then DROP ROLE old_role;
C. DROP ROLE old_role CASCADE;
D. DELETE FROM pg_roles WHERE rolname = 'old_role';

Answer: 

**35.** Which directory in the data directory holds WAL segment files?
A. pg_wal
B. base
C. pg_xact
D. pg_stat

Answer: 

**36.** What physically happens on an UPDATE in PostgreSQL?
A. The row is locked and nothing is written until commit
B. A new row version is written and the old version remains until VACUUM removes it
C. The old version is moved to an undo log
D. The row is overwritten in place

Answer: 

**37.** A server runs 18.1. What does moving to the 18.3 minor release typically require?
A. Installing the new binaries and restarting the server; no dump/restore or pg_upgrade needed
B. Running pg_upgrade to a new data directory
C. Setting up logical replication to a new cluster
D. A full pg_dumpall and restore

Answer: 

**38.** Where does `ALTER SYSTEM SET` store its changes?
A. Directly in postgresql.conf, rewriting the file
B. In pg_hba.conf
C. In postgresql.auto.conf in the data directory, which is read after postgresql.conf and overrides it
D. Only in the pg_settings catalog, lost at shutdown

Answer: 

**39.** What does `log_min_duration_statement = 500` do?
A. Logs the first 500 statements
B. Logs only statements shorter than 500 ms
C. Logs every statement that runs for at least 500 ms
D. Cancels statements running longer than 500 ms

Answer: 

**40.** What is the default value of `autovacuum_freeze_max_age`?
A. 1 billion
B. 200 million
C. 2 billion
D. 50 million

Answer: 

**41.** What does `INSERT ... ON CONFLICT (id) DO UPDATE ...` do?
A. Inserts the row, or updates the existing row if it violates the unique constraint on id (an upsert)
B. Defines conflict resolution for logical replication
C. Locks the table to prevent conflicts
D. Rolls back the transaction on any duplicate

Answer: 

**42.** How do you restore a plain-format (SQL script) dump?
A. Run it with psql -f
B. pg_restore
C. pg_resetwal
D. pg_basebackup

Answer: 

**43.** What does `WITH GRANT OPTION` on a GRANT mean?
A. The privilege is granted to PUBLIC as well
B. The recipient becomes superuser
C. The grant is automatically revoked at session end
D. The recipient can grant the same privilege on to other roles

Answer: 

**44.** In PostgreSQL 18, what is the default behavior of `initdb` regarding data checksums?
A. Checksums are only supported on Windows builds
B. Checksums are disabled by default; you must pass --data-checksums
C. Checksums can only be enabled with pg_checksums on a running server
D. Data checksums are enabled by default; pass --no-data-checksums to disable them

Answer: 

**45.** What does the PostgreSQL 18 parameter `autovacuum_vacuum_max_threshold` do?
A. Limits how many tables autovacuum processes at once
B. Caps the dead-tuple count that triggers autovacuum, so very large tables get vacuumed sooner (default 100 million)
C. Sets the maximum run time of one autovacuum
D. Sets the maximum number of autovacuum workers

Answer: 

**46.** What is the default `autovacuum_analyze_scale_factor`?
A. 0.2
B. 0.1
C. 0.01
D. 0.5

Answer: 

**47.** Which SQL command tells you which main configuration file the running server loaded?
A. SHOW postgresql.conf;
B. SELECT current_config();
C. SHOW config_file;
D. SHOW hba_dir;

Answer: 

**48.** Which psql command shows a table's columns, indexes, and constraints?
A. \l tablename
B. \dn tablename
C. \dt tablename
D. \d tablename

Answer: 

**49.** What changed for the `public` schema starting in PostgreSQL 15?
A. The public schema was removed
B. Public now allows only SELECT
C. All users lost USAGE on public
D. CREATE on the public schema is no longer granted to all users; by default only the database owner has it

Answer: 

**50.** Besides a base backup, what does PITR require?
A. A continuous WAL archive covering the period from the backup to the target time
B. A logical replication slot
C. A synchronous standby
D. A pg_dump of every database

Answer: 

**51.** Which best describes PostgreSQL's connection model?
A. A fixed pool of workers shared by all clients by default
B. One thread per connection in a single process
C. A single process handles all connections asynchronously
D. A dedicated backend process is forked for each client connection

Answer: 

**52.** You run `BEGIN; CREATE TABLE t (id int); ROLLBACK;`. What is the result?
A. The table exists because DDL auto-commits
B. The ROLLBACK raises an error
C. The table does not exist; DDL is transactional in PostgreSQL
D. The table exists but is empty

Answer: 

**53.** You want tables created in the future in schema `app` to be readable by role `reporting`. What do you use?
A. GRANT SELECT ON FUTURE TABLES IN SCHEMA app TO reporting;
B. ALTER ROLE reporting SET default_select = on;
C. ALTER DEFAULT PRIVILEGES IN SCHEMA app GRANT SELECT ON TABLES TO reporting;
D. GRANT SELECT ON ALL TABLES IN SCHEMA app TO reporting;

Answer: 

**54.** What is the default `autovacuum_vacuum_scale_factor`?
A. 0.1
B. 0.05
C. 0.2
D. 0.5

Answer: 

**55.** Declaring a PRIMARY KEY on a column automatically does what in PostgreSQL?
A. Creates a clustered index that physically orders the table
B. Creates a unique B-tree index and enforces NOT NULL
C. Records constraint metadata only, with no index
D. Creates a hash index

Answer: 

**56.** Where are a database's files stored under the data directory?
A. global/<database OID>/
B. pg_wal/<database name>/
C. pg_tblspc/ only
D. base/<database OID>/

Answer: 

**57.** What changed about `EXPLAIN ANALYZE` in PostgreSQL 18?
A. It outputs only JSON
B. It requires the pg_stat_statements extension
C. It includes BUFFERS information by default
D. It no longer executes the query

Answer: 

**58.** What does the `wait_event` column of pg_stat_activity show?
A. The last error raised
B. The next scheduled checkpoint
C. What the backend is currently waiting on, such as a lock or I/O
D. The event that started the session

Answer: 

**59.** Which psql command toggles expanded (vertical) output?
A. \H
B. \x
C. \a
D. \t

Answer: 

**60.** You edited pg_hba.conf. What is needed for the change to take effect?
A. A configuration reload (pg_ctl reload or SELECT pg_reload_conf()); no restart needed
B. A full server restart
C. Nothing; the file is re-read on every new connection attempt
D. Re-running initdb

Answer: 

**61.** When first starting the official `postgres` Docker image, which environment variable must you normally set (unless you explicitly allow trust authentication)?
A. POSTGRES_HBA_MODE
B. POSTGRES_SUPERUSER_KEY
C. POSTGRES_PASSWORD
D. PG_ADMIN_TOKEN

Answer: 

**62.** A role has SELECT on `app.t` but gets 'permission denied for schema app'. What is missing?
A. EXECUTE on schema app
B. SELECT on schema app
C. CONNECT on table app.t
D. USAGE on schema app

Answer: 

**63.** What is the main job of the WAL writer process?
A. Archives completed WAL segments
B. Streams WAL to standbys
C. Removes old WAL segments
D. Periodically flushes WAL buffers to disk

Answer: 

**64.** What does pg_basebackup produce?
A. A logical SQL script of all databases
B. An export of roles only
C. A copy of only the WAL archive
D. A physical copy of the cluster's data files, taken over the replication protocol by a role with the REPLICATION attribute

Answer: 

**65.** Which view shows dead-tuple counts and last autovacuum time per table?
A. pg_stat_database
B. pg_stat_user_tables
C. pg_stat_activity
D. pg_locks

Answer: 

**66.** In PostgreSQL, how does the READ UNCOMMITTED isolation level behave?
A. Like READ COMMITTED; dirty reads are never allowed
B. It permits dirty reads
C. Like SERIALIZABLE
D. Like REPEATABLE READ

Answer: 

**67.** Which are the valid values of `io_method` in PostgreSQL 18?
A. worker, aio, sync
B. async, direct, buffered
C. worker, io_uring, sync
D. threads, fork, sync

Answer: 

**68.** What is needed to use row-level security on a table?
A. Installing the pg_rls extension
B. Only CREATE POLICY; no ALTER TABLE needed
C. Only the BYPASSRLS attribute
D. ALTER TABLE ... ENABLE ROW LEVEL SECURITY plus at least one CREATE POLICY (otherwise non-owners see no rows)

Answer: 

**69.** What is PostgreSQL's default block (page) size?
A. 32 kB
B. 4 kB
C. 8 kB
D. 16 kB

Answer: 

**70.** What is TOAST?
A. A backup compression format
B. A type of index for text search
C. A mechanism that stores oversized column values out-of-line (compressed and/or chunked) in a secondary table
D. A background process that archives WAL

Answer: 

**71.** Which query returns only the first 10 rows in PostgreSQL?
A. SELECT TOP 10 * FROM t;
B. SET ROWCOUNT 10; SELECT * FROM t;
C. SELECT * FROM t WHERE ROWNUM <= 10;
D. SELECT * FROM t LIMIT 10;

Answer: 

**72.** pg_dump does not include roles. How do you dump roles and other cluster-wide objects?
A. pg_dumpall --globals-only
B. pg_dump --roles
C. pg_dump -F c --all-roles
D. pg_basebackup -R

Answer: 

**73.** Which role attribute lets a role bypass all permission checks?
A. CREATEROLE
B. BYPASSRLS
C. REPLICATION
D. SUPERUSER

Answer: 

**74.** How does pg_dump stay consistent while users are writing to the database?
A. It is not consistent; you must stop writes
B. It requires single-user mode
C. It takes ACCESS EXCLUSIVE locks on all tables
D. It uses a single transaction snapshot, so the dump reflects the moment it started, without blocking writers

Answer: 

**75.** Which `pg_settings` column shows that a changed parameter is waiting for a restart to take effect?
A. boot_val
B. pending_restart
C. reset_val
D. sourcefile

Answer: 

**76.** Two transactions deadlock. What does PostgreSQL do?
A. The older transaction always waits for the newer one
B. Both transactions wait forever
C. Both transactions are aborted
D. After deadlock_timeout it detects the cycle and aborts one transaction with an error, letting the other proceed

Answer: 

**77.** What does `VACUUM FULL` do?
A. Runs without blocking reads or writes and returns space to the OS
B. Only freezes old tuples
C. Rewrites the table into a new file and returns space to the OS, taking an ACCESS EXCLUSIVE lock
D. Only updates planner statistics

Answer: 

**78.** What does `VACUUM (PARALLEL 4) mytable;` do?
A. Vacuums 4 tables at once
B. Uses up to 4 background workers to process indexes during the vacuum
C. Runs 4 vacuums sequentially
D. Scans the heap with 4 parallel workers

Answer: 

**79.** What does the `RETURNING` clause on INSERT/UPDATE/DELETE do?
A. Returns control to the psql prompt
B. Is only valid inside functions
C. Rolls the statement back and returns an error code
D. Returns values from the affected rows without a separate query

Answer: 

**80.** Which background process writes dirty shared buffers to disk as part of a checkpoint?
A. autovacuum launcher
B. checkpointer
C. postmaster
D. walwriter

Answer: 
