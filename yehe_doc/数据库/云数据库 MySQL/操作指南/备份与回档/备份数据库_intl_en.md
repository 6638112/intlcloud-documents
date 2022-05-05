To avoid data loss or corruption, you can back up a database automatically or manually.

## Backup Overview
### Backup modes
Two-node and three-node TencentDB for MySQL instances support **automatic backup** and **manual backup** of databases.

### Backup types
Two-node and three-node TencentDB for MySQL instances support two backup types:
- **Physical backup**, which is a full copy of physical data (supported for both automatic backup and manual backup).
- **Logical backup**, which backs up SQL statements (only supported for manual backup).
>?
>- To restore a database from a physical backup, you need to use xbstream to decompress the package first. For more information, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).
>- If the number of tables in a single instance exceeds one million, backup may fail, and database monitoring may be affected. You need to control the number of tables in one single instance appropriately and make sure that it is below one million.
>- As the data of tables created by the MEMORY storage engine is stored in the memory, physical backups cannot be created for such tables. To avoid data loss, we recommend you replace them with InnoDB tables.
>- If there are a high number of tables without a primary key in the instance, backup may fail, and the high availability of the instance may be affected. You need to create a primary key or secondary index for such tables in time.

| Physical Backup Advantages | Logical Backup Disadvantages |
|---------|---------|
| <li>High backup speed. <li>Streaming backup and compression are supported. <li>High success rate. <li>Simple and efficient restoration. <li>Faster backup-based coupling operations such as adding real-only replicas and disaster recovery instances. <li>1/8 of average time needed for creating a logical backup. <li>Ten times faster than logical backups during import. | <li>Long time needed to restore as it takes time to run SQL statements and build indexes. <li>Low backup speed, especially when there are massive amounts of data. <li>Possible increase in source-replica delay due to the pressure on instances during backup. <li>Possible loss of precision information of floating points. <li>Potential backup failures due to wrong views and other problems. <li>Slower backup-based coupling operations such as adding read-only replicas and disaster recovery instances.</li> |

### Backup objects
| Data Backup | Log Backup |
|---------|---------|
| Two-node and three-node TencentDB for MySQL: <li>Automatic backup supports full physical backup. <li>Manual backup supports full physical backup, full logical backup, and single-database/table logical backup. <li>Both automatic and manual backups can be compressed and downloaded. | Two-node and three-node TencentDB for MySQL support binlog backup: <li>Log files occupy the instance's backup space. <li>Log files can be downloaded but cannot be compressed. <li>Retention periods can be set for log files.</li>|

## Notes
- Starting from February 26, 2019, the automatic backup feature of TencentDB for MySQL will only support physical backup (default type) and no longer provide logical backup. Existing automatic logical backups will be switched to physical backups automatically.
This will not affect your business access, but may have impact on your habit of automatic backup. If you need logical backups, you can use the manual backup option in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) or [call the relevant API](https://intl.cloud.tencent.com/document/product/236/15844) to generate logical backups.
- Instance backup files occupy backup space. We recommend that you plan the usage of backup space appropriately. Usage of backup space that exceeds the free tier will incur fees. For more information, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
- We recommend you back up your database during off-peak hours.
- To avoid situations where the required backup files are deleted after the retention period lapses, you need to download them to the local file system in a timely manner.
- DDL operations are prohibited during the backup process so as to avoid backup failure due to table locking.
- Single-node TencentDB for MySQL instances cannot be backed up.

## Backing up MySQL Data Automatically
### Configuring automatic backup
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID on the instance list page to enter the management page, and select **Backup and Restoration** > **Auto-Backup Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/da6aad42478cbbddba52d02b1d677238.png)
2. Select backup parameters in the pop-up window as detailed below and click **OK**:
>?
> - The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed.
> For example, if the backup cycle is set as Monday and Thursday and the retention period is set as seven days, you can roll a database back to any point of time in the past seven days (which is the actual retention days of data backups and log backups).
> - Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire.
> - Increasing the retention period of data and log backups may cause additional backup space fees.
> - Shortening the retention period of log backups may affect the data rollback cycle of the instance.

In the auto-backup settings, you can enable the archive backup policy. The following describes the parameters for archive backup and non-archive backup.
>!Archive backup retention period can only be longer than non-archive backup retention period.
>

