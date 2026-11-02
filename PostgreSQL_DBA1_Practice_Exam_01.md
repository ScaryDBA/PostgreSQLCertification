# OAPE PostgreSQL DBA-1 — Practice Exam 01

40 multiple-choice questions, 5 per topic area, scattered randomly. Mirrors the OAPE DBA-1 scope: https://www.oapg-edu.org/certifications/

**How to take it:** Answer inline by putting your letter choice after each question (e.g. `Answer: B`). Don't look anything up — treat it like the real exam. When you're done, tell me and I'll grade it and log your results by topic.

---

**1.** You want to run the latest minor release of PostgreSQL 16 as soon as it's out, ahead of what your Linux distribution's default package repo offers. What should you use?
A. Compile PostgreSQL from source every time a minor release ships
B. The PGDG (PostgreSQL Global Development Group) repository
C. The distribution's built-in repository only
D. A Docker image tagged `:latest`

Answer: 

**2.** Which command checks whether a PostgreSQL server is accepting connections, without actually logging in?
A. `pg_ctl status`
B. `psql -c "SELECT 1"`
C. `pg_isready`
D. `systemctl is-active postgresql`

Answer: 

**3.** Which file controls which hosts, users, and databases are permitted to connect, and by what authentication method?
A. `postgresql.conf`
B. `pg_hba.conf`
C. `pg_ident.conf`
D. `pg_service.conf`

Answer: 

**4.** Which of these best describes the purpose of a tablespace in PostgreSQL?
A. A logical grouping of tables that behaves like a schema
B. A way to map a database object's on-disk storage location to a specific directory/filesystem
C. A temporary in-memory area used for sorting
D. A backup format for pg_dump

Answer: 

**5.** You need to move from PostgreSQL 14 to PostgreSQL 17 with the least possible downtime, and you're willing to manage the added complexity. Which upgrade method is best suited to that goal?
A. `pg_upgrade` in `--link` mode
B. Dump with `pg_dumpall` and restore with `psql`
C. Logical replication to a new instance, then cut over
D. Stopping the server and copying the data directory to a new major version

Answer: 

**6.** In `psql`, which meta-command lists all tables in the current database?
A. `\l`
B. `\dt`
C. `\d+`
D. `\c`

Answer: 

**7.** What determines which schema PostgreSQL searches first when you reference an unqualified table name?
A. `default_tablespace`
B. `search_path`
C. `current_schema()`
D. The order schemas were created in

Answer: 

**8.** A materialized view's contents become stale as the underlying tables change. What must you do to update it?
A. Nothing — it updates automatically like a regular view
B. `REFRESH MATERIALIZED VIEW`
C. `VACUUM` the materialized view
D. Drop and recreate it

Answer: 

**9.** Which PostgreSQL object automatically generates the next value for a column, typically used behind `SERIAL` or `GENERATED ... AS IDENTITY` columns?
A. A trigger
B. A sequence
C. A rule
D. A domain

Answer: 

**10.** Which SQL construct would you use to safely concatenate two text columns, `first_name` and `last_name`, with a space between them?
A. `first_name + ' ' + last_name`
B. `CONCAT(first_name, last_name)` only
C. `first_name || ' ' || last_name`
D. `first_name . last_name`

Answer: 

**11.** A role is created with `NOLOGIN`. What does this mean?
A. The role cannot own any database objects
B. The role cannot be used to establish a direct database connection, but can still be granted to other roles
C. The role is automatically a superuser
D. The role's privileges expire immediately

Answer: 

**12.** Which statement grants the `SELECT` privilege on table `orders` to role `analyst`?
A. `ALTER ROLE analyst SELECT ON orders;`
B. `GRANT SELECT ON orders TO analyst;`
C. `SET PRIVILEGE SELECT ON orders FOR analyst;`
D. `GRANT analyst TO orders;`

Answer: 

**13.** In modern PostgreSQL (15+), what changed about the default privileges of the `public` schema?
A. Nothing changed; behavior has been constant since PostgreSQL 8
B. All roles now have superuser rights in the public schema by default
C. Regular users no longer have `CREATE` privilege on the `public` schema by default — only the database owner does
D. The `public` schema was removed entirely

