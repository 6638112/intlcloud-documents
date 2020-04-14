The Event Center of Cloud Monitor (CM) currently provides the following monitoring information for product events:
<html>

<style type="text/css">
.div-table-1 {width:100%;}
.div-table-1 td{white-space:pre-wrap; }
.div-td-el{word-wrap:break-word;word-break:break-all;}
.div-td-1{width:12%}
.div-td-2{width:12%}
.div-td-3{width:8%}
.div-td-4{width:12%}
.div-td-5{width:8%}
.div-td-6{width:20%}
.div-td-7{width:28%}
</style>
<h2>CVM</h2>
<table class="div-table-1">
<thead>
<tr>
<th class="div-td-1">Event<br>Name</th>
<th class="div-td-2">Event<br>Parameter</th>
<th class="div-td-3">Event<br>Type</th>
<th class="div-td-4">Dimension</th>
<th class="div-td-5">Recoverable<br><br></th>
<th class="div-td-6">Description</th>
<th class="div-td-7">Solution and Suggestion</th>
</tr>
</thead>
<tbody><tr>
<td class="div-td-1">Kernel failure</td>
<td class="div-td-2 div-td-el">GuestCoreError</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">No</td>
<td class="div-td-6">An OS kernel bug or driver issue causes a fatal error in the OS kernel</td>
<td class="div-td-7">1. Check whether any kernel driver modules are loaded into the system other than those provided by the kernel. Try not to load these modules and observe the operating status of the system. <br>2. View the bug reports of the kernel and OS, and try to upgrade the kernel. <br>3. By default, kdump is enabled for CVM. When a panic occurs, system memory dump information will be generated in the /var/crash directory. You can analyze it with the crash tool</td>
</tr>
<tr>
<td class="div-td-1">OOM</td>
<td class="div-td-2 div-td-el" >GuestOom</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">No</td>
<td class="div-td-6">System memory usage is overloaded</td>
<td class="div-td-7">1. Check whether the memory capacity configured in the current system meets business requirements. If additional capacity is required, we recommend you upgrade the CVM memory configuration. <br>2. View processes that are killed during OOM based on system logs such as dmesg and /var/log/messages to check whether the process memory is used as expected. Use tools such as valgrind to analyze whether memory leakage occurs</td>
</tr>
<tr>
<td class="div-td-1">ping failure</td>
<td class="div-td-2 div-td-el" >PingUnreachable</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-6">The network of the CVM instance is unpingable</td>
<td class="div-td-7">1. Check whether the running status of the CVM instance is normal. If any exception occurs (for example, the system crashes), force restart the CVM instance in the console to recover it. <br>2. If the CVM instance is running normally, check the CVM network configuration, including the internal network service configuration, firewall configuration, security group configuration, etc.</td>
</tr>
<tr>
<td class="div-td-1">Read-only disk</td>
<td class="div-td-2 div-td-el">DiskReadonly</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-6">Data cannot be written into the disk</td>
<td class="div-td-7">1. Check whether the disk is full. <br>2. On Linux, run the `df -i` command to check whether inode is used up. <br>3. Check whether the file system is corrupted</td>
</tr>
<tr>
<td class="div-td-1">Server restart</td>
<td class="div-td-2 div-td-el">GuestReboot</td>
<td class="div-td-3">Status<br>change</td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-6">The CVM instance restarts</td>
<td class="div-td-7">This event is triggered when the CVM restarts. Check whether the status change is as expected based on actual scenarios</td>
</tr>
<tr>
<td class="div-td-1">Packet loss occurs when the public network outbound bandwidth exceeds the limit</td>
<td class="div-td-2 div-td-el">PacketDroppedByQosWanOutBandwidth</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-6">The public network outbound bandwidth of the CVM instance exceeds the upper limit, causing packet loss. Packet loss caused by bandwidth glitches is not reflected on the bandwidth view, because the minimum granularity for bandwidth statistics is 10 (total traffic in 10 seconds/10 seconds). If the constant bandwidth is not exceeded by much, it can be ignored</td>
<td class="div-td-7">Increase the upper limit for public network bandwidth.<br>If the maximum limit can be purchased has been reached, <br>you can reduce the bandwidth consumption of the server through load balancing and other means</td>
</tr>
<tr>
<td class="div-td-1">Packet loss occurs when the number of connections exceeds the limit</td>
<td class="div-td-2 div-td-el">PacketDroppedByQosConnectionSession</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">CVM instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-6">There are too many connections to the CVM instance, causing packet loss</td>
<td class="div-td-7">Contact after sales service</td>
</tr>
</tbody></table>

