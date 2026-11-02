# OAPE PostgreSQL DBA-1 — Score Log

Tracks accuracy by topic across practice sessions. Feeds the study guide priorities.

Topic areas (per https://www.oapg-edu.org/certifications/):
1. Installation, Versioning & Basic Configuration
2. Connecting to PostgreSQL, Database Objects & Basic SQL
3. Roles & Privileges
4. Backup & Recovery
5. Server Architecture & Background Processes
6. MVCC & Transaction Management
7. VACUUM, ANALYZE & Autovacuum
8. Monitoring & Logging

## Session log

| Date | Exam | Overall | T1 | T2 | T3 | T4 | T5 | T6 | T7 | T8 | Notes |
|------|------|---------|----|----|----|----|----|----|----|----|-------|
| 2026-09-14 | Practice Exam 01 | 34/40 (85%) | 4/5 | 3/5 | 5/5 | 3/5 | 5/5 | 4/5 | 5/5 | 5/5 | Missed Q2, Q6, Q10, Q16, Q17, Q29 |
| 2026-09-14 | Practice Exam 02 | 31/40 (77.5%) | 4/5 | 5/5 | 4/5 | 3/5 | 2/5 | 5/5 | 4/5 | 4/5 | Missed Q1, Q13, Q14, Q15, Q19, Q21, Q23, Q29, Q33 |
| 2026-09-16 | Practice Exam 03 | 29/40 (72.5%) | 2/5 | 2/5 | 5/5 | 5/5 | 3/5 | 4/5 | 3/5 | 5/5 | Missed Q1, Q3, Q4, Q7, Q8, Q9, Q21, Q25, Q30, Q31, Q34. Exam intentionally toughened and PG18-heavy per Grant's request; most misses (7 of 11) were on new-in-18 features (io_method, pg_upgrade stats, include_dir, RETURNING old/new, virtual generated columns, uuidv7, pg_aios) rather than core conceptual gaps. |
| 2026-09-21 | Practice Exam 04 | 75/80 (93.75%) | 15/15 | 11/12 | 4/5 | 6/7 | 9/9 | 6/7 | 7/7 | 17/18 | Missed Q3 (psql connection URI vs. JDBC syntax), Q17 (pg_dump -F c custom vs. -F t tar format), Q25 (pg_table_size() vs. pg_stat_user_tables()), Q53 (pg_locks vs. pg_stat_activity for lock contention), Q55 (GRANT syntax word order). 80-question exam, weighted topic distribution (proportional to OAPE's published sub-objective counts per topic), dialed back to realistic difficulty after Exam 03's deliberate PG18 stress-test. All 4 repeat questions targeting Exam 03's flagged genuine gaps (READ COMMITTED snapshot timing, VACUUM SKIP_LOCKED, per-table autovacuum override, IO worker backend_type) were answered correctly — those gaps have closed. |

## Running weak-topic ranking (cumulative, most recent exam)

1. T3 — Roles & Privileges (80%) — single miss, but it's a GRANT syntax slip (word order), not a conceptual gap; was 100% on Exams 01–03
2. T4, T6 (86%) — T4 miss is real: confusing pg_dump's custom (-F c) vs. tar (-F t) format on compression/selective-restore behavior. T6 miss is monitoring-adjacent: reaching for pg_stat_activity instead of pg_locks for lock contention, not an MVCC/isolation-level gap — the previously flagged READ COMMITTED snapshot-timing gap is now resolved
3. T2, T8 (92–94%) — T2 miss was psql's connection URI scheme vs. JDBC-style syntax; T8 miss was pg_table_size() vs. a stats view — both syntax/recall slips, not conceptual
4. T1, T5, T7 (100%) — clean sweep; T7 in particular has now fully closed both flagged gaps from Exam 03 (VACUUM SKIP_LOCKED, per-table autovacuum overrides), and T5 closed the IO worker backend_type gap

Study guide priority: light touch this round — no deep conceptual gaps remain. Focus the guide on quick-reference syntax for the 5 misses (GRANT word order, pg_dump format flags, pg_table_size(), pg_locks vs. pg_stat_activity, psql connection URI scheme) rather than a full topic study plan.
