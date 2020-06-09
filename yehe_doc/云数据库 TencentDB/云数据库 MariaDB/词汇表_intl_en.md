## B

### Backup storage

Backup storage is used to persistently store the underlying storage resources of database data and log backups.

## D

### DBA

For more information, please see [Database administrator](https://cloud.tencent.com/document/product/237/34038#32).

### Read/Write separation

Read/Write separation allows the master instance to perform transaction operations such as insertion, update, and deletion (INSERT, UPDATE, and DELETE) and the slave instance (read-only) to perform SELECT query operations.

## G

### High reliability

High reliability is often used to describe a system that is specifically designed to reduce downtime so as to maintain high availability of its services.

### Relational database

A relational database is a database that is connected and organized based on relational data structure. In a relational database model, the complex data structure is simplified into a binary relation (a two-dimensional table).
In a relational database, almost all data operations are performed on one or more relational tables. You can manage the database by sorting, joining, connecting, or selecting those related tables. Common relational databases include Oracle, MySQL, MariaDB, Microsoft SQL Server, Access, DB2, PostgreSQL, Informix, and Sybase.

## L

### Cold backup

Cold backup is a backup method used when the system is shut down or under maintenance, which means that the data backed up is exactly the same as the data in the system.

### Logical backup

Logical backup is a process during which data is extracted from a database and stored in a binary file through the SQL language. Logical backup allows you to use software technology to export data from the database and write it to an output file. The format of this file is generally different from that of files in the original database. This file is only an image of the data content in the original database. Therefore, the logical backup file can only be used for logical restoration of the database (i.e., data import) instead of physical restoration according to the original storage characteristics of the database. Logical backup is generally used for incremental backup of data changed after last backup.

## R

### Hot backup

Hot backup is a backup method used when the system is running normally. In this case, since the data in the system is updated in real time, a lag may occur between the backup data and the real data of the system.

## S

### Data replication

Data is replicated from the master to the slave in one of the following methods: strong sync replication, semi-sync replication, or async replication.

### Database store

Database store is used to persistently store underlying storage resources of database data and logs.

### Database administrator

A database administrator (DBA) is a person responsible for managing the database by using specialized software to store and organize data. The responsibilities of this role may include capacity planning, installation, configuration, database design, migration, performance monitoring, security, troubleshooting, and backup and restoration.

### Number of database connections

Number of database connections refers to the number of sessions of the client connected to the database instance.

### Database migration

As business changes, the database also needs to be migrated from one environment to another along with application businesses, such as from a local IDC to a cloud platform or from a cloud platform to another one.

### Database instance

A database instance is a standalone database environment running in the cloud as the basic data block in TencentDB, which can contain multiple databases created by database users and can be accessed using the same client tools and applications as those for a standalone database instance.

### Database engine

Database engine is the core service for storing, processing, and protecting data. It allows you to control access permissions and process transactions quickly to meet the requirements of most applications for processing massive amounts of data in corporate scenarios. Database engine is supported by each database instance.

## W

### Physical backup

Physical backup is a backup process in which the operating system files that actually make up the database are copied from one place to another (usually from a disk to a tape). Physical backup is divided into cold backup and hot backup.

## Y

### TencentDB for MariaDB

TencentDB for MariaDB is a highly secure enterprise-grade cloud database dedicated to the online transaction processing (OLTP) scenario. It has always been used in Tencent's billing business. It is compatible with MySQL syntax and has various advanced features such as thread pool, audit, and remote disaster recovery while delivering easy scalability, simplicity, and high cost performance of TencentDB.
