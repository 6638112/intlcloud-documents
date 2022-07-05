## Access Methods
TencentDB for MariaDB can be accessed in the following ways:
- **Private network access**: a CVM instance can be used to access the private network address that is automatically assigned to a TencentDB instance. Both instances should reside in the same region, be under the same account, and use the same type of networks (both in the basic network or in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535)).
- **Public network access**: on a Windows or Linux server in the public network, install a database client to access the public network address of the TencentDB for MariaDB instance.
>!
>- Currently, public network is enabled in Guangzhou, Shanghai, Beijing, Chengdu and Nanjing.
>- For public network access, the database instance's public IP needs to be enabled, which may expose your database service to attacks or intrusions on the public network. Therefore, it is recommended to log in to the database over the private network.

## Prerequisites
No matter whether you access the instance from the private or public network, you need to [create an account](https://intl.cloud.tencent.com/document/product/237/7054) first.

## Accessing a Database
### Private network access
1. Log in to the CVM instance. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Getting Started with Windows CVM</a> or <a href="https://intl.cloud.tencent.com/document/product/213/10517" target="_blank">Getting Started with Linux CVM</a>.
2. Select the connection method based on the CVM operating system.
**Login on Windows**
1) Download and install a MariaDB client. [SQLyog](https://www.webyog.com/) is recommended.
2) Open SQLyog. Enter the private IP, port number, and database account/password of the TencentDB for MariaDB instance.
 - MySQL Host Address: private IP.
 - Username: username created in the prerequisites section.
 - Password: password of the username.
 - Port: port corresponding to the private IP.

3) After successful login, the following page will appear, where you can view the modes and objects of the TencentDB for MariaDB instance, create tables, and perform **operations** such as data insertion and query.

**Login on Linux**
1) In the following example, the CVM instance runs on CentOS 7.2 64-bit. You can use Yum, the package manager built in CentOS, to download and install the MySQL client from the Tencent Cloud image source.
Install the client by running the following command:
```
sudo yum install mysql
```
The command is executed as shown below:
![](https://main.qcloudimg.com/raw/d820e34b807d84e2c25debeed4ba171e.png)
2) Log in to the TencentDB for MariaDB instance by using the MySQL command line tool.
```
mysql -h hostname -u username -p
```
Replace "hostname" with the private IP address of the target TencentDB for MariaDB instance, replace "username" with the username previously created, and enter its password when prompted with "Enter password:".
3) Under the prompt "MySQL>", you can send an SQL statement to the TencentDB for MariaDB server for execution. For specific command lines, please see [here](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Take `show databases;` for example as below:
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)

### Public network access
1. Get the public network address of the instance.
1) Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/mariadb) and click an instance name or **Manage** in the "Operation" column.
2) On the instance details page, click **Enable** after the public network address to enable it.
3) After the public network address is enabled successfully, it will be displayed.

2. Log in to the instance.
**Login on Windows**
1) Download and install a MariaDB client. [SQLyog](https://www.webyog.com/) is recommended.
2) Open SQLyog. Enter the public network domain name, port number, and database account/password of the TencentDB for MariaDB instance.
 - MySQL Host Address: public network domain name.
 - Username: username created in the prerequisites section.
 - Password: password of the username.
 - Port: port number corresponding to the public network domain name.

3) After successful login, the following page will appear, where you can view the modes and objects of the TencentDB for MariaDB instance, create tables, and perform operations such as data insertion and query.


**Login on Linux**
1) In the following example, the CVM instance runs on CentOS 7.2 64-bit. Download the MySQL client from the official website and install it with the following command:
```
sudo yum install mysql
```
2) Log in to the TencentDB for MariaDB instance by using the MySQL command line tool. The command is as follows:
```
mysql -h hostname -P port -u username -p
```
Replace "hostname" with the public network domain name of the target TencentDB for MariaDB instance, replace "username" with the username previously created, and enter its password when prompted with "Enter password:".
![](https://main.qcloudimg.com/raw/22c5ebefc86688cf30523ce2717b04e4.png)
3) Under the prompt "MySQL>", you can send an SQL statement to the TencentDB for MariaDB server for execution. For specific command lines, please see [here](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Take `show databases;` for example as below:
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