### Non-archive backup settings
| Parameter | Description |
|---------|---------|
| Backup Start Time | <li>The default backup start time is automatically assigned by the system. <li>You can set a start time as needed. We recommend that you set it to off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the backup start time is set to 02:00-06:00, the system will initiate a backup at a point in time during 02:00-06:00, which depends on the backend backup policy and backup system conditions.</br> |
| Data Backup Retention Period | Data backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |
| Backup Cycle | To ensure data security, back up your data at least twice a week. All seven days of the week will be selected by default. |
| Log Backup Retention Period | Log backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |

![](https://qcloudimg.tencent-cloud.cn/raw/9c018f548a012b427daf0227f2a93642.png)

### Archive backup settings
| Parameter | Description |
|---------|---------|
| Backup Start Time | <li>The default backup start time is automatically assigned by the system. <li>You can set a start time as needed. We recommend that you set it to off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the backup start time is set to 02:00-06:00, the system will initiate a backup at a point in time during 02:00-06:00, which depends on the backend backup policy and backup system conditions.</br> |
| Data Backup Retention Period | Data backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |
| Backup Cycle | To ensure data security, back up your data at least twice a week. All seven days of the week will be selected by default. |
| Archive Backup Retention Period | Data backup files can be retained for 90 to 3,650 days (1,080 days by default) and will be automatically deleted upon expiration. |
| Archive Backup Retention Policy | You can set the number of backups by month, quarter, or year. |
| Start Time | The time to start archive backup. |
| Log Backup Retention Period | Log backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |

![](https://qcloudimg.tencent-cloud.cn/raw/78c89e11aa7acab08de33b2f609fc56e.png)

### Viewing retention plan
After you select an archive backup retention policy in the backup settings, you can click **View Retention Plan** to preview it.
![](https://qcloudimg.tencent-cloud.cn/raw/9b7c21feff9bf1409c80f745fbf1d370.png)
- Blue dates are for non-archive backups.
- Red dates are for archive backups.
- You can click **Non-archive Backup** or **Archive Backup** to hide corresponding dates for easier preview.
- The backup plan preview is currently for backups for the year to come and is for reference only.

Example 1: The backup cycle is Monday, Wednesday, Friday, and Sunday, with one backup retained for each month starting from January 11, 2022.
![](https://qcloudimg.tencent-cloud.cn/raw/9815814482b467916689b36d7f7b523b.png)
Example 2: The backup cycle is Monday, Wednesday, and Friday, with three backups retained for each quarter starting from January 11, 2022.
![](https://qcloudimg.tencent-cloud.cn/raw/9815814482b467916689b36d7f7b523b.png)
Example 3: Show only archive backups.
![](https://qcloudimg.tencent-cloud.cn/raw/ec59982c8f84ae59e652f5efdfb65996.png)


## [Backing up MySQL Data Manually](id:manual-backup)
The manual backup feature allows you to initiate a backup task manually.
>?
>- Manual backup supports full physical backup, full logical backup, and single-database/table logical backup.
>- Manual backups can be manually deleted from the backup list in the console. You can delete manual backups that are no longer in use to free up space. Manual backups can be retained as long as they are not deleted until the database instance is deactivated.
>- When the instance is performing daily automatic backup, you cannot initiate a manual backup task.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID on the instance list page to enter the management page, and select **Backup and Restoration** > **Manual Backup**.
2. Select backup modes and objects in the pop-up window, enter an alias, and click **OK**.
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>?For single-database/table logical backup, select the database or table to be backed up in **Select databases and tables** in the left column and add the selected item to the right column. If you don't have a database, create a database/table first.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)

## FAQs
#### 1. Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- You are recommended to configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
- You can also manually back up the instance data in the console, and manual backup files will be retained permanently.
>?Manual backups will also take up the backup space. We recommend that you plan the usage of the backup space appropriately to reduce costs.

#### 2. Can I delete backups manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire. 
- Manual backups can be manually deleted from the backup list in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). Manual backups can be retained permanently as long as they are not deleted.

#### 3. Can I disable data and log backups?
No. However, you can lower the backup frequency and delete manual backup data that is no longer used in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to reduce the backup space.

#### 4. How can I reduce the backup space costs?
- Delete manual backups that are no longer used (you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID/name to access the instance's management page, and delete manual backups on the **Backup and Restoration** tab). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback time range for instance data. You need to configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | Seven days |
| Archive businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