Answer: 

**14.** If role `team_lead` has the `INHERIT` attribute and is a member of role `dev_team`, what happens?
A. `team_lead` must explicitly run `SET ROLE dev_team` to use `dev_team`'s privileges
B. `team_lead` automatically has the privileges of `dev_team` without an explicit `SET ROLE`
C. `team_lead` inherits `dev_team`'s password
D. Inheritance has no effect on privileges, only on role membership listing

Answer: 

**15.** Which of the following determines who can `DROP` a table, regardless of explicit `GRANT` statements?
A. Only a role with the `DROP` privilege explicitly granted
B. The table's owner (or a superuser)
C. Any role with `CONNECT` privilege on the database
D. Any role listed in `pg_hba.conf`

Answer: 

**16.** What is the fundamental difference between a logical backup and a physical backup in PostgreSQL?
A. Logical backups copy raw data files; physical backups export SQL statements or data via a defined format
B. Logical backups (e.g. `pg_dump`) export a portable representation of the data; physical backups (e.g. `pg_basebackup`) copy the actual data files
C. There is no meaningful difference — both terms describe `pg_dump`
D. Physical backups can only be restored to the exact same PostgreSQL version

Answer: 

**17.** Which tool would you use to back up all databases in a cluster, including global objects like roles, in one operation?
A. `pg_dump`
B. `pg_dumpall`
C. `pg_basebackup`
D. `pg_restore`

Answer: 

**18.** You created a backup using `pg_dump -Fc` (custom format). Which tool must you use to restore it?
A. `psql`
B. `pg_restore`
C. `pg_ctl`
D. `pg_loader`

Answer: 

**19.** What must be enabled for PostgreSQL to retain WAL segments for continuous archiving?
A. `hot_standby = on`
B. `archive_mode = on` with a valid `archive_command`
C. `fsync = off`
D. `wal_level = minimal`

Answer: 

**20.** Point-in-Time Recovery (PITR) allows you to:
A. Restore a database to any arbitrary moment in time using a base backup plus archived WAL
B. Instantly roll back a single transaction without restoring anything
C. Recover only the most recent committed transaction
D. Recover data without needing any prior backup

Answer: 

**21.** What is the role of the postmaster process in PostgreSQL?
A. It executes every client's SQL queries directly
B. It's the supervisor process that listens for connections and forks backend processes to handle them
C. It only handles WAL writing
D. It is a client-side connection pooler

Answer: 

**22.** `shared_buffers` primarily controls:
A. The amount of memory PostgreSQL uses for client connection sockets
B. The amount of memory used for caching table and index pages shared across all backend processes
C. Per-session memory used for sorting query results
D. The size of the WAL buffer only

Answer: 

**23.** What is the main difference between `work_mem` and `maintenance_work_mem`?
A. They are the same setting under different names
B. `work_mem` bounds memory for operations like sorts/hashes per query operation; `maintenance_work_mem` bounds memory for maintenance tasks like `VACUUM`, `CREATE INDEX`, and `ALTER TABLE`
C. `work_mem` is cluster-wide and cannot be set per session
D. `maintenance_work_mem` only affects autovacuum, never manual `VACUUM`

Answer: 

**24.** Which background process is responsible for flushing dirty buffers to disk in an orderly way at checkpoint time, distinct from the background writer's ongoing incremental flushing?
A. The autovacuum launcher
B. The checkpointer
C. The WAL receiver
D. The stats collector

Answer: 

**25.** Why does PostgreSQL use Write-Ahead Logging (WAL)?
A. To store the query plan cache
B. To ensure durability and crash recovery by recording changes before they're applied to data files
C. To replace the need for regular backups
D. To reduce disk I/O to zero

Answer: 

**26.** What is the core idea behind MVCC (Multi-Version Concurrency Control) in PostgreSQL?
A. Every transaction locks the entire table to prevent conflicts
B. Readers and writers don't block each other because each transaction sees a consistent snapshot of data via row versions
C. Only one transaction can run at a time per database
D. Data is versioned only during backups

Answer: 

**27.** What is PostgreSQL's default transaction isolation level?
A. READ UNCOMMITTED
B. READ COMMITTED
C. REPEATABLE READ
D. SERIALIZABLE

