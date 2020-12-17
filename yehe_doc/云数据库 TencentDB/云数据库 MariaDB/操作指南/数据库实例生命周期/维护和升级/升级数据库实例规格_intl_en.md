## How Upgrade Works
After you click "Upgrade" in the console, the Tencent Cloud OPS management system will generally perform the following steps:
1. Assign a new instance (the "new instance") based on the required configuration.
2. Sync the data and configuration of the instance to be upgraded (the "old instance") to the new instance.
3. After the sync is completed, switch the route in the Tencent Cloud gateway to the new instance for continued use.
![](https://main.qcloudimg.com/raw/c6c8778c93fb4438210b5bb492a956ce.png)

## Upgrading Instance Specification
>?
>- You can still use the old instance as usual during the upgrade process, such as importing or exporting data.
>- The name, access IP, and access port of an instance will remain the same after upgrade.
>- When the upgrade is completed, the database will be disconnected for several seconds. You are recommended to implement an auto reconnection feature in your program.
>- During the upgrade process, please try to avoid operations such as modifying global parameters, instance name, or user password of the database.
>
1. Log in to the [MariaDB Console](https://console.cloud.tencent.com/mariadb). In the instance list, find the desired instance and click **More** > **Adjust Configurations** in the "Operation" column.
2. On the instance upgrade page, select the upgraded specification, disk capacity, and scheduled switch time and click **Adjust Configurations**.
>!
>- Generally, the switch time has a tolerance of about 15 minutes, as there may be high amounts of write requests to large transactions, which will affect the data sync progress. In this case, the system will first guarantee sync between the new and old instances instead of performing the scheduled switch.
>- The maximum scheduled switch time range is 72 hours. Please configure a time reasonably.
>- Please be sure to select a time during off-peak hours to avoid interrupting your business.
>


## Upgrade Fees
When you upgrade a database instance, the system will calculate the price difference between instance specifications and charge it to your account. You need to top up first if your account balance is insufficient. After the upgrade is completed, usage fees will be calculated based on the new instance specification.

