This document describes the TDSQL-C for MySQL kernel version updates. For information on how to upgrade the kernel, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617?).

## TDSQL-C for MySQL 8.0
### 3.1.2
#### Feature updates
- Supported MySQL 8.0 for read-only nodes and source-replica physical replication.
- Supported table space expansion and up to above 1 PB of capacity per instance.
- Supported limiting the number of preloaded rows, which achieved a 1%-5% performance increase during point query testing.
- Supported extended ANALYZE syntax (UPDATE HISTOGRAM c USING DATA 'json') and direct writes to histograms.

#### Performance optimizations
- Replaced index dive with histogram to reduce evaluation errors and I/O overheads (this capability is not enabled by default).

#### Fixes
- Fixed the issue where updates related to large object pages were not written to the log when a full-text index containing large object columns was created.
- Fixed the issue with inconsistent formats of `undo page` and different definitions of `TRX_UNDO_HISTORY_NODE` in the computing and storage layers.
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

### 3.1.1
#### Feature updates
- Supported the official updates of MySQL 8.0.19, 8.0.20, 8.0.21, and 8.0.22.
- Supported dynamic setting of thread pooling mode or connection pooling mode by using the `thread_handling` parameter.
- Supported source-replica buffer pool sync: After a high-availability (HA) source-replica switch occurs, it usually takes a long time to warm up the replica, that is, to load hotspot data into its buffer pool. To accelerate the replica's warmup, TXSQL now supports the buffer pool sync between the source and the replica.
- Supported sort merge join.
- Supported async commit: With the thread pool enabled and binlog disabled, async commit can be enabled by setting the parameter `innodb_log_sync_method` to `async`.
- Supported fast DDL operations.
- Supported querying the value of the `character_set_client_handshake` parameter.
- Supported database audit.

#### Performance optimizations
- Optimized the mechanism of scanning and flushing the dirty pages tracked in the flush list, so as to solve the performance fluctuation issue while creating indexes and thus improve the system stability.
- Optimized the `BINLOG LOCK_done` conflict to improve write performance.
- Optimized the `trx_sys mutex` conflict by using lock free hash and improve performance.
- Optimized redo log flushing.
- Optimized the buffer pool initialization time.
- Optimized the clearing of adaptive hash indexes (AHI) during the `drop table` operations on big tables.
- Optimized the `BINLOG LOCK_done` conflict to improve write performance.
- Optimized the `trx_sys mutex` conflict by using lock free hash and improve performance.
- Optimized redo log flushing.
- Optimized the buffer pool initialization time.
- Optimized the clearing of adaptive hash indexes (AHI) during the `drop table` operations on big tables.

#### Fixes
- Fixed the deadlocks caused by the modification of the `offline_mode` and `cdb_working_mode` parameters.
- Fixed the concurrency issue while persistently storing `max_trx_id` of global object `trx_sys`.
- Fixed performance fluctuation when cleaning InnoDB temporary tables.
- Fixed the read-only performance decrease when the instance has many cores.
- Fixed the error (error code: 1032) caused by hash scans.
- Fixed concurrency security issues caused by hotspot update.

### 3.0.1
#### Feature updates
- Supported three methods of querying `cynos_version`: `select CYNOS_VERSION()`, `select @@cynos_version`, and `show variables like 'cynos_version'`.
- Added a space limit parameter. If the total space usage exceeds the limit, an error will be reported to prompt you to release the space or upgrade the specification.
- Added the `innodb_ncdb_log_priority` read-only parameter, which indicates the priority of the source instance's backend log thread.
- Added the `innodb_ncdb_apply_priority` read-only parameter, which indicates the priority of the read-only instance's log replay thread.
- Added the `innodb_ncdb_fast_shutdown` dynamic parameter, which controls whether to quickly shut down processes. After it is enabled, when a process exits, no destruction operations on the global structure will be performed, which reduces the shutdown time. It is disabled by default.
- Added the `innodb_max_temp_data_file_size` read-only parameter. Its default value is 128 MB. If its value is greater than 0, it indicates the maximum size of the temp tablespace in the local storage.

## TDSQL-C for MySQL 5.7
### 2.0.16
#### Feature updates
- Optimized `undo space truncate` to improve the speed of `undo truncate` on large-spec instances.
- Optimized the performance of large-scale queries on read-only instances.

#### Fixes
- Fixed the issue where `backup lock` couldn't be locked due to the `lock table` statement.
- Fixed the issue where `table share` went wrong after thousands of columns were added through `instant add`.
- Fixed the replay error when the content of binlog contained escaped keywords.
- Fixed the issue where externally prepared XA transactions were not explicitly rolled back and thus blocked normal shutdown.
- Fixed the issue where the warning "tablespace -1 not found" was reported during read-only instance startup.

### 2.0.15
#### Feature updates
- Supported the extended table space: When a single table space exceeds the `innodb_ncdb_extend_space_threshold` configuration, a new table will be created in the extended table space.
- Added new JSON functions: JSON_MERGE_PRESERVE, JSON_MERGE_PATCH, JSON_PRETTY, JSON_STORAGE_SIZE, JSON_ARRAYAGG, JSON_OBJECTAGG.
- Optimized the table lock recovery process at system startup to shorten the startup time.

