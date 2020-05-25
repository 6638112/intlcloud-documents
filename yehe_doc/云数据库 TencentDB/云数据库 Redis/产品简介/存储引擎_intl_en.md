## Memory Edition Engine
The Memory Edition engine provides a native Redis experience and supports a myriad of scenarios. It supports both Redis standard and cluster deployment architectures to meet the requirements of different business scenarios.

Editions supported by the Memory Edition engine include:
 - Memory Edition (standard architecture): when the number of replicas is greater than 0, data is synced between the master node and the replica nodes (slaves) in real time. When the master node fails, automatic failover will be performed in a matter of seconds, and a replica node will take over the business in an imperceptible manner. The master/slave architecture guarantees high availability of system services and provides 0.25–60 GB of storage capacity.
 - [Memory Edition (cluster architecture)](https://intl.cloud.tencent.com/document/product/239/18336): a cluster instance uses a distributed architecture, which allows flexible selection of shard quantity, shard capacity, and replica quantity and enables scaling imperceptible to the business. It provides 6 GB–4 TB of storage capacity and a performance of tens of millions of QPS.

## Hybrid Storage Edition Engine 
Tendis, the Hybrid Storage Edition engine, is Tencent's proprietary RocksDB storage engine compatible with the Redis protocol. It features high performance, compression ratio, and stability and has been widely used in Tencent's various businesses.

Editions supported by the Hybrid Storage Edition engine include:
- [Hybrid Storage Edition (cluster architecture)](https://intl.cloud.tencent.com/document/product/239/36163): it is compatible with the version commands of Redis Cluster Edition v4.0 and provides 240 GB–32 TB of storage capacity. It supports 6 replicas of disk data to fully guarantee data reliability.