<h2>CLB</h2>
<table class="div-table-1">
<thead>
   <tr>
     <th class="div-td-1">Event<br>Name</th>
     <th class="div-td-2">Event<br>Parameter</th>
     <th class="div-td-3">Event<br>Type</th>
     <th class="div-td-4">Dimension</th>
     <th class="div-td-5">Recoverable<br></th>
     <th class="div-td-6">Description</th>
     <th class="div-td-7">Solution and Suggestion</th>
   </tr>
 </thead>
 <tbody>
   <tr>
      <td class="div-td-1">Blocked public IP</td>
      <td class="div-td-2 div-td-el">VipBlockInfo</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">CLB instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">The CLB public IP under attack is blocked after an exception is detected by the security protection system</td>
      <td class="div-td-7">Submit a ticket for specific causes and solutions</td>
   </tr>
    <tr>
      <td class="div-td-1">Server port status has an exception</td>
      <td class="div-td-2 div-td-el">RsPortStatusChange</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">Real server port</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">An exception is found at the real server port of the public network CLB instance during health check</td>
      <td class="div-td-7">View the service status of the real server port</td>
   </tr>
 </tbody>
   </table>

<h2>VPN Gateway</h2>
<table class="div-table-1">
<thead>
<tr>
<th class="div-td-1">Event<br>Name</th>
<th class="div-td-2">Event<br>Parameter</th>
<th class="div-td-3">Event<br>Type</th>
<th class="div-td-4">Dimension</th>
<th class="div-td-5">Recoverable<br></th>
<th class="div-td-7">Description</th>
<th class="div-td-6">Solution and Suggestion</th>
</tr>
</thead>
<tbody>
<tr>
<td class="div-td-1">Packet loss occurs when the public network outbound bandwidth exceeds the limit</td>
<td class="div-td-2 div-td-el">PacketDroppedByQosWanOutBandwidth</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">VPN Gateway instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-7">The public network outbound bandwidth of the VPN Gateway instance exceeds the upper limit, causing packet loss. Packet loss caused by bandwidth glitches is not reflected on the bandwidth view, because the minimum granularity for bandwidth statistics is 10 (total traffic in 10 seconds/10 seconds). If the constant bandwidth is not exceeded by much, it can be ignored</td>
<td class="div-td-6">Increase the upper limit for public network bandwidth</td>
</tr>
<tr>
<td class="div-td-1">Packet loss occurs when the number of connections exceeds the limit</td>
<td class="div-td-2 div-td-el">PacketDroppedByQosConnectionSession</td>
<td class="div-td-3">Exception<br></td>
<td class="div-td-4">VPN Gateway instance</td>
<td class="div-td-5">Yes</td>
<td class="div-td-7">There are too many connections to the VPN Gateway instance, causing packet loss</td>
<td class="div-td-6">Contact after sales service</td>
</tr>
</tbody>
</table>

<h2>TKE</h2>
<table class="div-table-1">
<thead>
<tr>
	 <th class="div-td-1">Event<br>Name</th>
     <th class="div-td-2">Event<br>Parameter</th>
     <th class="div-td-3">Event<br>Type</th>
     <th class="div-td-4">Dimension</th>
     <th class="div-td-5">Recoverable<br></th>
     <th class="div-td-6">Description</th>
     <th class="div-td-7">Solution and Suggestion</th>
</tr>
</thead>
<tr>
     <td class="div-td-1">Node exception</td>
     <td class="div-td-2 div-td-el">NodeNotReady</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">Yes</td>
     <td class="div-td-7">A node exception may be caused by a variety of reasons, such as network disconnection, node kubelet exception, and container OOM. If the node has an exception for a long time, Kubernetes will drain the containers on the node</td>
     <td class="div-td-6">1. Check whether the node is running on the CVM monitoring page.<br>2. Log in to the node server to check whether kubelet is running normally. 3. Log in to the node server to check whether docker is running normally</td>
</tr>
<tr>
     <td class="div-td-1">Node disk capacity will run out soon</td>
     <td class="div-td-2 div-td-el">NodeHasDiskPressure</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">Yes</td>
     <td class="div-td-7">The disk (cbs or root) capacity used for container and image storage on the node will run out soon. NodeOutOfDisk will be triggered after the capacity runs out, and new containers cannot be scheduled to this node</td>
     <td class="div-td-6">Clean up the disk or container images no longer in use</td>
</tr>
<tr>
     <td class="div-td-1">Node disk capacity has run out</td>
     <td class="div-td-2 div-td-el">NodeOutOfDisk</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">Yes</td>
     <td class="div-td-7">The disk (cbs or root) capacity used for container and image storage on the node has run out, and new containers cannot be scheduled to this node</td>
     <td class="div-td-6">Clean up the disk or container images no longer in use</td>
