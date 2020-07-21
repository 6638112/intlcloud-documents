## 1. Obtaining the Migration Tool  
 [Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to obtain the compressed migration tool package.

## 2. Choosing a Migration Mode Based on the Network Environment
Choose the appropriate migration mode according to the network environments of your source servers and destination CVMs.
Currently, the migration tool supports the default mode and the private network mode. The private network mode applies to three scenarios. Each migration mode or scenario has different network requirements for source servers and destination CVMs. If both source servers and destination CVMs can access the public network, you can use the default mode for migration. If source servers or destination CVMs cannot directly access the public network, you need to establish a connection between them through [VPC peering connections](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216) before using the private network mode for migration.

## 3. Backing up Data
- Source server: you can use the Alibaba Cloud snapshot feature or use other methods to back up data.
- Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.

## 4. Checking before Migrating
Before migrating, check the following on source servers and destination CVMs, respectively:
<table>
	<tr><th style="width: 15%;">Destination CVM</th><td><ol  style="margin: 0;"><li>Storage: the storage space in its cloud disks (including system disks and data disks) is sufficient to store the data from the source server.</li><li>Security group: the 443 and 80 ports must be open to the Internet in a security group.</li><li>Bandwidth: we recommend that you increase inbound and outbound bandwidth for faster migration. The traffic consumed during migration will be approximately equal to the data volume. If needed, change your network billing method in advance.</li><li>Operating system: we recommend using the same operating system on both the source server and the destination CVM. Different operating systems will result in inconsistency between the image that will be created later and the actual operating system. For example, when migrating a source server with the CentOS 7 system installed, choose a CVM with the CentOS 7 system installed as the migration destination.</li></ol></td></tr>
	<tr><th>Linux source server</th><td><ol  style="margin: 0;"><li>Check for and install Virtio. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li><li>Check whether rsync and grub2-install (or grub-install) are installed.</li><li>Check whether SELinux is enabled. Disable it if it is enabled.</li><li>Ensure the current system time is correct, because the Tencent Cloud API will use the UNIX timestamp to check against the generated token after receiving a migration request.</li></ol></td></tr>
</table>

>? 
> - You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server. 
> - The “go2tencentcloud” migration tool automatically checks the source server by default when it starts to run. If you want to skip this check and force migration, configure the value of the `Client.Extra.IgnoreCheck` field in the “client.json” file to `true`.
> 

## 5. Starting the Migration
 
1. (Optional) Establish a connection between the source server and the destination CVM.  
 - If you are using the private network mode, establish a connection between the source server and the destination CVM through [VPC peering connections](https://intl.cloud.tencent.com/document/product/553), [VPN connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
 - Skip to the next step if you are using the default mode.
2. Configure the “user.json” file.
The “user.json” file is used to configure the source server and the destination CVM. It contains the following configuration items:
 - The API keys of your account; that is, `SecretId` and `SecretKey`. For more information, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).
 - The region of the destination CVM.
 - The instance ID of the destination CVM.
 - (Optional) The data disk configuration of the source server.  
3. Configure the “client.json” file.
The “client.json” file is used to configure the migration mode and other parameters. You need to configure the `Client.Net.Mode` parameter in the “client.json” file, regardless of which migration modes or scenarios you select.
4. (Optional) Exclude files and directories that do not need to be migrated on the source server.  
 Edit the “rsync\_excludes\_linux.txt” file on the Linux source server to remove files and directories that do not need to be migrated.
5. Run the tool.
For example, on a 64-bit Linux source server, execute the following command as `root` to run the tool.
```
sudo ./go2tencentcloud_x64
```
If the following appears on the console, the migration has been completed successfully.
![](https://main.qcloudimg.com/raw/c77736b7fc0b465c53f0a14720155c47.png)