Answer: 

**28.** Two transactions each try to update the same row that the other has locked, in an order that creates a cycle of waiting. What does PostgreSQL do?
A. It waits forever since it cannot detect this situation
B. It silently commits both transactions
C. It detects the deadlock (after `deadlock_timeout`) and aborts one of the transactions with an error
D. It automatically merges the two transactions

Answer: 

**29.** Which view would you query to see current lock information, including what's blocking what?
A. `pg_stat_activity` only
B. `pg_locks`
C. `pg_stat_user_tables`
D. `information_schema.locks`

Answer: 

**30.** Why does MVCC create a need for VACUUM?
A. VACUUM is unrelated to MVCC; it only manages indexes
B. Old row versions (dead tuples) left behind by updates/deletes accumulate and need to be reclaimed for space reuse
C. VACUUM is needed to encrypt old row versions
D. MVCC never leaves old row versions behind

Answer: 

**31.** What is the difference between plain `VACUUM` and `VACUUM FULL`?
A. They are identical in effect
B. Plain `VACUUM` reclaims space for reuse within the table without an exclusive lock (mostly); `VACUUM FULL` rewrites the entire table into a new file, requiring an exclusive lock, to reclaim disk space back to the OS
C. `VACUUM FULL` is only for indexes
D. Plain `VACUUM` requires downtime; `VACUUM FULL` does not

Answer: 

**32.** At a conceptual level, why does transaction ID wraparound matter for VACUUM?
A. It doesn't — wraparound was removed in modern PostgreSQL
B. Transaction IDs are finite; VACUUM must freeze old row versions so PostgreSQL doesn't confuse very old rows with future transactions once IDs wrap around
C. Wraparound only affects replication, never VACUUM
D. It's a purely cosmetic counter with no operational impact

Answer: 

**33.** Which system view would you check to see how many dead tuples a table has and when it was last vacuumed/autovacuumed?
A. `pg_stat_activity`
B. `pg_stat_user_tables`
C. `pg_locks`
D. `pg_stat_bgwriter`

Answer: 

**34.** What triggers the autovacuum daemon to vacuum a table (at a conceptual level)?
A. A fixed daily schedule only
B. When the estimated number of dead/updated rows exceeds a threshold based on table size and autovacuum settings
C. Only when a superuser manually starts it
D. Only when the table is queried with `SELECT *`

Answer: 

**35.** What does `ANALYZE` do, as distinct from `VACUUM`?
A. It reclaims disk space from dead tuples, same as `VACUUM`
B. It updates the planner's statistics about table contents (row counts, value distributions) so the query planner can make better decisions
C. It rewrites the table into a new file
D. It only runs as part of `VACUUM FULL`

Answer: 

**36.** Which function/view would you use to check how many current sessions exist and what query (if any) each is running?
A. `pg_stat_database`
B. `pg_stat_activity`
C. `pg_stat_bgwriter`
D. `pg_available_extensions`

Answer: 

**37.** You need to forcibly disconnect a runaway session without waiting for it to finish. Which function does that (versus just canceling its current query)?
A. `pg_cancel_backend()`
B. `pg_terminate_backend()`
C. `pg_reload_conf()`
D. `pg_stat_reset()`

Answer: 

**38.** Which extension, once installed and loaded via `shared_preload_libraries`, tracks execution statistics for SQL statements so you can find your slowest or most frequent queries?
A. `pg_stat_statements`
B. `pg_buffercache`
C. `auto_explain`
D. `pgcrypto`

Answer: 

**39.** Which parameter controls the minimum execution time a statement must reach before it gets logged?
A. `log_statement`
B. `log_min_duration_statement`
C. `log_min_messages`
D. `log_duration`

Answer: 

**40.** What is the purpose of `log_line_prefix`?
A. It sets which log destination (stderr, csvlog, jsonlog) is used
B. It defines a customizable prefix (timestamps, PID, user, database, etc.) prepended to each log line for structured/parseable logs
C. It filters out log lines below a severity threshold
D. It rotates log files based on size

Answer: 

---

*When finished, let Claude know — grading and a per-topic score log will follow.*
