
Resource-level permission can be used to specify which resources a user can manipulate. TDSQL-C for MySQL supports certain resource-level permissions. This means that for TDSQL-C for MySQL operations with resource-level permissions, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| --------------------------------------------------- | ------------------------------------------------------------ |
|  [Cluster APIs](#xiangguan) |`qcs::cynosdb:$region::instance/*`<br>`qcs::cynosdb:$region:$account:instanceId/$clusterId` |

The table below lists the TDSQL-C for MySQL API operations which currently support resource-level permission control as well as the resources supported by each operation. When specifying a resource path, you can use the `*` wildcard in the path.
>?Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

#### [Cluster APIs](id:xiangguan)

| API Operation | Resource Path |
| ------------------------------ | ------------------------------------------------------------ |
| DescribeBackupConfig           | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeBackupList             | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeRollbackTimeRange      | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeRollbackTimeValidity   | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyBackupConfig             | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ActivateCluster                | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterDetail          | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| IsolateCluster                 | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyClusterName              | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyClusterProject           | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| OfflineCluster                 | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DeleteAccounts                 | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeAccounts               | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyAccountDescription       | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ResetAccountPassword           | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterInstanceGrps    | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ActivateInstance               | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeInstanceDetail         | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| IsolateInstance                | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| UpgradeInstance                | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyInstanceName             | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| OfflineInstance                | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterAddr            | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterNetService      | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterParams          | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusterServerInfo      | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeErrorLogs              | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeMaintainPeriod         | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeSlowLogs               | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyClusterParam             | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyMaintainPeriodConfig     | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeDBSecurityGroups       | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| ModifyDBInstanceSecurityGroups | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| CloseWan                       | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| OpenWan                        | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeClusters               | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeInstances              | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |
| DescribeIsolatedInstances      | `qcs::cynosdb:$region:$account:instanceId/*`    `qcs::cynosdb:$region:$account:instanceId/$clusterId` |