</tr>
<tr>
     <td class="div-td-1">Insufficient node memory</td>
     <td class="div-td-2 div-td-el">NodeHasInsufficientMemory</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">Yes</td>
     <td class="div-td-7">The node memory utilization is high</td>
     <td class="div-td-6">Expand the node or schedule containers to other nodes</td>
</tr>
<tr>
     <td class="div-td-1">Node OOM</td>
     <td class="div-td-2 div-td-el">SystemOOM</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">No</td>
     <td class="div-td-7">OOM occurs on the node due to high memory utilization</td>
     <td class="div-td-6">Check the cause of OOM on the node by viewing monitoring data, syslog, demsg, etc.</td>
</tr>
<tr>
     <td class="div-td-1">Unreachable node network</td>
     <td class="div-td-2 div-td-el">NodeNetworkUnavailable</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">No</td>
     <td class="div-td-7">The network on the node is not configured properly. Normally, this problem will not occur to clusters created through the console or Tencent Cloud API</td>
     <td class="div-td-6">Submit a ticket or contact after sales service</td>
</tr>
<tr>
     <td class="div-td-1">Insufficient inodes on the node</td>
     <td class="div-td-2 div-td-el">NodeInodePressure</td>
     <td class="div-td-3">Exception<br></td>
     <td class="div-td-4">Cluster</td>
     <td class="div-td-5">No</td>
     <td class="div-td-7">Insufficient inodes on the node will prevent the node from creating containers</td>
     <td class="div-td-6">Check the remaining inodes on the node. Try to clean up container images no longer in use to free up inode space</td>
</tr>
</tbody>
</table>

<h2>TencentDB for MySQL</h2>
<table class="div-table-1">
<thead>
<tr>
      <th class="div-td-1">Event<br>Name</th>
      <th class="div-td-2">Event<br>Parameter</th>
      <th class="div-td-3">Event<br>Type</th>
      <th class="div-td-4">Dimension</th>
      <th class="div-td-5">Recoverable<br></th>
      <th class="div-td-6">Description</th>
      <th class="div-td-7">Solution and Suggestion</th>
</tr>
</thead>
<tbody>
   <tr>
      <td class="div-td-1">OOM</td>
      <td class="div-td-2 div-td-el">OutOfMemory</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MySQL instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">Database memory usage is overloaded</td>
      <td class="div-td-7">Check whether the memory capacity configured in the database meets business requirements. If additional capacity is required, we recommend you upgrade the MySQL memory configuration</td>
   </tr>
   <tr>
      <td class="div-td-1">Master/slave switchover</td>
      <td class="div-td-2 div-td-el">PrimarySwitch</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MySQL instance</td>
      <td class="div-td-5">No</td>
      <td class="div-td-6">Master/slave switchover occurs</td>
      <td class="div-td-7">This event may be triggered when a physical machine fails. Check whether the instance status is normal</td>
   </tr>
   <tr>
      <td class="div-td-1">Removal of read-only instance</td>
      <td class="div-td-2 div-td-el">RORemoval</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MySQL instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">A read-only instance fails or exceeds the latency threshold</td>
      <td class="div-td-7">If the read-only group contains only one read-only instance, promptly switch the read traffic after deleting this read-only instance to avoid single points of failure. We recommend you purchase at least two read-only instances for the group</td>
   </tr>
   <tr>
      <td class="div-td-1">Instance migration caused by server failure</td>
      <td class="div-td-2 div-td-el">ServerfailureInstanceMigration</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MySQL instance</td>
      <td class="div-td-5">No</td>
      <td class="div-td-6">Instance migration is caused by a server failure</td>
      <td class="div-td-7">The migration time is subject to the maintenance window. Please change the time promptly if needed. The new migration time will be subject to the new maintenance window
      </td>
   </tr>
</tbody>
</table>

