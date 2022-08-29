This document describes the MySQL kernel version updates. For information on how to upgrade the kernel, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

## MySQL 8.0
### 20220331

#### Bug fixes

- Fixed the crash caused by dereferencing wild pointers in the thread pool.

### 20220330

#### New features

- Enabled writeset parallel replication by default.
- Supported extended resource groups to control the I/O, memory utilization, and SQL timeout policy by user.
- Supported flashback query to query data at any time point within the UNDO time range.
- Supported RETURNING in a DELETE, INSERT, or REPLACE statement to retrieve the data rows modified by the statement.
- Supported the GTID replication feature extension in row mode.
- Supported transaction lock optimization.
- Enhanced the recycle bin to support TRUNCATE TABLE and automatic cleanup of tables in the recycle bin.
- Supported parallel DDL to speed up DDL operations for which to create indexes through three-phase parallel operations.
- Supported quick index column modification.
- Supported automatic statistics collection and cross-server statistics collection.

#### Performance optimizations

- Optimized the GTID lock conflicts when transactions were committed if `binlog_order_commits` was disabled.
- Accelerated MySQL startup by changing the InnoDB startup phase from single-threaded creation of Rsegs to multi-threaded creation.

#### Bug fixes

- Fixed the issue where the transaction did not end when the connection was closed after deadlock or lock wait.
- Fixed the issue where the `innodb_row_lock_current_waits` value was abnormal.
- Fixed the SQL type error in the audit plugin without USE DATABASE.
- Fixed the issue where tables smaller than `innodb_async_table_size` were also renamed during async drop of big tables.
- Fixed the issue with incorrect escape characters in the audit plugin.
- Fixed the issue of rollback after quick column modification.
- Fixed the possible crash when `trx_sys close` carried `xa`.
- Fixed the crash when merging derived tables.
- Fixed the issue with modifying `binlog_format` after writeset was enabled.
- Fixed the error (error code: 1032) caused by hash scans with A->B->A->C update on the same row.
- Fixed the issue where the sort index might be invalid in prepared statement mode.
- Fixed the issue where the operator that consumed the materialized result might be merged into the returned value path of the materialized operator and result in incorrect comprehension and display of the execution plan.
- Fixed exceptions in extreme cases for async drop of big tables.
- Fixed the abnormal error message when setting a SQL filter.
- Fixed the syntax error reported during stored procedure parsing.
- Fixed the issue where historical histograms couldn't be applied.
- Fixed the compatibility issue caused by the role column display in `SHOW SLAVE HOSTS(show replicas)`.
- Fixed the crash of `Item_in_subselect::single_value_transformer` when the number of columns was incorrect.
- Fixed the crash caused by memory leaks during cascading update if a subtable contained virtual columns and foreign key columns.


### 20211202
#### New features
- Supported quick column modification.
- Supported histogram versioning.
- Supported SQL:2003 TABLESAMPLE (single table) sampling control syntax for obtaining random samples of physical tables.
- Added non-reserved keywords: TABLESAMPLE BERNOULLI.
- Added the `HISTOGRAM()` function to build a histogram for a given input field.
- Supported compressed histograms.
- Supported SQL throttling (expected in April 2022 for DBbrain).
- Supported MySQL cluster role configuration (default role: CDB_ROLE_UNKNOWN).
- Added a new `Role` column to the `show replicas` command's display results to display roles.
- Supported proxy.

#### Performance optimizations
- Optimized the hotspot update problem caused by `insert on duplicate key update`.
- Accelerated the application of hash scan by aggregating multiple identical binlog events.
- Greatly reduced the memory usage by the `prepare` statement in point queries in the thread pool mode when the plan cache was enabled.

#### Bug fixes
- Fixed the error of unstable performance after hotspot update optimization was enabled.
- Fixed the issue where `select count(*)` parallel scans caused full-table scans in extreme cases.
- Fixed performance issues caused by execution plan changes due to reading zero statistics in various cases.
- Fixed the bug where queries were in the `query end` status for a long time.
- Fixed the bug where statistics were severely underestimated in long records.
- Fixed the bug where an error was reported when the Temptable engine was used and the number of aggregate functions in the selected column exceeded 255.
- Fixed the case sensitivity issue of column names in the `json_table` function.
- Fixed the bug that caused correctness issues in window functions because expressions returned early during `return true`.
- Fixed the correctness issue caused by the pushdown by `derived condition pushdown` when it contained user variables.
- Fixed the issue where SQL filters were prone to crash when no namespaces were added in a rule.
- Fixed the QPS jitters when the thread pool was enabled under high concurrency and high conflict.
- Fixed the issue where source-replica buffer pool sync leaked file handles in extreme cases (when host file systems were corrupted).
- Fixed the index mapping issue.
- Fixed the statistics cache sync issue.
- Fixed the crash when information was not cleared during execution of the `update` statement or stored procedures.

