### How do I modify the time zone in TencentDB for SQL Server?
TencentDB for SQL Server uses the China Standard Time by default, which cannot be modified.

### How do I modify character sets/collations in TencentDB for SQL Server?
TencentDB for SQL Server provides character sets/collations at instance and database levels.
- The character set/collation for instances is `Chinese_PRC_CI_AS` by default, which cannot be modified.
- The character set/collation for databases can be specified during database creation. For more information, see [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780). If it is not specified, `Chinese_PRC_CI_AS` will be used by default.

### How do I modify the configuration parameters of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select **Parameter Configuration** > **Parameter Settings*, and modify instance parameters. For more information, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/238/41609).

### Which parameters can I modify quickly in the TencentDB for SQL Server console?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select **Parameter Configuration** > **Parameter Settings*, and you can modify the following instance parameters:
- fill factor (%)
- max worker threads
- cost threshold for parallelism
- max degree of parallelism
- optimize for ad hoc workloads
- min server memory (MB)
- blocked process threshold (s)

[](id:CSXGLS)
### How do I view parameter modification logs in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select **Parameter Configuration** > **Modification Log**, and view parameter modification logs. For more information, see [Viewing Parameter Modification Log](https://intl.cloud.tencent.com/document/product/238/41610).