<h2>TencentDB for MongoDB</h2>
<table class="div-table-1">
<thead>
	<tr>
      <th class="div-td-1">Event<br>Name</th>
      <th class="div-td-2">Event<br>Parameter</th>
      <th class="div-td-3">Event<br>Type</th>
      <th class="div-td-4">Dimension</th>
      <th class="div-td-5">Recoverable<br></th>
      <th class="div-td-6">Description</th>
      <th class="div-td-7">Solution and Suggestion</th>
	</tr>
	<tr>
      <td class="div-td-1">Insufficient backup oplog</td>
      <td class="div-td-2 div-td-el">oplogInsufficient</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MongoDB instance</td>
      <td class="div-td-5">No</td>
      <td class="div-td-6">When TencentDB for MongoDB is backing up data, it cannot read the full oplog from the last backup to the current backup. This affects database rollback to any time point in the last 7 days</td>
      <td class="div-td-7">We recommend you adjust the size or backup frequency of MongoDB oplog on the TencentDB for MongoDB Console. If you do not need this event notification, you can disable it on the backup page in the console</td>
    </tr>
    <tr>
      <td class="div-td-1">The number of connections exceeds the limit</td>
      <td class="div-td-2 div-td-el">connectionOverlimit</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MongoDB instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">The number of connections to the instance exceeds the limit</td>
      <td class="div-td-7">Check whether the maximum number of connections configured for the TencentDB for MongoDB instance meets business requirements. If additional connections are required, we recommend you upgrade the instance configuration</td>
    </tr>
    <tr>
      <td class="div-td-1">Master/slave switchover</td>
      <td class="div-td-2 div-td-el">primarywitch</td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MongoDB instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">Switchover occurs between primary and secondary databases</td>
      <td class="div-td-7">This event may be triggered when a physical machine fails. Check whether the instance status is normal</td>
    </tr>
    <tr>
      <td class="div-td-1">The disk capacity has run out</td>
      <td class="div-td-2 div-td-el">instanceOutOfDisk </td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MongoDB instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">The disk capacity is full and the instance becomes read-only</td>
      <td class="div-td-7">Clean up the disk</td>
    </tr>
    <tr>
      <td class="div-td-1">Instance rollback</td>
      <td class="div-td-2 div-td-el">instanceRollback </td>
      <td class="div-td-3">Exception<br></td>
      <td class="div-td-4">TencentDB for MongoDB instance</td>
      <td class="div-td-5">Yes</td>
      <td class="div-td-6">The instance data is rolled back</td>
      <td class="div-td-7">This event may be triggered if the master node fails and a master/slave switchover occurs when some data on the master node has not been synced to the slave node in time. Check whether the instance status is normal</td>
    </tr>
</thead>
</table>

<h2>Direct Connect (Connection, Dedicated Tunnel)</h2>
<table class="div-table-1">
<thead>
		<tr>
         <th class="div-td-1">Event<br>Name</th>
         <th class="div-td-2">Event<br>Parameter</th>
         <th class="div-td-3">Event<br>Type</th>
         <th class="div-td-4">Dimension</th>
         <th class="div-td-5">Recoverable<br></th>
         <th class="div-td-6">Description</th>
         <th class="div-td-7">Solution and Suggestion</th>
		</tr>
    </thead>
<tbody>
		<tr>
			<td class="div-td-1">Connection downtime</td>
			<td class="div-td-2 div-td-el">DirectConnecDown</td>
			<td class="div-td-3">Exception<br></td>
			<td class="div-td-4">Connection</td>
			<td class="div-td-5">Yes</td>
			<td class="div-td-6">The physical linkage transmission of the connection is interrupted or has an exception</td>
			<td class="div-td-7">1. Check whether the physical line has an exception or is interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.) <br>2. Check whether the receiving port and optical/electrical modules are functioning normally<br>3. Check whether the network device port is turned off</td>
		</tr>
		<tr>
			<td class="div-td-1">Dedicated tunnel downtime</td>
			<td class="div-td-2 div-td-el">DirectConnectTunnelDown</td>
			<td class="div-td-3">Exception<br></td>
			<td class="div-td-4">Dedicated tunnel</td>
			<td class="div-td-5">Yes</td>
			<td class="div-td-6">The physical linkage transmission of the connection is interrupted or exceptional</td>
			<td class="div-td-7">1. Check whether the physical line has an exception or is interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.) <br>2. Check whether the receiving port and optical/electrical modules are functioning normally<br>3. Check whether the network device port is turned off</td>
		</tr>
		<tr>
			<td class="div-td-1">Dedicated tunnel BGP session downtime</td>
			<td class="div-td-2 div-td-el">DirectConnectTunnelBGPSessionDown</td>
			<td class="div-td-3">Exception<br></td>
			<td class="div-td-4">Dedicated tunnel</td>
			<td class="div-td-5">Yes</td>
			<td class="div-td-6">The dedicated tunnel BGP session is interrupted</td>
			<td class="div-td-7">1. Check whether the BGP process of the network device is normal <br>2. Check whether the dedicated tunnel is normal <br>3. Check whether the physical line is normal</td>
		</tr>	
		<tr>
			<td class="div-td-1">Alarm for excessive BGP tunnel routes</td>
			<td class="div-td-2 div-td-el">DirectConnectTunnelRouteTableOverload</td>
			<td class="div-td-3">Exception<br></td>
			<td class="div-td-4">Dedicated tunnel</td>
			<td class="div-td-5">No</td>
			<td class="div-td-6">The number of BGP session routes in a dedicated tunnel exceeds 80% of the threshold</td>
			<td class="div-td-7">1. Check whether the routes published by the dedicated tunnel's BGP session reaches 80% of the upper limit (the default value is 100. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/216/546">here</a>)</td>
		</tr>
</tbody>
</table>

</html>

