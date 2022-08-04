
## Overview
This document describes how to create an instance in the TencentDB for SQL Server console.

## Prerequisites
You have signed up for a Tencent Cloud account and completed identity verification as instructed in [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) and [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629) respectively.

## Directions
### Creating an instance
1. Log in to the [TencentDB for SQL Server purchase page](https://buy.intl.cloud.tencent.com/sqlserver), select the desired database configuration, read and indicate your consent to the Terms of Service, confirm that everything is correct, and click **Buy Now**.
 - Billing Mode: Pay-as-you-go billing is supported.
 - Region and AZ: For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520).
 - Network: VPC (recommended) and the classic network are supported. For more information on their differences and connectivity testing, see [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562). Both VPCs and subnets support fuzzy search.
>?
>- We recommend you place the CVM and TencentDB instances under the same account in the same VPC in the same region.
>- As the classic network resources become increasingly scarce and cannot be expanded, Tencent Cloud accounts registered after June 13, 2017 can create instances (including CVM and TencentDB) only in a VPC rather than the classic network.
 - Instance Type: Dual-Server High-Availability Edition, Cluster Edition, and Basic Edition are supported.
>?The Cluster Edition currently supports SQL Server 2017 Enterprise and SQL Server 2019 Enterprise, which use the Always On technology to build SQL Server clusters with high performance, availability, reliability, and ease of maintenance.
 - Disk Type: High-performance local SSD, high-performance cloud disk, and SSD cloud disk are supported.
>?In the Chinese mainland, if you need SSD cloud disks for your Basic Edition instances, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
<table>
<thead><tr><th>Disk Type</th><th>Description</th><th>Suitable Database Architecture</th><th>Applicable Scenario</th></tr></thead>
<tbody><tr>
<td>High-Performance local SSD</td>
<td>High-I/O local disk storage type.</td>
<td>High-Availability Edition/Cluster Edition</td>
<td>Business scenarios that have extremely high requirements for storage I/O performance and high-availability architecture at the application layer, such as online games, ecommerce, ERP software services, video live streaming, and media.</td></tr>
<tr>
<td>High-Performance cloud disk</td>
<td>Hybrid storage type. It provides high-performance storage capabilities close to SSD through the cache mechanism and adopts a three-copy distributed mechanism to ensure the data reliability.</td>
<td>Basic Edition</td>
<td>Small and medium application scenarios that require high data reliability and moderate performance, such as web/app servers, business logic processing, and small and medium websites.</td></tr>
<tr>
<td>SSD cloud disk</td>
<td>All-flash cloud disk storage type with NVMe SSD as the storage media. It adopts a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security.</td>
<td>Basic Edition</td>
<td>Application scenarios such as I/O-intensive applications and small and medium relational databases.</td></tr>
</tbody></table>
 - Database Version: The Enterprise and Standard Editions of SQL Server 2008 R2, SQL Server 2012, SQL Server 2016, SQL Server 2017, and SQL Server 2019 are supported. Each AZ supports different database versions.
 - Select an instance specification and required disk capacity.
 - Multi-AZ: Currently, only Shanghai, Beijing, Guangzhou, and Hong Kong (China) regions support selecting multi-AZ. By combining multiple AZs into a single "multi-AZ", the multi-AZ deployment mode protects databases from database instance failures and AZ outage.
 - Maintenance Window and Maintenance Time: To ensure the stability of your TencentDB for SQL Server instance, the backend system performs maintenance operations on the instance during the maintenance time from time to time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.
 - Project List: TencentDB for SQL Server supports assigning instances to different projects for management. You can fuzzy search for projects by name.
 - Security Group: It serves as a stateful virtual firewall with filtering feature for configuring network access control for one or more TencentDB instances. It is an important network security isolation tool provided by Tencent Cloud.
 - Tag: It facilitates resource categorization and management.
 - Select the quantity and length of purchase.
 - Terms of Service: For more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/238/35546).
2. After the purchase is made, return to the [instance list](https://console.cloud.tencent.com/sqlserver#/) and view the created instance. When the instance status becomes **Running**, the instance is successfully created.
![](https://main.qcloudimg.com/raw/7abd65a18810994b0c34c75450a41868.png)

### [Creating an account](id:cjzh)
1.In the [instance list](https://console.cloud.tencent.com/sqlserver), click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Account Management** > **Create Account** and enter relevant information in the pop-up window. After confirming that everything is correct, click **OK**.
>?The account name and password will be used when connecting to TencentDB for SQL Server. Store them properly.
>

### Creating a database
1.In the [instance list](https://console.cloud.tencent.com/sqlserver), click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management** > **Create Database** and enter relevant information in the pop-up window. After confirming that everything is correct, click **OK**.
 - Database Name: It can contain up to 32 letters, digits, and underscores and must start with a letter.
 - Character Set: Select the character set to be used by the database. Currently, most native character sets are supported.
 - Authorize Account: You can authorize existing accounts to access the database. If you haven't created an account yet, see [Creating an account](#cjzh).
 - Remarks: Enter remarks, which can contain up to 256 characters.
![](https://main.qcloudimg.com/raw/6bb212145f1cf97837ed7aa6be0bf05c.png)

