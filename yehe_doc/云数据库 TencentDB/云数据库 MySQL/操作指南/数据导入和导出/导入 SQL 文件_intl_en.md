## Operation Scenarios
TencentDB for MySQL supports importing SQL files via the console, allowing you to execute SQL statements in the selected database. You can also use this feature to create databases/tables and change table structures to initialize or modify the instance.
>?High-availability edition and finance edition of TencentDB for MySQL instances support importing SQL files.
## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Database List** and click **Data Importing**.
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
3. On the pop-up page, click **Add File** to import the file. After the upload is completed, click **Next**.
>
>- To avoid database unavailability caused by corruption of system tables, do not import data from system tables such as the `mysql.user` table. 
>- Only incremental import is supported. If there is obsolete data in the database, clear the data before the importing operation.
>- A single file does not exceed 2 GB. The file name only allows letters, numbers, and underlines.
>- Uploaded files are valid for 14 days and will be automatically deleted after expiration.
>
<img src="https://main.qcloudimg.com/raw/fd6c70707a8722ca64a87f71978e2a2a.png">
4. On the database selection page, select the target database and click **Next**.
5. On the confirmation page, after confirming that the imported data is correct, enter the account and password and click **Import**.
>
>- The import cannot be rolled back. Please confirm the import information.
>- If you forgot the password, please reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
>

![](https://main.qcloudimg.com/raw/e21ccbe6c1f0a95cd46b4387fea1fab1.png)

