TDSQL-C for MySQL supports data migration through a command line tool.

## [Data Migration with the Command Line Tool](id:AA)
1. Generate the SQL file to be imported with the MySQL command line tool `mysqldump` in the following way:
>!The data files exported by using `mysqldump` must be compatible with the SQL specification of your purchased TDSQL-C for MySQL database. You can log in to the database and get the MySQL version information by running the `select version();` command. The name of the generated SQL file can contain letters, digits, and underscores but not "test".
> 
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
Here, `options` is the export option, `db_name` is the database name, `tbl_name` is the table name, and `bak_pathname` is the export path.
For more information on how to export data with mysqldump, see [mysqldump — A Database Backup Program](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).
2. A database can be restored with the MySQL command line tool by running the following command:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Here, `hostname` is the target server for data restoration, `port` is the port of target server, `username` is the username of the database on the target server, and `bak_pathname` is the full path to the backup file.

### Migrating Data on Windows
1. Use the Windows version of mysqldump to dump the data. For more information, see the description in [Data Migration with the Command Line Tool](#AA).
>!Make sure that the same source and target database versions, mysqldump tool versions, and source and target database character sets are used. You can specify the character set using the parameter ```--default-character-set```.
2. Enter the command prompt and restore the data with the MySQL command line tool.
![](https://main.qcloudimg.com/raw/0d9caa9bbccfa840a88222fe31af980e.png)
3. Log in to the MySQL database and you can see the backed up database has already been restored to the server.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### Migrating data on Linux CVM instance
For more information on how to access a database on a CVM instance, see [Connecting to Cluster via the Console](https://www.tencentcloud.com/document/product/1098/51980).

1. Taking the `db_blog` database in TencentDB for example, log in to the CVM instance and generate the SQL file to be imported with the MySQL command line tool "mysqldump".
![](https://staticintl.cloudcachetci.com/yehe/backend-news/PFJ9829_51.png)
2. Restore the data with the MySQL command line tool. In this example, data is restored to the CVM instance. You can see that the backed up database has been imported to the database corresponding to the target CVM instance.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2PTw679_52.png)

## Issues with the Character Set of Imported Data Files
1. If no character set is specified during data file import into the database, the one configured by the database will be used.
2. Otherwise, the specified character set will be used.
3. If the specified character set is different from that of TencentDB, garbled text will be displayed.

For more information, see the character set description in <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">Use Limits</a>.
