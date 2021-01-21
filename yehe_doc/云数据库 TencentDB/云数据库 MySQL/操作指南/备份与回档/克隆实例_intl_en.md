This document describes how to clone a TencentDB for MySQL instance and quickly restore data to the newly purchased clone in the console.

## Overview
You can clone a TencentDB for MySQL instance, and restore the clone to any point in time within the log backup retention period or from the backup set of a specific physical backup. The clone is a new instance created from the backup data according to the restoration point in time you have specified. After the clone has been verified, you can migrate its data back to the original instance with [DTS](https://intl.cloud.tencent.com/document/product/571/13709) or you can start using the clone.

#### Clone mode
- Clone an instance and restore the clone to any point in time within the log backup retention period you set.
- Clone an instance and restore the clone from the backup set of a specific physical backup within the data backup retention period you set.

#### Billing of the clone
- The clone adopts the pay-as-you-go billing mode. For more information about the billing mode and fee calculation, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/236/18335).
- The clone will not be billed until the clone process is completed.  

## Prerequisites
- Instance version: MySQL High-Availability Edition and Finance Edition
- The original instance must be in the "Running" status.
- If the clone mode is set to **By backup set**, the original instance must have created at least one physical backup. You can log in to the [console](https://console.cloud.tencent.com/cdb), select **Database Backup** on the left sidebar, and view backup status on the **Backup List** tab.
- The balance of your account must be positive.

## Notes
- The hard disk space of the clone must be larger than the amount of the data to be cloned from, or else the clone task may fail.
- The availability zone, database version, replication mode, and default database parameters of the clone must be the same as those of the original instance.
- The clone will not be displayed in the instance list in the console until the clone process is completed.

## Directions
1. Log in to the [MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID/name or **Manage** in the **Operation** column to access the instance management page.
2. Select **Backup and Restore** > **Data Backup List**, click **Clone** on the upper left corner, or locate the desired backup and click **Clone** in the **Operation** column.
![](https://main.qcloudimg.com/raw/b53e3c4f249a5f22638c32f4c92c7f75.png)
3. On the displayed purchase page, specify the restoration mode and other configurations, and click **Buy Now**.
 - **By time point**: you can restore the clone to a point in time within the log backup retention period you set.
 - **By backup set**: you can restore the clone from the backup set of a specific physical backup within the data backup retention period you set.
 >?You can log in to the [console](https://console.cloud.tencent.com/cdb), select **Database Backup** on the left sidebar, and view backup retention period on the **Backup List** tab.
 >
![](https://main.qcloudimg.com/raw/f2fcdd5471326b60f6ee7ea8872f00bc.png)
4. After purchase, you can view the clone details on the **Backup and Restore** > **Cloned Instance List** tab.
![](https://main.qcloudimg.com/raw/3b6a2781adafd4cbde550ea00f3898a8.png)
5. After the clone process is completed, you can view the clone in the instance list.

## Documentation
- For more information about restoration of single databases and tables, please see [Database Rollback](https://intl.cloud.tencent.com/document/product/236/7276)
- For more information about how to restore data to a self-created instance, please see [Restoring Databases from Physical Backups](https://intl.cloud.tencent.com/document/product/236/31910) and [Restoring Databases from Logical Backups](https://intl.cloud.tencent.com/document/product/236/31909).
