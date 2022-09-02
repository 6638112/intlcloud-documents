## Feature Overview
The data migration feature refers to data replication between different data sources. DTS supports non-stop data migration to minimize the impact of database downtime on the business. It is applicable to diverse business scenarios, including data migration to Tencent Cloud, cross-TencentDB instance data migration, and data migration from third-party cloud databases to TencentDB. 

## How It Works
 The following takes MySQL as an example to describe the data migration process:
- Source database export: All existing data in the source database is exported.
- Data import: Existing data is imported into the target database.
- Incremental data sync and data check: Binlog takeover will begin when a migration task is started. During migration, SQL operations in the source database are written to the binlog, which DTS parses to write incremental data generated during existing data migration into the target database.
![](https://qcloudimg.tencent-cloud.cn/raw/2b7a50c41be8d18a389b6bb5ffcba791.jpg)

## Typical Use Cases
#### Data migration to Tencent Cloud
It simply takes a few steps in DTS to set up data migration to Tencent Cloud without any complicated configuration. The migration process does not interrupt the service provided by your source database, thereby minimizing the impact of cloudification on your business.
![](https://qcloudimg.tencent-cloud.cn/raw/491739f110738c80e2a8d7406c8ef7cd.png)

## Restrictions  
- Only basic tables and views can be migrated, and objects such as functions, triggers, and stored procedures are not supported currently (such unsupported migration objects will be gradually supported in the future).
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, view/table reference by stored procedures/functions/triggers, and tables correlated through primary/foreign keys.

## Supported Migration Types
DTS supports the following three migration types:
- Structured migration: The structure of the migration objects in the source database is migrated to the target database.
- Full migration: All data except system tables in the source database is migrated to the target database at a time. Full migration is one-time migration and is applicable to scenarios where the source database has no data writes.
- Full + incremental migration: Full migration is performed first to initialize the target database, and then the incremental data is migrated. Technical methods such as log parsing are used to keep the data between the source and target databases consistent. Full + incremental migration is applicable to scenarios where the source database has data writes.
- If you select full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental migration.

## Supported Database Types
For more information on the source and target database types, versions, and migration types supported for data migration, see [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).

## Supported Advanced Features

| **Feature**          | **Description**                        | **Documentation**                           |
| ------------------------- | ----------------------------------- | -------------------------------------- |
| Heterogeneous migration and migration from third-party cloud databases | Data migration between databases in different types is supported, such as migration from MySQL to TDSQL-C. Currently supported third-party cloud databases include Alibaba Cloud and AWS databases. | [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647)                                     |
| Cross-account migration                           | Data migration between different Tencent Cloud accounts is supported.                              | [Cross-account TencentDB Instance Migration](https://intl.cloud.tencent.com/document/product/571/42646) |
| Cross-version migration of most databases              | The target database version should be equal to or later than the source database version; for example, data on v5.5.x can be migrated to v5.5.x, v5.6.x, or later. The last digit in the version number is the minor version number, which is not restricted. | [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647)                                     |
| Migration of user information, views, and advanced objects | User information, views, stored procedures, functions, triggers, and events can be migrated. | - |
| Data consistency check | The data in the source and target databases can be checked for consistency. | [Creating Data Consistency Check Task](https://intl.cloud.tencent.com/document/product/571/42724) |
| Task progress visualization                    | Information such as migration steps and progress can be displayed.                         | [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637) |
| Metric monitoring and default alarm policy          | <li>Data migration metrics can be monitored. <li>Default configuration is supported for data migration event monitoring to automatically notify you of abnormal events. | [Supported Events and Metrics](https://intl.cloud.tencent.com/document/product/571/42611)                   |
| Migration without locks                             | Migration is implemented without locks, during which no global lock (the FTWRL lock) is added, and only tables without a primary key are locked. | -    |
| Table mapping                       | Tables migrated from the source database to the target database can be renamed.                      | [Table Mapping](https://intl.cloud.tencent.com/document/product/571/48482)                                                |
| Instance restart or upgrade                | During incremental data migration, the instances can be restarted or upgraded.                 | -                   |
| HA switch                           | HA switch from the source database (with GTID enabled) to the target database is supported.     | -             |
| No requirements for the super privileges                   | The operator does not need to have the super privileges of the source database account (only for certain databases currently). | -         |

