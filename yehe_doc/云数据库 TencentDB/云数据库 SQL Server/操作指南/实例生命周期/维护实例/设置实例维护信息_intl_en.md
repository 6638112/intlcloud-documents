## Operation Scenarios
Maintenance time is a very important concept for TencentDB for SQL Server. To ensure the stability of your TencentDB for SQL Server instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. It is highly recommended that you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, it is recommended that operations involving data migration also be performed during the maintenance time, such as instance specification adjustment, instance version upgrade, and instance kernel upgrade. Currently, the maintenance period is supported by master and read-only instances.

Taking the database instance specification upgrade as an example, as this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **switch time** can be selected as **during maintenance window**, so that the instance specification switch will be enabled during the next **maintenance window** after the instance upgrade is completed. Please note that when you do so, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance window** when the switch will be performed. In this way, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for SQL Server, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.
>- Instance switch is accompanied by a momentary disconnection from the database. Please make sure that your business has a reconnection mechanism.

## Directions
### Setting maintenance time
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance details page.
2. Click **Modify** in "Maintenance Info".

3. In the pop-up dialog box, select the **Maintenance Period** and **Maintenance Time** as needed and click **OK**.


<span id="lijiqiehuan"></span>
### Performing immediate switch
If a task is configured to be switched during the maintenance window, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the "Operation" column in the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver).
>?Immediate switch is applicable to operations involving data migration such as instance specification adjustment, instance version upgrade, and instance kernel upgrade.


