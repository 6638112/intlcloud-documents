## Strong Data Consistency
Strong sync replication can be configured. In the primary/replica architecture, strong sync can ensure primary/replica data consistency to avoid data loss in case of primary/replica switchover. Of course, you can modify the configuration to disable strong sync to improve database performance.

## High Security
- Anti-DDoS attacks: When you use the internet to connect to and access a TencentDB for MariaDB instance, you may suffer from DDoS attacks. When the TencentDB for MariaDB security system considers that your instance is under attacks, it will automatically enable traffic cleansing.
- System security: Even in the private network, TencentDB for MariaDB is under protection by multiple layers of firewalls in order to effectively fight against various attacks and protect data security. In addition, physical servers do not allow direct login and only open ports required by specific database services to isolate risky operations.
- VPC isolation: VPCs are supported to securely isolate access requests from other devices in the private network.
- Private network risk management: The TencentDB team cannot directly access TencentDB for MariaDB physical machines or instances; instead, they must access them through the Tencent Cloud Ops management platform. Even troubleshooting has to be performed on secure devices and strictly controlled by the internal risk management system.
- Object-level permission control: TencentDB for MariaDB allows you to define table-level permissions and configure IP addresses that can access TencentDB for MariaDB instances. Access from other IP addresses will be denied.
- Database audit: Database audit can be configured. Operations of admins or users are recorded for subsequent risk management.
- Operation logs: The system records all users' operations on TencentDB for MariaDB instances through the Tencent Cloud console for future traceability.

## High Availability
TencentDB for MariaDB is designed to achieve an availability of over 99.99%. It provides primary/replica hot backup or two replicas for one primary (where the two replicas are used to implement imperceptible failover). In addition, it has features such as automatic recovery of faulty nodes, automatic backup, and rollback to facilitate smoother and securer business operations.

#### High physical availability
Based on the configuration of your purchased instances, TencentDB for MariaDB usually adopts the architecture of two nodes (one primary and one replica) or three nodes (one primary and two replicas). Each node is installed on an independent physical machine deployed across racks to ensure that database service will not be affected by network or power failure of a single device or rack.

#### High network availability
The physical machine of each TencentDB for MariaDB node adopts the dual-ENI dual-connection switch configuration to ensure security and reliability of the physical network. In actual use, TProxy connects to TGW; when the primary node fails, TProxy can switch database routes within 200 ms at best; if TProxy fails, TGW can schedule the loads to another healthy TProxy within one second; and the switching does not change the access VIP (virtual IP) so as to eliminate the impact caused by change of physical servers.

#### Backup and restoration services
**Backup service**: The backup module is responsible for periodically creating (physical) backups and storing binary files (binlogs) of TencentDB for MariaDB. Backup files will be uploaded to a distributed file cluster (HDFS) with a higher level of security. Generally, backup is initiated on replica nodes to avoid impact on services provided by the primary node.
**Restoration service**: It is also known as rollback, where the restoration module restores backup files in HDFS to the temp instance for you to check or adjust without affecting operations of the primary instance.
**Backup download**: You can transfer or download backup files to a specified location, e.g., lower-priced COS.

#### 2-region-3-DC
2-region-3-DC deployment architecture of TencentDB for MariaDB: The straight-line distance between nodes in the same city is greater than 10 KM, and that between nodes in different cities is greater than 100 KM. This architecture can be implemented by Tencent's proprietary high availability (HA) scheduling scheme as shown below:
![](https://main.qcloudimg.com/raw/911a8b1f890e9160ab46ad0d046abcb5.png)

## High Performance
Based on PCI-E SSD, TencentDB for MariaDB has powerful I/O performance that guarantees the accessibility of database. The storage firmware adopts the NVMe protocol and is specifically designed for PCI-E SSD, bringing TencentDB for MariaDB's superior performance to full play with one single high-IO instance sustaining up to 6 TB storage, 480 GB memory, and at least 220,000 queries per second (QPS). The performance advantage allows you to support higher business concurrence with a smaller number of database instances.

TencentDB for MariaDB instances doesn’t use native kernels directly. Instead, it keeps optimizing the kernels in real-word scenarios, with default parameters fine-tuned over Tencent Cloud's many years of production practices and continuously improved by professional DBAs. In this way, it can always run based on the best practices.

## Powerful Features
- Multi-source replication is supported, which well sustains complex enterprise-level businesses such as frontend, middleend, backend, and data warehouse in the insurance sector.
- Higher-level storage engines such as XtraDB and TokuDB are supported, and technologies such as "group commit for the binary log" are introduced to effectively improve business performance and decrease storage usage.
- Features such as thread pool and audit logs are supported.
- The clock is accurate down to the microsecond, making it ideal for financial transaction businesses that require higher time accuracy.
- Virtual columns (function indices) are provided to improve database analysis, statistics collection, and computing performance.

## High Compatibility with MySQL 
TencentDB for MariaDB uses the InnoDB storage engine and is highly compatible with MySQL 5.5/5.6, which means that code, applications, drivers, and tools that apply to MySQL databases can be directly used in TencentDB for MariaDB with no or only slight change required.

## Cost Effectiveness and Ease of Use
- Out-of-the-box usage: You can customize TencentDB for MariaDB specifications at Tencent Cloud's official website. Once an order is placed, a TencentDB for MariaDB instance will be generated automatically. You can use it with CVM to reduce internet traffic fees and application response time.
- On-demand upgrade: At the initial stage of your business, you can purchase low-specced TencentDB for MariaDB instances to cope with business pressure. As database pressure increases and data volume changes, you have the flexibility to adjust instance specifications.
- Easy management: Tencent Cloud is responsible for routine maintenance and management of TencentDB for MariaDB instances, including without limitation software and hardware troubleshooting and database patch update, to ensure normal operations of the instances. You can also perform management operations in the Tencent Cloud console on your own, such as adding, dropping, restarting, backing up, and restoring databases.