### 20210830
#### New features
- Supported limiting the number of preloaded rows.
- Supported optimizing plan cache check.
- Supported extended ANALYZE syntax (UPDATE HISTOGRAM c USING DATA 'json') and direct writes to histograms.

#### Performance optimizations
- Replaced index dive with histogram to reduce evaluation errors and I/O overheads (this capability is not enabled by default).

#### Bug fixes
- Fixed the issue where statistics information might be zero during online-DDL.
- Fixed the issue where columns generated from replica instances were not updated.
- Fixed the issue where the instance hung when binlog was compressed.
- Fixed the issue of missing GTID in the previous_gtids event of the newly generated binlog file.
- Fixed possible deadlocks when system variables were modified.
- Fixed the issue where the information of the SQL thread of the replica instance in SHOW PROCESSLIST was incorrectly displayed.
- Implemented the bug fix related to hash join provided in MySQL 8.0.23.
- Implemented the bug fix related to writeset provided in MySQL.
- Implemented the bug fix related to the query optimizer provided in MySQL 8.0.24.
- Fixed the concurrency bugs of optimizing flush list and releasing pages in FAST DDL.
- Optimized the memory usage during data dictionary update in instances with a large number of tables.
- Fixed the crash caused by new primary key creation after INSTANT ADD COLUMN.
- Fixed the OOM caused by memory growth in full-text index query.
- Fixed the issue where -1 was included in the TIME field in the result set returned by SHOW PROCESSLIST.
- Fixed the issue where tables might fail to be opened due to histogram compatibility.
- Fixed the floating point accumulation error when Singleton histograms were constructed.
- Fixed the replication interruption caused by using many Chinese characters in the table name of a row format log.

### 20210330
#### New features
- Supported source-replica buffer pool sync: After a high-availability (HA) source-replica switch occurs, it usually takes a long time to warm up the replica, that is, to load hotspot data into its buffer pool. To accelerate the replica's warmup, TXSQL now supports the buffer pool sync between the source and the replica.
- Supported sort merge join.
- Supported fast DDL operations.
- Supported querying the value of the `character_set_client_handshake` parameter.

#### Performance optimizations
- Optimized the mechanism of scanning and flushing the dirty pages tracked in the flush list, so as to solve the performance fluctuation issue while creating indexes and thus improve the system stability.

#### Bug fixes
- Fixed the deadlocks caused by the modification of the `offline_mode` and `cdb_working_mode` parameters.
- Fixed the concurrency issue while persistently storing `max_trx_id` of global object `trx_sys`.

### 20201230
#### New features
- Supported the official updates of MySQL [8.0.19](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html), [8.0.20](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html), [8.0.21](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html), and [8.0.22](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html).
- Supported dynamic setting of thread pooling mode or connection pooling mode by using the `thread_handling` parameter.

#### Performance optimizations
- Optimized the `BINLOG LOCK_done` conflict to improve write performance.
- Optimized the `trx_sys mutex` conflict by using lock free hash and improve performance.
- Optimized redo log flushing.
- Optimized the buffer pool initialization time.
- Optimized the clearing of adaptive hash indexes (AHI) during the `drop table` operations on big tables.
- Optimized audit performance.

#### Bug fixes
- Fixed performance fluctuation when cleaning InnoDB temporary tables.
- Fixed the read-only performance decrease when the instance has many cores.
- Fixed the error (error code: 1032) caused by hash scans.
- Fixed concurrency security issues caused by hotspot update.

### 20200630
#### New features
- Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported automatic killing of idle tasks to reduce resource conflicts. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported transparent data encryption (TDE).