#### Fixes
- Fixed the bugs for the `group by` performance issue in text columns and multiple issues related to virtual columns.
- Fixed the possible crash when large transaction rollback and shutdown operations were performed concurrently after instance startup.
- Fixed the issue where repeatedly failed IO retries of related pages caused instance exit after `undo space truncate` failed.
- Fixed the crash when statistics update accessed the snapshot cache for disabled read-only instances.
- Fixed the issue where the truncation log might be behind the `truncate` operation in `undo space truncate`.
- Fixed the bug where an error in ICP check for partitioned table scan resulted in slow query.
- Fixed the crash when the previous scan in a read-only instance encountered the partial replay of a split index log.

### 2.0.14
#### Feature updates
- Supported INSTANT MODIFY COLUMN. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44589).

#### Fixes
- Fixed the issue where the used space was not reclaimed when a temp table in a read-only instance was dropped.
- Fixed the issue where the process exited when a read-only instance read the old page version due to changes in storage routes.
- Fixed the issue of possible crash when `information_schema.metadata_locks` was queried.
- Fixed the concurrency error of forward scan and B-tree SMO in read-only instance.
- Fixed the issue where when multiple tables had complex foreign key dependencies and the foreign key attribute was `ON DELETE CASCADE`, the corresponding record in a child table might be deleted twice when a record was delete in its parent table with DELETE.
- Fixed the issue where the process exited due to operations such as CREATE USER in a read-only instance.
- Fixed the issue where SHOW VOLUME STATUS in a read-only instance might trigger an assertion failure.
- Fixed the issue where a read-only instance had exceptional query results and crashed when DDL operations were performed in partitioned tables frequently.
- Fixed the issue where the process crashed during historical version construction when an read-only instance scanned a purged undo log.

### 2.0.13
#### Feature updates
- Supported INSTANT ADD COLUMN. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44589).
- Optimized the audit performance under high load and added the `lock_usleep_time` dynamic parameter.

#### Fixes
- Fixed the issue where `dict_operation_lock` might cause deadlock during foreign key check.
- Fixed the issue where the process might exit when the ACL change log was replayed during read-only instance startup.
- Fixed the issue where data in source and replica instances was inconsistent after INSTANT ADD COLUMN and TRUNCATE TABLE.
- Fixed the log replay error occurring when data was inserted again after INSTANT ADD COLUMN and TRUNCATE TABLE.
- Fixed the issue where the process exited when a primary key containing a column added by INSTANT ADD COLUMN was created.
- Fixed the issue where the process exited during table structure query in a read-only instance when INSTANT COLUMN was used to create or rebuild a partition.

### 2.0.12
#### Feature updates
- Supported database audit. For more information on how to use it, see [Enabling TDSQL-C Audit](https://intl.cloud.tencent.com/document/product/1102/41312).
- Supported purging page read-ahead to accelerate space reclaim.
- Supported real-time update of the size information of tables and indexes in the system view.
- Added a thread to accelerate recycle LSN and storage GC.

#### Fixes
- Fixed official bugs in full-text index, including BUG#24938374, BUG#21625016, BUG#27082268, BUG#27155294, BUG#27326796, BUG#27304661, BUG#25289359, BUG#29717909, and BUG#30787535.
- Fixed official bugs where concurrent update might cause system crashes, including BUG#30950714, BUG#31205266, and BUG#25669686.
- Fixed the official bug BUG#28104394 where uncommitted INSERT operations would affect the range scan created by an index and made it return an incorrect number of rows.
- Fixed the official bug BUG#30488700 where an incorrect query execution plan of a derived table could result in a poor performance.
- Fixed the issue where the process exited when a read-only instance replayed statistics logs after the source (read-write) instance executed a DDL statement.
- Fixed the issue where RENAME TABLE was performed on a database that did not exist.
- Fixed the issue where a read-only instance might exit when OPTIMIZE TABLE was used for the source instance.
- Fixed the issue where transactions were inconsistent after a table with a full-text index was updated in a read-only instance.
- Fixed the deadlock occurring during SET OFFLINE MODE and SHOW VARIABLES operations.

### 2.0.11
#### Feature updates
- Optimized the binlog file index to accelerate binlog file scan.
- Optimized the shutdown process to make it faster.
- Optimized the instance memory to reduce the memory usage by structures such as buffer, ZIP, and hash.
- Optimized the DDL lock recovery process during read-only instance startup to accelerate replay.
- Optimized system table loading in read-only instance to accelerate startup.
- Optimized worker thread assignment during PURGE COORDINATOR to accelerate purge.

#### Fixes
- Fixed the issue where the process crashed during OPEN TABLE due to incorrect index structure mapping.
- Fixed the issue where read-only instance replication was exceptional during XA transaction rollback.
- Fixed the issue where startup crashed when binlog replication was started in a read-only instance.
- Fixed the memory leak caused by FLUSH LOGS.
- Fixed the shutdown failure of `mysqladmin shutdown`.
- Fixed the issue where a read-only instance failed to replay logs when DROP COLUMN was performed on the source instance.
- Fixed the issue where data could still be input after space restriction was triggered when a BLOB was inserted.
- Fixed the issue of read-only instance replication availability that might be caused by DDL statements in big tables or slow log storage in the source instance.
- Fixed the issue where storage wasted small tables after `innodb_max_temp_data_file_size` was set for a temp table.
