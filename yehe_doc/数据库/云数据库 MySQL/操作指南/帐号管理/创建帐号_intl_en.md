
## Overview
Besides the default root account created by the system, you can create other business accounts in the TencentDB for MySQL console based on your actual business needs.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select **Database Management**> **Account Management** and click **Create Account**.
![](https://qcloudimg.tencent-cloud.cn/raw/76068498b5b5161fcfed90abf39274f3.png)
3. In the pop-up window, enter the account name, host, password, and confirm password and click **OK**.
 - **Account Name**:
    - The account name in MySQL 5.5 and 5.6 can contain 1–16 letters, digits, and underscores (_) and must begin with a letter and end with a letter or digit.
    - The account name in MySQL 5.7 and 8.0 can contain 1–32 letters, digits, and underscores (_) and must begin with a letter and end with a letter or digit.
 - **Host**: the host address for database access can be an IP and contain `%` (indicating not to limit the IP range). Multiple hosts should be separated by line breaks, spaces, semicolons, commas, or vertical bars.
    - Example 1: enter `%` to indicate not to limit the IP range, that is, clients at all IP addresses are allowed to use this account to access the database.
    - Example 2: enter `10.5.10.%`, which means that clients whose IP range is within `10.5.10.%` are allowed to use this account to access the database.
 - **Password**: the password must contain 8–64 characters in at least two of the following character types: letters, digits, and special symbols `\_+-&amp;=!@#$%^\*()`.
 - **Maximum Connections**: the number of connections for this account, which must be no more than 10,240. If you don't enter a value, no limit will be imposed (subject to the maximum number of connections).
4. After successful creation, the database account can be managed in the database account list of the current instance.

## Related APIs

| API Name                                                      | Description     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](https://intl.cloud.tencent.com/document/product/236/17502) | Creates TencentDB account |


