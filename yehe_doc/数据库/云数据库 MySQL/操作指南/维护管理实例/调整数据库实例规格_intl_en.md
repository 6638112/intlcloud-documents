TencentDB for MySQL supports quick adjustment of instance specification and allows flexible scaling operations in the console. You can elastically adjust the specifications of MySQL instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization. For details on instance adjustment fees, see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).

## Instance Disk Space Description
- To ensure the normal operation of your business, upgrade database instance specification or purchase more disk storage in time when your disk is going to run out of space.
>?You can view disk space on the instance details page in the [MySQL console](https://console.cloud.tencent.com/cdb), or receive disk alarms by configuring alarms as instructed in [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
- When the data size stored on the instance exceeds capacity limit, the instance is locked and only allows reading data (writing data is not allowed). You need to expand the capacity or delete some of the database tables on console to remove the read-only status.
- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity is more than 20% of its total capacity or over 50 GB.

## Configuration Adjustment Description
By default, the instance configuration is adjusted in the normal mode, which requires a data migration for the adjustment to complete after you adjust the instance configuration in the console. But if the physical machine where the instance is located has sufficient remaining resources (i.e., local resources), you can choose the QuickChange mode. The adjustment process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/8e7702c81886573a459dbf73b2846701.png)

- **Normal mode**: To adjust the instance configuration, instance data needs to be migrated from the original physical machine to a new one. Because adjustment in this mode requires data migration, comparison, and verification, the overall adjustment process will take a long time in case of a huge amount of data. Besides, an instance switch may occur after the adjustment is completed.
- **QuickChange mode**: The instance configuration can be adjusted without migrating data or switching to another physical machine. As no migration preparation is needed, the overall adjustment process is much shorter.
>!
>- If the local resources are sufficient and meet the conditions of the QuickChange mode, this mode will be used by default. If you don't need to use it, you can disable it by toggling it off on the configuration adjustment page.

## Notes
- A read-only instance with an exclusive VIP enabled does not support QuickChange.
- If a read-only instance group (read-only group) enables the "Remove Delayed RO Instances" feature, read-only instances with a delay exceeding the specified threshold will be removed from the read-only group until the number of remaining ones reaches the allowed minimum number. If the number of the remaining available read-only instances in a read-only group is less than or equal to the allowed minimum number, none of those instances will support QuickChange.
- If a read-only group only has one read-only instance, the instance does not support QuickChange.
- If the kernel minor version of the instance is not the latest when the configuration is adjusted, it will be upgraded to the latest. In this case, enabling the QuickChange mode may cause the instance to restart, as prompted on the **QuickChange** page.

## [Configuration Adjustment Rules](id:guize)
- You can adjust the configuration of a TencentDB for MySQL instance and its associated read-only and disaster recovery instances only when they are in normal status (running) and are not executing any task.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- During configuration adjustment, you should avoid such operations as modifying MySQL's global parameters and user password.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). We recommend you use applications configured with automatic reconnection feature and conduct the switch during the instance maintenance time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend you adjust instance configuration during off-peak hours.

## Instance Specification and Storage Table
### Two-node/Three-node (local SSD disk)
<table class="table-striped">
<tbody>
<tr><th>Isolation Policy</th><th>CPU and Memory</th><th>Maximum IOPS</th><th>Storage Space</th></tr>
<tr>
<td rowspan="14">General</td>
<td>1-core 1000 MB</td><td>1200</td><td rowspan="10">25–3000 GB</td></tr>	
<tr>
<td>1-core 2000 MB</td><td>2000</td></tr>
<tr>
<td>2-core 4000 MB</td><td>4000</td></tr>
<tr>
<td>4-core 8000 MB</td><td>8000</td></tr>
<tr>
<td>4-core 16000 MB</td><td>14000</td></tr>
<tr>
<td>8-core 16000 MB</td><td>20000</td></tr>
<tr>
<td>8-core 32000 MB</td><td>28000</td></tr>
<tr>
<td>16-core 32000 MB</td><td>32000</td></tr>
<tr>
<td>16-core 64000 MB</td><td>40000</td></tr>
<tr>
<td>16-core 96000 MB</td><td>40000</td></tr>
<tr>
<td>16-core 128000 MB</td><td>40000</td><td rowspan="4">25–6000GB</td></tr>
<tr>
<td>24-core 244000 MB</td><td>60000</td></tr>
<tr>
<td>32-core 256000 MB</td><td>80000</td></tr>
<tr>
<td>48-core 488000 MB</td><td>120000</td></tr>
<tr>
<td rowspan="26">Dedicated</td>
<td>2-core 16000 MB</td><td>8000</td><td rowspan="7">25–3000 GB</td></tr>	
<tr>
<td>4-core 16000 MB</td><td>10000</td></tr>
<tr>
<td>4-core 24000 MB</td><td>13000</td></tr>
<tr>
<td>4-core 32000 MB</td><td>16000</td></tr>
<tr>
<td>8-core 32000 MB</td><td>32000</td></tr>
<tr>
<td>8-core 48000 MB</td><td>36000</td></tr>
<tr>
<td>8-core 64000 MB</td><td>40000</td></tr>
<tr>
<td>12-core 48000 MB</td><td>36000</td><td rowspan="15">25–6000 GB</td></tr>
<tr>
<td>16-core 64000 MB</td><td>60000</td></tr>
<tr>
<td>12-core 72000 MB</td><td>40000</td></tr>
<tr>
<td>12-core 96000 MB</td><td>48000</td></tr>
<tr>
<td>16-core 96000 MB</td><td>60000</td></tr>
<tr>
<td>24-core 96000 MB</td><td>72000</td></tr>
<tr>
<td>16-core 128000 MB</td><td>60000</td></tr>
<tr>
<td>32-core 128000 MB</td><td>80000</td></tr>
<tr>
<td>24-core 144000 MB</td><td>76000</td></tr>
<tr>
<td>24-core 192000 MB</td><td>80000</td></tr>
<tr>
<td>32-core 192000 MB</td><td>90000</td></tr>
<tr>
<td>48-core 192000 MB</td><td>120000</td></tr>
<tr>
<td>32-core 256000 MB</td><td>100000</td></tr>
<tr>
<td>48-core 288000 MB</td><td>140000</td></tr>
<tr>
<td>48-core 384000 MB</td><td>140000</td></tr>
<tr>
<td>64-core 256000 MB</td><td>150000</td><td rowspan="2">25–9000 GB</td></tr>
<tr>
<td>64-core 384000 MB</td><td>150000</td></tr>
<tr>
<td>64-core 512000 MB</td><td>150000</td><td rowspan="2">25–12000 GB</td></tr>
<tr>
<td>90-core 720000 MB</td><td>150000</td></tr>
</tbody></table>	