#### Bug fixes
- Fixed the issue where switch failed due to inconsistent checkpoints between `relay_log_pos` and `master_log_pos`.
- Fixed the data file error caused by asynchronously storing data in the disk.
- Fixed the hard error when `fsync` returned `EIO` and retries were made repeatedly.
- Fixed the crash caused by phrase search under multi-byte character sets in full-text index.

## MySQL 5.7
### 20211230

#### New features

- Supported the official updates of MySQL [5.7.19](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-19.html) to [5.7.36](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-36.html).
- Supported source-replica buffer pool sync to speed up the performance recovery after HA switch (around 90 seconds faster than that in native mode).
- Added the backup lock feature to provide lightweight metadata locks to improve the service availability during backup.

#### Performance optimizations

- Made functions related to `utf8/utf8mb4 my_charpos` inline to optimize the performance of UTF_8 functions in read_write scenarios.
- Upgraded jemalloc to v5.2.1.
- Optimized file number acquisition during binlog rotation.
- Optimized semi-sync replica I/O.
- Optimized hash scan aggregation.
- Accelerated the startup of crash recovery for large transactions.

### 20211102
#### New features
- Fixed the exception of the third-party data subscription tool caused by subscription to the comparison SQL for internal data consistency during tool usage.
>?After the database instance is migrated, upgraded, or recovered after failure, the system will compare the data consistency to ensure the consistency of data. When comparison SQL is in `statement` mode, exceptions are easy to occur in response of some third-party subscription tools to the SQL in `statement` mode. When the instance is upgraded to its kernel, the third-party data subscription tool can't subscribe the comparison SQL for internal data consistency

### 20211031
#### New features
- Supported writeset replication.

#### Performance optimizations
- Optimized the checkpoint mechanism to increase the backup success rate.
- Optimized the hash scan index selection.
- Optimized the hotspot update performance to support `insert on duplicate key update`.

