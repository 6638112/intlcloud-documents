## Operation Scenarios
TencentDB for SQL Server supports creating and deleting accounts and modifying account permissions on the **Manage Account** page in the console. Such operations cannot be performed in Microsoft SQL Server Management.
>?The created account name and password will be used when connecting to TencentDB for SQL Server. Please store them properly.
>

## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Manage Account** > **Create Account** and enter relevant information in the pop-up dialog box. After confirming that everything is correct, click **OK**.
 - 	Account Name: it is required, can contain 1–50 letters, digits, or special symbol, and must start with a letter. The special symbol is \_.
 - 	Admin: it is optional. Each TencentDB for SQL Server instance can have one admin account, which has read/write permissions to all databases by default. A newly added database will be automatically authorized for the admin account with no manual authorization required.
>?There are three types of account permissions in TencentDB for SQL Server:
>- Admin: by default, it has read/write permissions to all databases. Only one admin account can be set for one instance.
>- Read/Write: it has read/write permissions to authorized databases and can perform database changes.
>- Read-only: it has read-only permission to only authorized databases and cannot perform changes.
 - Database: it is optional. You can set the permissions (read-only or write-only) that the account has to the database when creating an account. You can also grant permissions when modifying permissions or creating databases.
 - Password: it is required and should contain 8–32 characters in at least two of the following character types: letters, digits, and special symbols (_+-&=!@#$%^*()[]).
 - Account Remarks: it is optional and can contain up to 256 characters.

3. After the account is created, you can perform operations such as **Remove Admin**, **Modify Permissions**, **Reset Password**, and **Delete Account** in the account list.