## Adjusting the Instance Configuration in the Console
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), locate the target instance in the instance list, and select **More** > **Adjust Configurations** in the **Operation** column.
2. In the pop-up window, select the target configuration and click **Submit**.
>?
>- When the local resources are sufficient, you can enable the QuickChange mode by turning on the **QuickChange** toggle on the configuration adjustment page in the console.
>![](https://main.qcloudimg.com/raw/c37bb99f0a2db0a9108c7068ad72ba7c.png)
>- In some cases, instance restart is not required in the QuickChange mode and the configuration adjustment will take effect immediately after you submit the request, as shown below:
![](https://main.qcloudimg.com/raw/6f5e9ab54f270c0833f5545cccbc8c6d.png)
>
![](https://main.qcloudimg.com/raw/ef2bf519dabe88cb23b9c73993602b9b.png)

## Adjusting the Instance Configuration Through an API
You can adjust the instance configuration using the `UpgradeDBInstance` API. For more information, see [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).

## FAQs
#### Will instance configuration adjustment affect instances?
- In the process of TencentDB for MySQL configuration adjustment, data migration may occur, and instances can still be accessed during the process. After the migration is completed, there is a switch which causes a short disconnection lasting for just seconds, ensure that your business has a reconnection mechanism.
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend you adjust instance configuration during off-peak hours.

#### Why can't my instance be downgraded?
It may be because the used storage capacity has reached the maximum capacity of the hard disk. To downgrade your instance, you need to clean up data first and make sure the remaining available capacity accounts for more than 20% of the total capacity or over 50 GB.

#### Why is my instance in the "Waiting for switch" status for a long time after I adjust instance configuration in the console?
It may be because you select **During maintenance time** as the **Switch Time** when you adjust instance configuration in the [console](https://console.cloud.tencent.com/cdb), so the instance will not be switched immediately after the adjustment.
To switch immediately, you can locate the target instance in the instance list and click **Switch Now** in the **Operation** column. The switch causes a short disconnection lasting for just seconds. Ensure that your business has a reconnection mechanism.

#### How long does it take to upgrade instance configuration?
The time it takes depends on the instance's data volume and data replication speed.
Instances can still be accessed during the upgrade, but a VIP switch causes a short disconnection lasting for just seconds after the upgrade completes.

#### How do I view the progress of instance configuration adjustment?
You can view the progress in [Task List](https://console.cloud.tencent.com/mysql/task) in the console.

#### What should I do if the disk space is being used up?
If over 85% disk space is used, we recommend you delete data no longer used or expand disk space in the [console](https://console.cloud.tencent.com/cdb) by selecting **More** > **Adjust Configurations** in the **Operation** column on the right of the instance list.

#### How do I know whether the QuickChange mode is supported when I adjust instance memory or disk capacity?
On the configuration adjustment page, if the QuickChange mode is supported, the **QuickChange** toggle can be turned on or off as needed; otherwise, the toggle cannot be used.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Does expanding memory or disk capacity affect the kernel minor version of the instance?
If the kernel minor version of the instance is not the latest when memory or disk capacity is expanded, it will be upgraded to the latest. In this case, enabling the QuickChange mode will cause the database restart.

#### Will enabling the QuickChange mode cause the instance to restart?
The instance needs to be restarted in some cases. A prompt whether to restart the instance will be displayed on the configuration adjustment page as shown below:
![](https://main.qcloudimg.com/raw/d97d2daa7cb8e5aa0924355c59bc4fc8.png)

>?If the kernel minor version of the instance is the latest, adjusting only the disk capacity in the QuickChange mode will not cause the instance to restart.

#### How do I know whether the QuickChange mode is enabled when I upgrade instance configuration in the console?
You can check the **QuickChange** switch on the configuration adjustment page: if the switch is toggled on, the QuickChange mode is enabled; otherwise, the mode is disabled.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### How do I know whether the QuickChange mode is enabled when I use APIs to adjust instance configuration?
APIs do not support QuickChange for the time being, so instance configuration can be adjusted only by migrating data if you use APIs. APIs will support QuickChange in the future.

#### Will database parameters be modified during database configuration adjustment?
The `innodb_buffer_pool_size` parameter will be modified according to the configuration changes.

#### Will database parameters be modified during database configuration adjustment in the QuickChange mode?
It is the same as the normal mode. In the QuickChange mode, some parameters will be modified in response to the configuration changes.

#### What is the difference between QuickChange mode and normal mode?
The QuickChange mode requires no data migration, so it takes less time to adjust instance configuration.

