## Overview
You can migrate an instance to another availability zone (AZ) within the same region. All attributes and configurations (including the private network address and the subnet) of the instance remain unchanged after migration. The amount of time required is proportional to the volume of data in the instance. The more data there is, the longer the data migration takes. In addition, the instance access is not affected during migration.

## Supported Instance Types
- Primary instances of high availability edition and cluster edition are supported.
>?If a primary instance of high availability edition or cluster edition has read-only instances or implements the pub/sub messaging paradigm, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to migrate it across AZs.
- Basic edition instances are not supported.
- Read-Only instances are not supported.

## Prerequisite
The region where the instance resides must have multiple AZs.

## Impact
- An ongoing migration cannot be canceled.
- The name, access IP, and access port of the instance remain unchanged after migration.
- Data migration will occur during the instance's migration to another AZ. During the data migration, the instance can be accessed normally and your business will not be affected.
-  The amount of time required is proportional to the volume of data in the instance. The more data there is, the longer the data migration takes. 
- An instance switch will occur after migration, causing a flash disconnection. You can specify the switch time.

## Directions
### Migrating across AZs
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. In the **Basic Info** section, click **Migrate across AZs** to access the cross-AZ migration page.
![](https://qcloudimg.tencent-cloud.cn/raw/2de60347d9a5265ae2b227821a488d63.png)
3. View the original AZ of the instance, specify the target AZ, enable/disable multi-AZ deployment, select the switch time, check the box to agree to the cross-AZ migration rules, and click **Submit**.
>?After you click **Submit**, instance data will be migrated to the target AZ at the underlying layer without affecting instance running and access.
>After instance data is migrated, an instance switch will occur (**upon migration completion** or **during maintenance time**), causing a flash disconnection. After the switch is done, the whole process of cross-AZ migration is completed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a92d8a7615296b87a6d630887b503660.png)

### Viewing migration tasks
You can view cross-AZ migration tasks in the **Running Tasks** box in the upper-right corner of the **Database Management** tab.
<img src="https://qcloudimg.tencent-cloud.cn/raw/577730c9f93171b1b01277c71afa5146.png" style="zoom:50%;" />

### Performing immediate switch
If the instance is scheduled to be switched during the maintenance time according to the configurations of its cross-AZ migration task, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column in the instance list in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).

