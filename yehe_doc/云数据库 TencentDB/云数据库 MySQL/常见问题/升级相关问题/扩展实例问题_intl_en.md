### What is the difference between read-only, slave, and disaster recovery instances?
- Read-only instance: it only allows the read operation and is deployed in the same region as the master instance. A master instance can have up to 5 read-only instances.
- Slave instance: it is used to back up the database and deployed in the same region as the master instance. A master instance can have 1 or 2 slave instances.
- Disaster recovery instance: it provides cross-AZ and cross-region disaster recovery capabilities. A master instance can have up to 1 disaster recovery instance.

### Can a TencentDB for MySQL read-only instance connect to the public network?
Read-only instances can connect to both public and private networks.

### How often does a TencentDB for MySQL master instance sync data with a disaster recovery instance?
After sync is enabled and initial sync is completed, the master instance and disaster recovery instance will sync data in real time.

### Can a temporary instance be added to TencentDB for MySQL?
Currently not supported.

### Why does instance upgrade fail?
If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.