#### Bug fixes
- Fixed the error of unstable performance after hotspot update was enabled.
- Fixed the crash caused by rolling back the `update` operation after an instant DDL.
- Fixed the issue where the `create table select` statement didn't inherit the compression attribute after column compression was enabled.
- Fixed the instance crash caused by the `show variables like 'tencent_root%'` statement after the `skip-grant-table` option was enabled.
- Fixed the crash of the Query Rewriter plugin in read-only mode.
- Fixed the error (error code: 1032) caused by hash scans in partitioned tables.
- Fixed the issue where the first large transaction's SBM was 0 in MTS mode.
- Fixed the crash of `stop slave` caused by `slave_preserve_commit_order=ON, slave_transaction_retries=0`.
- Fixed several XA transaction bugs.
- Fixed the issue where SQL splicing went wrong during `show create` after a JSON field with a default value was created.
- Fixed the issue where disconnected transactions could not be rolled back after transactions were blocked.
- Fixed the issue where the statistics might be 0 under long records in InnoDB persistent mode.
- Ported 8.0 to fix the issue where `ANALYZE TABLE` might cause query retention.
- Fixed the issue where the InnoDB statistics couldn't be synced to the server layer in time after change.
- Fixed the issue where statistical sampling might block writes for too long and cause a crash (bug# 31889883).
- Fixed the possibility of reading zero rows during the InnoDB statistics update process (bug# 105224).
- Fixed the possible O(N^2) behavior in MVCC (bug# 28825617).
- Fixed the crash caused by closing a temp table and triggering binlog rotation when a connection was released.

### 20210630
#### New features
- Added the new command SHOW SLAVE DETAIL [FOR CHANNEL channel] for displaying the binlog timestamp that the current replica has replayed.
- Supported transaction_read_only/transaction_isolation parameters.

#### Performance optimizations
- Accelerated the application of hash scan on replicas by aggregating multiple identical binlog events.

#### Bug fixes
- Fixed the issue where duplicate primary keys existed, columns couldn't be found, and columns were too long in temp tables caused by the UPDATE statement.
- Fixed the issue where the statistics might be zero during the DDL process.
- Fixed the inaccurate undo log size in connection status statistics.
- Fixed the instance crash caused by querying the metadata_locks table.
- Modified `of` as a non-reserved keyword.
- Fixed the issue where the dynamically modified version number was not correctly displayed in new connections.
- Fixed the wild pointer of page_cache cleaning access.
- Fixed the issue where the execution of ALTER TABLE might report the "Incorrect key file for table" error.
- Fixed the excessive memory usage by partitioned tables.
- Fixed the issue where -1 was included in the TIME field in the result set returned by SHOW PROCESSLIST.
- Fixed the lock wait of XA transaction replication on replica nodes.
- Fixed the incorrect lock of partitioned tables in equal range query.

### 20210331
#### New features
- Supported RETURNING in a DELETE, INSERT, or REPLACE statement to retrieve the data rows modified by the statement. For DELETE, the returned data rows are pre-images, while for INSERT and UPDATE, they are post-images.
- Supported column compression: Row compression and data page compression are already supported, but if small fields in a table are read and written frequently while big fields are not, both of the compression methods waste a lot of computing resources. In contrast, column compression can compress big fields that are infrequently accessed and reduce the space for storing whole rows of fields, so as to improve read and write access efficiency.
- Supported querying the value of the `character_set_client_handshake` parameter.
- Supported the manual clearing of page cache occupied by log files by using the `posix_fadvise()` function based on the sliding window technique, so as to lower the memory pressure on the operating system and improve instance stability.

#### Performance optimizations
- Optimized the parallelism of CREATE INDEX: A merge sort is needed in a temp table in the process of creating indexes, which is time-consuming. To solve the issue, the parallel temp-table merge sort algorithm is now supported, reducing the time by more than 50%.
- Optimized the mechanism of scanning and flushing the dirty pages tracked in the flush list, so as to solve the performance fluctuation issue while creating indexes and thus improve the system stability.

#### Bug fixes
- Fixed the memory leak issue.
- Implemented the JSON bug fixes provided in MySQL 8.0 to improve the stability of using JSON.
- Fixed the error (error code: 1032) caused by hash scans.
- Fixed concurrency security issues caused by hotspot update.
- Implemented the gcol bug fixes provided by MySQL in batches.
- Fixed the failure to compare DateTime data with String data in some cases.
- Fixed the bug where file handles cannot be released if source-replica buffer pool sync is enabled.
- Fixed the deadlocks caused by setting the `offline_mode` parameter and creating connections at the same time.
- Fixed the crashes caused by the `m_end_range` parameter incorrectly set in concurrent range queries.
- Fixed the issue where it takes a long time to execute an UPDATE statement on a temp table if a JSON column appears in the GROUP BY clause.

### 20201231
#### New features
- Supported using `NOWAIT` and `SKIP LOCKED` in `SELECT FOR UPDATE/SHARE` statements.
- Supported dynamic setting of thread pooling mode or connection pooling mode by using the `thread_handling` parameter.
- Supported source-replica buffer pool synchronization.
- Supported monitoring of user connection status. Monitoring items include sync/async IO, memory, log size, CPU time, lock duration, etc.

#### Performance optimizations
- Optimized the transaction subsystem to improve the high concurrency performance.
- Optimized the time to start crash recovery for large transactions.
- Optimized redo log flushing.
- Optimized the buffer pool initialization time.
- Optimized UTF8/UTF8MB4 string efficiency.
- Optimized audit performance.
- Revoked the restriction on the value of `gtid_purged` being empty.
- Optimized the backup lock. `LOCK TABLES FOR BACKUP`, `LOCK BINLOG FOR BACKUP`, and `UNLOCK BINLOG` are supported. `FLUSH TABLES WITH READ LOCK` is used to take a backup of the database, but it blocks the whole database from providing service. In contrast, the three statements above use a lightweight backup lock to ensure data consistency during physical/logical backup while allowing the database to providing service.
- Optimized the `drop table` operations on big tables.

#### Bug fixes
- Fixed the hang issue when querying `performance_schema`.
- Fixed the overflow of the `digest_add_token` function.
- Fixed the crashes when accessing ibuf using the `truncate table` statement.
- Fixed incorrect queries when `const` in `left join` statements was calculated earlier than it should.

### 20200930
#### Performance optimizations
- Optimized the backup lock. 
`FLUSH TABLES WITH READ LOCK` is used to take a backup of the database, but it blocks the whole database from providing service. Therefore, a lightweight backup lock is provided in this version.
- Optimized the `drop table` operations on big tables. 
The `innodb_fast_ahi_cleanup_for_drop_table` parameter helps significantly reduce the time it takes to clean up adaptive hash indexes when dropping big tables.

#### Bug fixes
- Fixed the crashes when accessing ibuf using the `truncate table` statement.
- Fixed cold backup failures when the quick column adding feature was enabled.
- Fixed performance degradation caused by frequently releasing InnoDB memory table objects.
- Fixed incorrect queries when `const` in `left join` statements was calculated earlier than it should.
- Fixed the core issue caused by rule class name conflict between SQL throttling and query rewrite.
- Fixed the concurrent update issue caused by the `insert on duplicate key update` statement in multiple sessions.
- Fixed the `duplicate key error` caused by concurrently inserting data into auto_increment columns.
- Fixed the crashes caused by evicting InnoDB memory objects.
- Fixed concurrency security issues caused by hotspot update.
- Fixed the coredump issue when enabling the thread pool after jemalloc was upgraded to v5.2.1.
- Fixed the incomplete audit log due to fwrite error-free handling.
- Fixed the issue where mysqld_safe failed to print logs when it was started as `root`.
- Fixed the increase in the size of the DDL log file caused by `alter table exchange partition`.

### 20200701
#### Bug fixes
- Fixed the `INNOBASE_SHARE index mapping` error.

### 20200630
#### New features
- Supported using `NOWAIT` and `SKIP LOCKED` in `SELECT FOR UPDATE/SHARE` statements.
- Supported large transaction optimization, which can solve such problems as source-replica delay and backup failures caused by large transactions.
- Optimized audit performance: Async audit is supported.

#### Bug fixes
- Fixed the overflow of the `digest_add_token` function.
- Fixed the instance crash caused by `insert blob`.
- Fixed the source-replica replication interruption when a hash scan failed to find the record while updating the same row in an event.
- Fixed the hang issue when querying `performance_schema`.

### 20200331
#### New features
- Added the official MySQL 5.7.22 JSON series functions.
- Supported the hotspot update feature as described in [Real-Time Session](https://intl.cloud.tencent.com/document/product/1035/48638) feature for ecommerce flash sale scenarios.
- Supported SQL throttling as described in [Real-Time Session](https://intl.cloud.tencent.com/document/product/1035/48638).
- Supported encryption with custom KMS keys.

#### Bug fixes
- Fixed the crash caused by phrase search under multi-byte character sets in full-text index.
- Fixed the crash of the CATS lock scheduling module in high-concurrence scenarios.

### 20190830
#### New features
- Supported skipping the corrupted data and continuing to parse when a binlog is corrupted. If the source instance and binlog are both damaged, this feature helps restore data from the replica database for use as much as possible.
- Supported syncing data from non-GTID to GTID mode.
- Supported querying the "user thread memory usage" by executing the `show full processlist` statement.
- Supported [quick column adding](https://intl.cloud.tencent.com/document/product/236/35988) for tables. This feature does not replicate the data or use disk capacity/IO, and can implement changes in real time during peak hours.
- Supported persistent auto-increment values.

#### Bug fixes
- Fixed the issue where replication would be interrupted if the column name in a `GRANT` statement contained reserved words.
- Fixed the issue where SQL execution efficiency dropped when reverse scan was performed on a partitioned table.
- Fixed the issue where the query result had an exception due to data inconsistency when using virtual column index and primary key.
- Fixed the issue where data was missing due to InnoDB primary key range queries.
- Fixed the issue where the system crashed when a DDL statement was executed for a table with spatial indexes.
- Fixed the issue where source-replica disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.
- Fixed the issue where other events could not be executed as scheduled when an event was deleted.
- Fixed the issue where the aggregate query result was incorrect.

### 20190615
#### New features
- Supported transparent data encryption (TDE).

### 20190430
#### Bug fixes
- Fixed the issue where null pointer reference occurred when the LONGTEXT feature was used in subqueries.
- Fixed the issue where source-replica disconnection occurred due to hash scan.
- Fixed the issue where the replica I/O thread was interrupted due to source binlog switch.
- Fixed the crash caused by the use of `NAME_CONST`.
- Fixed the illegal mix of collation error caused by character set.

### 20190203
#### New features
- Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported CATS lock scheduling.
- Supported creating and dropping temp tables and CTS syntax in transactions when GTID is enabled. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported implicit primary keys. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported users without super privileges to kill sessions of other users by configuring the `cdb_kill_user_extra` parameter (default value: `root@%`).
- Supported enterprise-grade encryption functions. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Bug fixes
- Fixed the issue where replication was interrupted when binlog cache file ran out of space.
- Fixed the hard error when `fsync` returned `EIO` and retries were made repeatedly.
- Fixed the issue where replication was interrupted and could not be recovered due to GTID holes.
  
### 20180918
#### New features
- Supported automatic killing of idle transactions to reduce resource conflicts. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported automatically changing the storage engine from MEMORY to InnoDB: if the global variable `cdb_convert_memory_to_innodb` is `ON`, the engine will be changed from MEMORY to InnoDB when a table is created or modified.
- Supported invisible indexes.
- Supported memory management with jemalloc, which can replace the jlibc memory management module to reduce memory usage and improve allocation efficiency.
  
#### Performance optimizations
- Optimized binlog switch to reduce the `rotate` lock duration and improve system performance.
- Increased the crash recovery speed.
  
#### Bug fixes
- Fixed the issue where an event became invalid due to source-replica switch.
- Fixed the crash caused by `REPLAY LOG RECORD`.
- Fixed the issue where the query result was incorrect due to loose index scans.

### 20180530
#### New features
- Supported SQL auditing.
- Supported table-level concurrent replication. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
  
#### Performance optimizations
- Optimized replica instance locks to improve the performance synchronization of replica instances.   
- Optimized the pushdown of the `select ... limit` statement.
  
#### Bug fixes
- Fixed the issue where switch failed due to inconsistent checkpoints between `relay_log_pos` and `master_log_pos`.
- Fixed the crash caused by `Crash on UPDATE ON DUPLICATE KEY`.
- Fixed the `Invalid escape character in string.` error when a JSON column was imported.
  
### 20171130
#### New features
- Supported the `information_schema.metadata_locks` view to query the MDL grant and wait status in the current instance.
- Supported the `ALTER TABLE NO_WAIT | TIMEOUT` syntax to grant DDL operations wait timeout. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported the thread pool. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Bug fixes
- Fixed the error of `innodb_buffer_pool_pages_data` parameter overflow by calculating it based on `bytes_data`.
- Fixed the issue where speed limit plugin became unavailable in async mode.

## MySQL 5.6
### 20220302
#### Bug fixes
- Fixed the memory leak issue in `sql_update.cc`.

### 20220301
#### New features
- Supported dynamically configuring the spin cycle (0–100) with the dynamic parameter `innodb_spin_wait_pause_multiplier`.
This parameter is used for temporary adjustment and does not support fixing the change through the console.
- Supported printing deadlock loop information.
After this feature is enabled through the parameter `innodb_print_dead_lock_loop_info`, when a deadlock occurs, you can run `show engine innodb status` to view the deadlock loop information.

#### Bug fixes
- Fixed the issue where anonymous GTID transactions were generated in memory tables after replica restart.
- Fixed the issue where upgrade failed due to the missing root@localhost permission.
- Fixed the issue where the values of monitoring variables such as `innodb_row_lock_current_waits` were abnormal.
- Fixed the SQL type mapping error in the audit plugin.

### 20211030
#### New features
- Supported large transaction replication optimization.

#### Performance optimizations
- Optimized the application speed of hash scan.

#### Bug fixes
- Fixed the OOM caused by a large number of table queries.
- Fixed the infinite loop error caused by setting `innodb_thread_concurrecy` to 0.
- Fixed the issue where the statistics of long records were 0.
- Fixed the SBM jump error.
- Fixed the `LOCK_binlog_end_pos hang` error.

### 20210630
#### New features
- Supported large transaction replication optimization.

#### Bug fixes
- Fixed the incorrect copy when index merge was enabled.
- Fixed the issue where the replication would be interrupted if the execution of CREATE TABLE SELECT was interrupted when cdb_more_gtid_feature_supported was enabled in row mode.
- Fixed the bug that max(id) was greater than AUTO_INCREMENT in SHOW CREATE TABLE.

### 20201231
#### Bug fixes
- Fixed the error (error code: 1032) caused by hash scans. 
- Fixed the issue where REPLACE INTO does not update AUTO_INCREMENT columns in row-based replication.
- Fixed the memory leak caused by not freeing up the memory requested for parsing SQL statements.
- Fixed the issue where the sql_mode check is skipped when running CREATE TABLE AS SELECT.
- Fixed the issue where the sql_mode check is skipped when inserting default values.
- Fixed the issue where the sql_mode check is skipped when running UPDATE with bound parameters.

### 20200915
#### New features
- Supported SQL throttling as described in [Real-Time Session](https://intl.cloud.tencent.com/document/product/1035/48638).

#### Performance optimizations   
- Optimized the initialization acceleration of buffer pool.

#### Bug fixes
- Fixed the hang issue of `rename table` on both source and replica. 
- Fixed the crash when `event_scheduler` was set to `disable` and `cdb_skip_event_scheduler` was changed from `on` to `off`. 
- Fixed the `sync_wait_array` assertion failure when the maximum number of connections of `tencentroot` was not counted in `srv_max_n_threads`. 
- Fixed the crash of source-replica parallel replication caused by the system table structure inconsistency between TencentDB for MySQL v5.6 and other cloud vendors' MySQL v5.6. 
- Fixed the `INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW` error. 
- Fixed the error of `index_mapping`. 
- Fixed the MTR failure. 
- Fixed the source-replica replication interruption when a hash scan failed to find the record while updating the same row in an event. 

### 20190930
#### New features
- Supported querying the "user thread memory usage" by executing the `show full processlist` statement.  

#### Bug fixes
- Fixed GTID holes caused by the replication filter of the replica.
- Fixed the issue where source-replica disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.
- Fixed the illegal mix of collation error caused by character set.
- Fixed the issue where the source-replica disconnection occurred due to hash scan.
- Fixed the crash caused by the use of `NAME_CONST`.
- Fixed the issue where the replica I/O thread was interrupted due to source binlog switch.
- Fixed the error of incompatible backups due to `innodb_log_checusum`.

### 20190530
#### Bug fixes
- Fixed the issue where dirty data might be read in RC mode.
- Fixed the issue where replica instance replay might fail due to the drop of temp table.
- Fixed the error of deadlock under high concurrency.
  
### 20190203
#### New features
- Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported users without super privileges to kill sessions of other users by configuring the `cdb_kill_user_extra` parameter (default value: `root@%`).
- Supported creating and dropping temp tables and CTS syntax in transactions when GTID is enabled. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
  
#### Performance optimizations   
- Optimized the replication and replay of partitioned tables to improve efficiency.
  
#### Bug fixes
- Fixed the error of data inconsistency between source and replica due to insufficient temporary space.
- Fixed the error of suspended hot record updates.
- Fixed the issue where the `Seconds_Behind_Master` value had an exception during concurrent replication.

### 20180915
#### New features
- Supported automatically changing the storage engine from MEMORY to InnoDB: if the global variable `cdb_convert_memory_to_innodb` is `ON`, the engine will be changed from MEMORY to InnoDB when a table is created or modified.
- Supported automatic killing of idle transactions to reduce resource conflicts. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
  
#### Bug fixes
- Fixed the crash caused by `REPLAY LOG RECORD`.
- Fixed the error of time data inconsistency between source and replica due to decimal precision issues.

### 20180130
#### New features
- Supported the thread pool. To apply for this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Supported dynamically modifying replication filtering rules for replica nodes.

#### Performance optimizations
- Reduced performance fluctuation caused by `drop table`.
  
#### Bug fixes
- Fixed the issue where the database crashed due to authentication password strings.
  
### 20180122
#### New features
- Supported SQL auditing.

#### Bug fixes
- Fixed the error of integer overflow.
- Fixed the error caused by queries using full-text index.
- Fixed the issue where the replica crashed during replication.
	
### 20170830
#### Bug fixes
- Fixed the issue where binlog speed limit became invalid in async mode.
- Fixed the issue where the `buffer_pool` status had an exception.
- Fixed the issue where `SEQUENCE` and implicit primary key conflicted.
  
### 20170228
#### Bug fixes
- Fixed the character encoding bug in `drop table`.
- Fixed the issue where special symbols such as decimal point in a database or table could not be properly filtered by the `replicate-wild-do-table` statement.
- Fixed the issue where SQL threads exited too early after the replica had a `rotate` event.
  
### 20161130
#### Performance optimizations
- Split the `lock_log` lock to reduce the time used by lock log and improve the concurrency performance.
- Separated the ACK thread of the source to improve the response time.
- Prohibited the user thread from being killed while waiting for ACK in order to prevent phantom reads.
- Fixed the unnecessary `lock_sync` lock when `sync_binlog != 1`.
