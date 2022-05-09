## Connection Methods
You can connect to TDSQL-C for MySQL in the following ways:
- **Private network connection**: A CVM instance can be used to connect to the private network address of a TDSQL-C for MySQL instance. This method utilizes the high-speed private network of Tencent Cloud and features low delay.
 - The CVM instance and the database must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region.
 - The private network address is provided by the system by default and can be viewed in the cluster list or on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb).
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over the private network through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>
- **Public network connection**: You can connect to your TDSQL-C for MySQL cluster at its public network address. The public network address needs to be [manually enabled](#waiwang). It can be viewed on the instance details page in the [console](https://console.cloud.tencent.com/cynosdb) and can be disabled if no longer needed.
 - Enabling the public network address will expose your database services to the public network, which may lead to database intrusions or attacks. We recommend you use the private network to connect to the database. 
 - Public network access to TencentDB is suitable for development or auxiliary database management but not for actual business access, because uncontrollable factors may cause public network access to be unavailable, such as DDoS attacks and sudden surges in access traffic.
- **DMC connection**: You can access TDSQL-C for MySQL through Database Management Console (DMC).


## Connection to TDSQL-C for MySQL over Private or Public Network
### Connecting from Windows CVM instance
1. Log in to a Windows CVM instance. For more information, see [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).
2. Download a standard SQL client.
>?We recommend you download MySQL Workbench. Click [here](https://dev.mysql.com/downloads/workbench/) and download an installer based on your operating system.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. **Login**, **Sign Up**, and **No thanks, just start my download.** will appear on the page. Select **No thanks, just start my download.** to download quickly.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. Install MySQL Workbench on this CVM instance.
>?
>- Microsoft .NET Framework 4.5 and Visual C++ Redistributable for Visual Studio 2015 are required for the installation.
>- You can click **Download Prerequisites** in the MySQL Workbench installation wizard to enter the corresponding page to download and install them. Then, install MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Open MySQL Workbench, select **Database** > **Connect to Database**, enter the private (or public) network address, username, and password of your MySQL instance and click **OK** to log in.
   - **Hostname**: Enter the private (or public) network address of the target database, which can be viewed on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb). For public network address, check whether it has been enabled as instructed in [Enabling Public Network Address](#waiwang).
   - **Port**: Private (or public) network port.
   - **Username**: The default value is `root`.
   - **Password**: The password corresponding to the username. If you forgot the password, reset it in the [console](https://console.cloud.tencent.com/cynosdb).
![](https://main.qcloudimg.com/raw/9c9e5dcc8a2bb9fa15fa4d98a18308f1.png)
6. After successful login, the following page will appear, where you can view the modes and objects of the database, create tables, and perform operations such as data insertion and query.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

### Connecting from Linux CVM instance
1. Log in to the Linux CVM instance. For more information, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
2. Taking a CVM instance on CentOS 7.2 (64-bit) as an example, run the following command to install the MySQL client.
```
yum install mysql
```
If `Complete!` is displayed, the MySQL client is installed successfully.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. Perform the corresponding operation based on the connection method:
   - **Private network connection:**
    1. Run the following command to log in to the TDSQL-C for MySQL cluster.
```
mysql -h hostname -P port -u username -p
```
       - hostname: Replace it with the private network address of the target cluster, which can be viewed on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb).
       - port: Replace it with the private network port number.
    	- username: Replace it with the default username `root`.
For example, if the private network address is `10.0.168.14:5308` and the username is `root`, enter the following connection command: `mysql -h 10.0.168.14 -P 5308 -u root -p`.
    2. Enter the password corresponding to the `root` account of the cluster after `Enter password:` is prompted. If you forgot the password, reset it in the [console](https://console.cloud.tencent.com/cynosdb).
    If `MySQL [(none)]>` is displayed, you have logged in to TDSQL-C for MySQL successfully. ![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **Public network connection:**

    1. Run the following command to log in to the TDSQL-C for MySQL cluster.
```
mysql -h hostname -P port -u username -p
```
       - hostname: Replace it with the public network address of the target cluster, which can be viewed together with the port on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb). If the public network address has not been enabled, enable it as instructed in [Enabling Public Network Address](#waiwang).
       - port: Replace it with the public network port number.
       - username: Replace it with the public network connection username. We recommend you create a separate account in the console for easier connection control.
    2. Enter the password corresponding to the public network connection username after `Enter password:` is prompted. If you forgot the password, reset it in the [console](https://console.cloud.tencent.com/cynosdb).
    In this example, `hostname` is 59281c4exxx.myqcloud.com and public network port is 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Under the `MySQL [(none)]>` prompt, you can send an SQL statement to the TDSQL-C for MySQL server for execution. For specific command lines, see [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Below takes `show databases;` as an example:
![](https://qcloudimg.tencent-cloud.cn/raw/261184416556eae8a9cfa6b411541874.png)


## Connection Through DMC
1. Log in to the [console](https://console.cloud.tencent.com/cynosdb) and click **Log In** in the **Operation** column in the cluster list.
2. On the login page of DMC, enter "root" as the account and the password configured for the root account during cluster creation and click **Log In**.
>?DMC enables you to easily access instances, manipulate tables and databases, manage instance sessions, and monitor InnoDB lock waits, SQL window, etc. in real time.
>
![](https://qcloudimg.tencent-cloud.cn/raw/b81a19a203550de1ad862bab0f6c0c2f.png)

## [Appendix 1. Enabling Public Network Address](id:waiwang)
>?To connect over the public network, you need to enable the public network address of your database first.
>
1. Log in to the [console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster details page.
2. On the cluster details page, click **Enable** after the public network addresses.
![](https://qcloudimg.tencent-cloud.cn/raw/b0de7eea7ba5d07a62c9b03438904047.png)
3. In the pop-up window, click **OK**.
>?
>- Once enabled successfully, the public network address can be viewed in the connection information.
>- The public network access can be disabled by using the switch. When it is enabled again, the public IP corresponding to the domain name remains the same.
>- To access the public network, you need to enable and [configure a security group](https://intl.cloud.tencent.com/document/product/1098/44594) policy and open the default (3306) or modified private network access port.

