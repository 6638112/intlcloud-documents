## Feature overview
Cluster events include event lists and event policies.
- Event list: It records key change events and abnormal events occurring in the cluster.
- Event policy: Event monitoring trigger policies can be customized based on the actual business conditions. Events with monitoring enabled can be set as cluster inspection items.

## Viewing the event list
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event List** to view all operation events in the current cluster.
![](https://main.qcloudimg.com/raw/5060d9a929e662b5b14c8fa78f3b6843.png)
The severity divides into the following:
 - Fatal: Exception events of a node or service that require manual intervention and will cause service interruption if left unattended. Such events may last for a period of time.
 - Severe: Alert events that currently have not caused service or node interruption but will cause fatal events if left unattended.
 - Moderate: Regular events occurring in the cluster that generally do not require special processing.

3. Click the value in the **Triggers today** column to view the event's trigger records, metrics, logs, and snapshots.
![](https://qcloudimg.tencent-cloud.cn/raw/d184a9581e1c72055b921964df069ec8.png)

## Setting an event policy
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event Policy** and you can customize the event monitoring trigger policies.
3. The event configuration list contains the event name, event trigger policy, severity (fatal, severe, and moderate), and option to enable/disable monitoring, which can be modified and saved.
![](https://main.qcloudimg.com/raw/7107d9b985db81e2b8fdbf921bf567c1.png)
4. Event trigger policies cover two types of events: fixed system policy events (which cannot be modified) and custom events (which can be configured based on the business standards).
![](https://qcloudimg.tencent-cloud.cn/raw/5fc474a988b252d0cf25f41cec7e7864.png)
5. You can select whether to enable event monitoring in an event policy. Only events with monitoring enabled can be selected as cluster inspection items. Monitoring is enabled by default for some events and is enabled by default and cannot be disabled for some other events. The following are the specific rules:
<table>
<thead>
<tr>
<th ><strong>Type</strong></th>
<th><strong>Event</strong></th>
<th><strong>Description</strong></th>
<th><strong>Recommended Measure</strong></th>
<th><strong>Default Value</strong></th>
<th><strong>Severity</strong></th>
<th><strong>Disableable</strong></th>
<th><strong>Enabled by Default</strong></th>
</tr>
</thead>
<tbody><tr>
<td rowspan="23"><strong>Node</strong></td>
<td>The CPU utilization exceeds the threshold continuously</td>
<td>The server CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average CPU utilization exceeds the threshold</td>
<td>The average server CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average CPU iowait utilization exceeds the threshold</td>
<td>The average CPU iowait utilization of the server in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=60, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The 1-second CPU load exceeds the threshold continuously</td>
<td>The 1-minute CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=8, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The 5-second CPU load exceeds the threshold continuously</td>
<td>The 5-minute CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=8, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The memory utilization exceeds the threshold continuously</td>
<td>The memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The swap space exceeds the threshold continuously</td>
<td>The server swap memory has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.1, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The total number of system processes exceeds the threshold continuously</td>
<td>The total number of system processes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=10000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average total number of fork subprocesses exceeds the threshold</td>
<td>The average total number of fork subprocesses in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=5000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The process does not exist due to OOM</td>
<td>An OOM error occurred in the process</td>
<td>Adjust the process heap memory size</td>
<td>-</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>A disk I/O error occurred (this event is not supported currently)</td>
<td>A disk I/O error occurred</td>
<td>Replace the disk</td>
<td>-</td>
<td>Fatal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average disk space utilization exceeds the threshold continuously</td>
<td>The average disk space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average disk I/O device utilization exceeds the threshold continuously</td>
<td>The average disk I/O device utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node file handle utilization exceeds the threshold continuously</td>
<td>The node file handle utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of TCP connections to the node exceeds the threshold continuously</td>
<td>The number of TCP connections to the node has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check whether there are connection leaks</td>
<td>m=10000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The configured node memory utilization exceeds the threshold</td>
<td>The memory utilization configured for all roles on the node exceeds the node's physical memory threshold</td>
<td>Adjust the allocated node process heap memory</td>
<td>90%</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The node process is unavailable</td>
<td>The node service process is unavailable</td>
<td>View the service logs to find out why the service failed to be pulled</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node heartbeat is missing</td>
<td>The node heartbeat failed to be reported regularly</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Fatal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>Incorrect hostname</td>
<td>The node's hostname is incorrect</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Fatal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>Failed to ping the metadatabase</td>
<td>The TencentDB instance heartbeat failed to be reported regularly</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>The single disk space utilization exceeds the threshold continuously</td>
<td>The single disk space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The single disk I/O device utilization exceeds the threshold continuously</td>
<td>The single disk I/O device utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The single disk inodes utilization exceeds the threshold continuously</td>
<td>	The single disk inodes utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="17"><strong>HDFS</strong></td>
<td>The total number of HDFS files exceeds the threshold continuously</td>
<td>The total number of files in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Increase the NameNode memory</td>
<td>m=50,000,000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average total number of HDFS files exceeds the threshold</td>
<td>The average total number of files in the cluster in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Increase the NameNode memory</td>
<td>m=50,000,000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The total number of HDFS blocks exceeds the threshold continuously</td>
<td>The total number of blocks in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Increase the NameNode memory or the block size</td>
<td>m=50,000,000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average total number of HDFS blocks exceeds the threshold</td>
<td>The average total number of HDFS blocks in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Increase the NameNode memory or the block size</td>
<td>m=50,000,000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of HDFS data nodes marked as dead exceeds the threshold continuously</td>
<td>The number of data nodes marked as dead has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The HDFS storage space utilization exceeds the threshold continuously</td>
<td>The HDFS storage space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Clear files in HDFS or expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average HDFS storage space utilization exceeds the threshold</td>
<td>The average HDFS storage space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Clear files in HDFS or expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Active/Standby NameNodes were switched</td>
<td>Active/Standby NameNodes were switched</td>
<td>Locate the cause of NameNode switch</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The NameNode RPC request processing latency exceeds the threshold continuously</td>
<td>The RPC request processing latency has been greater than or equal to m milliseconds for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=300, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current NameNode connections exceeds the threshold continuously</td>
<td>The number of current NameNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred on a NameNode</td>
<td>A full GC event occurred on a NameNode</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The NameNode JVM memory utilization exceeds the threshold continuously</td>
<td>The NameNode JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NameNode heap memory size</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The DataNode RPC request processing latency exceeds the threshold continuously</td>
<td>The RPC request processing latency has been greater than or equal to m milliseconds for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=300, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current DataNode connections exceeds the threshold continuously</td>
<td>The number of current DataNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred on a DataNode</td>
<td>A full GC event occurred on a NameNode</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The DataNode JVM memory utilization exceeds the threshold continuously</td>
<td>The NameNode JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the DataNode heap memory size</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>Both NameNodes of HDFS are in Standby service status</td>
<td>Both NameNode roles are in Standby status at the same time</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="14"><strong>YARN</strong></td>
<td>The number of currently missing NodeManagers in the cluster exceeds the threshold continuously</td>
<td>The number of currently missing NodeManagers in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check the NodeManager process status and check whether the network connection is smooth</td>
<td>m=1, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of pending containers exceeds the threshold continuously</td>
<td>The number of pending containers has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Reasonably specify resources that can be used by YARN jobs</td>
<td>m=90, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster memory utilization exceeds the threshold continuously</td>
<td>The memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster memory utilization exceeds the threshold</td>
<td>The average memory utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster CPU utilization exceeds the threshold continuously</td>
<td>The CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster CPU utilization exceeds the threshold</td>
<td>The average CPU utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of available CPU cores in each queue is below the threshold continuously.</td>
<td>The number of available CPU cores in each queue has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Assign more resources to the queue</td>
<td>m=1, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in each queue is below the threshold continuously</td>
<td>The available memory in each queue has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Assign more resources to the queue</td>
<td>m=1024, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Active/Standby ResourceManagers were switched</td>
<td>Active/Standby ResourceManagers were switched</td>
<td>Check the ResourceManager process status and view the standby ResourceManager logs to locate the cause of active/standby switch</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in a ResourceManager</td>
<td>A full GC event occurred in a ResourceManager</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The ResourceManager JVM memory utilization exceeds the threshold continuously</td>
<td>The ResourceManager JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the ResourceManager heap memory size</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in a NodeManager</td>
<td>A full GC event occurred in a NodeManager</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in NodeManager is below the threshold continuously</td>
<td>The available memory in a single NodeManager has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=1, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The NodeManager JVM memory utilization exceeds the threshold continuously</td>
<td>The NodeManager JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td rowspan="13"><strong>HBase</strong></td>
<td>The number of regions in RIT status in the cluster exceeds the threshold continuously</td>
<td>The number of regions in RIT status in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>If the HBase version is below 2.0, run `hbase hbck -fixAssigment`</td>
<td>m=1, t=60</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The number of dead RegionServers exceeds the threshold continuously</td>
<td>The number of dead RegionServers has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average number of regions in each RegionServer in the cluster exceeds the threshold continuously</td>
<td>The average number of regions in each RegionServer in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=300, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred on HMaster</td>
<td>A full GC event occurred on HMaster</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The HMaster JVM memory utilization exceeds the threshold continuously</td>
<td>The HMaster JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HMaster heap memory size</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The number of current HMaster connections exceeds the threshold continuously</td>
<td>The number of current HMaster connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred in RegionServer</td>
<td>A full GC event occurred in RegionServer</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The RegionServer JVM memory utilization exceeds the threshold continuously</td>
<td>The RegionServer JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the RegionServer heap memory size</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current RPC connections to RegionServer exceeds the threshold continuously</td>
<td>The number of current RPC connections to RegionServer has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of RegionServer StoreFiles exceeds the threshold continuously</td>
<td>The number of RegionServer StoreFiles has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Run the major compaction</td>
<td>m=50000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred in HBase Thrift</td>
<td>A full GC event occurred in HBase Thrift</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The HBase Thrift JVM memory utilization exceeds the threshold continuously</td>
<td>The HBase Thrift JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HBase Thrift heap memory size</td>
<td>m=85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Both HMasters of HBase is in Standby service status</td>
<td>Both HMaster roles are in Standby status at the same time</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="4"><strong>Hive</strong></td>
<td>A full GC event occurred in HiveServer2</td>
<td>A full GC event occurred in HiveServer2</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The HiveServer2 JVM memory utilization exceeds the threshold continuously</td>
<td>The HiveServer2 JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HiveServer2 heap memory size</td>
<td>m=85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in HiveMetaStore</td>
<td>A full GC event occurred in HiveMetaStore</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in HiveWebHcat</td>
<td>A full GC event occurred in HiveWebHcat</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="2"><strong>ZooKeeper</strong></td>
<td>The number of ZooKeeper connections exceeds the threshold continuously</td>
<td>The number of ZooKeeper connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=65535, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of ZNodes exceeds the threshold continuously</td>
<td>The number of ZNodes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2000, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="8"><strong>Impala</strong></td>
<td>The ImpalaCatalog JVM memory utilization exceeds the threshold continuously</td>
<td>The ImpalaCatalog JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the ImpalaCatalog heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Impala daemon JVM memory utilization exceeds the threshold continuously</td>
<td>The Impala daemon JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>Adjust the ImpalaDaemon heap memory size	</td>
<td>m=0.85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The number of Impala Beeswax API client connections exceeds the threshold</td>
<td>The number of Impala Beeswax API client connections has been greater than or equal to m	</td>
<td>Adjust the value of `fs_sevice_threads` in the `impalad.flgs` configuration in the console	</td>
<td>m=64,t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of Impala HiveServer2 client connections exceeds the threshold</td>
<td>The number of Impala HiveServer2 client connections has been greater than or equal to m</td>
<td>Adjust the value of `fs_sevice_threads` in the `impalad.flgs` configuration in the console	</td>
<td>m=64,t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The query execution duration exceeds the threshold</td>
<td>The query execution duration exceeds m seconds</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The total number of failed queries exceeds the threshold</td>
<td>The total number of failed queries has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)	</td>
<td>Troubleshoot</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The total number of committed queries exceeds the threshold</td>
<td>The total number of committed queries has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)</td>
<td>Troubleshoot</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The query execution failure rate exceeds the threshold</td>
<td>The query execution failure rate has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)</td>
<td>Troubleshoot</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td rowspan="7"><strong>PrestoSQL</strong></td>
<td>The current number of failed PrestoSQL nodes exceeds the threshold continuously</td>
<td>The current number of failed PrestoSQL nodes has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of queuing resources in the current PrestoSQL resource group exceeds the threshold continuously</td>
<td>The number of queuing tasks in the PrestoSQL resource group has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>	Fine-tune the parameter settings</td>
<td>m=5000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed PrestoSQL queries exceeds the threshold</td>
<td>The number of failed PrestoSQL queries is greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred in a PrestoSQLCoordinator</td>
<td>A full GC event occurred in a PrestoSQLCoordinator</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The PrestoSQLCoordinator JVM memory utilization exceeds the threshold continuously</td>
<td>The PrestoSQLCoordinator JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the PrestoSQLCoordinator heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on a PrestoSQL worker</td>
<td>A full GC event occurred on a PrestoSQL worker</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The PrestoSQLWorker JVM memory utilization exceeds the threshold continuously</td>
<td>The PrestoSQLWorker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the PrestoSQLWorker heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="7"><strong>Presto</strong></td>
<td>The current number of failed Presto nodes exceeds the threshold continuously</td>
<td>The current number of failed Presto nodes has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of queuing resources in the current Presto resource group exceeds the threshold continuously</td>
<td>The number of queuing tasks in the Presto resource group has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>	Fine-tune the parameter settings</td>
<td>m=5000, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed Presto queries exceeds the threshold</td>
<td>The number of failed Presto queries is greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred on a PrestoSQL coordinator</td>
<td>A full GC event occurred on a PrestoSQL coordinator</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Presto coordinator JVM memory utilization exceeds the threshold continuously</td>
<td>The Presto coordinator JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Presto coordinator heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on a Presto worker</td>
<td>A full GC event occurred on a Presto worker</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Presto worker JVM memory utilization exceeds the threshold continuously</td>
<td>The Presto worker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Presto worker heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="6"><strong>Alluxio</strong></td>
<td>The current total number of Alluxio workers is below the threshold continuously</td>
<td>The current total number of Alluxio workers has been smaller than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The utilization of the capacity on all tiers of the current Alluxio worker exceeds the threshold</td>
<td>The utilization of the capacity on all tiers of the current Alluxio worker has been greater than or equal to the threshold for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>Fine-tune the parameter settings</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred on an Alluxio master</td>
<td>A full GC event occurred on an Alluxio master</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Alluxio master JVM memory utilization exceeds the threshold continuously</td>
<td>The Alluxio master JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>Adjust the Alluxio worker heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on an Alluxio worker</td>
<td>A full GC event occurred on an Alluxio worker</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Alluxio worker JVM memory utilization exceeds the threshold continuously</td>
<td>The Alluxio worker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Alluxio master heap memory size</td>
<td>m=0.85, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td rowspan="10"><strong>Kudu</strong></td>
<td>The cluster replica skew exceeds the threshold</td>
<td>The cluster replica skew has been greater than or equal to the threshold for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Run the `rebalance` command to balance the replicas</td>
<td>m=100, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The hybrid clock error exceeds the threshold</td>
<td>The hybrid clock error has been greater than or equal to the threshold for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>	Make sure that the NTP daemon is running and the network communication with the NTP server is normal</td>
<td>m=5000000, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of running tablets exceeds the threshold</td>
<td>The number of running tablets has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>	Too many tablets on a node can affect the performance. We recommend you clear unnecessary tables and partitions or expand the capacity as needed</td>
<td>	m=1000, t=300	</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed tablets exceeds the threshold</td>
<td>The number of failed tablets has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously	</td>
<td>Check whether any disk is unavailable or data file is corrupted</td>
<td>	m=1, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed data directories exceeds the threshold</td>
<td>The number of failed data directories has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously	</td>
<td>	Check whether the path configured in the `fs_data_dirs` parameter is available</td>
<td>		m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of full data directories exceeds the threshold</td>
<td>The number of full data directories has been greater than or equal to m for t (120 ≤ t ≤ 3,600) seconds continuously</td>
<td>Clear unnecessary data files or expand the capacity as needed</td>
<td>m=1, t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of write requests rejected due to queue overloading exceeds the threshold</td>
<td>The number of write requests rejected due to queue overloading has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously		</td>
<td>Check whether the number of write hotspots or worker threads is small</td>
<td>m=10, t=300	</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The number of expired scanners exceeds the threshold</td>
<td>The number of expired scanners has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Be sure to call the method for closing a scanner after reading data</td>
<td>m=100, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of error logs exceeds the threshold</td>
<td>The number of error logs has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=10, t=300	</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of RPC requests that timed out while waiting in the queue exceeds the threshold</td>
<td>The number of RPC requests that timed out while waiting in the queue has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Check whether the system load is too high</td>
<td>m=100, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
</tbody>
</table>
