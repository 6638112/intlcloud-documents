### Which operating systems are supported by CFS?
Linux, Unix, and Windows clients are supported.

### How is CFS billed?
CFS is billed hourly based on the peak storage usage for the hour.

### I have never used any resources in the Guangzhou region. Why are there fees for Guangzhou in CFS bills?
As storage usage in Mainland China is billed in a consolidated manner, the billing zone will be displayed as "South China (Guangzhou)" in CFS bills; the specific regions will be shown in the extended fields. This document describes how to view CFS bills in the console.

**Viewing your Bills**
1. Go to "[Billing Center](https://console.cloud.tencent.com/expense/overview) > Manage Bills > Billing Details > Resource ID Bills", click <img src="https://main.qcloudimg.com/raw/c861c752e9882ce5b8fbbb964b47b035.png"  style="margin:0;"> in the top-right corner, check "Extended Field 1" in the pop-up window, and click **OK**.
2. Scroll to the end of the table and you will see the notes on the consolidated billing zones of "Beijing, Guangzhou, Shanghai, and Chengdu" in the **Extended Field 1** column.


### Which access protocols are supported by CFS?
NFS v3.0/v4.0 and CIFS/SMB. CIFS/SMB file systems are in beta. For more information, go [here](https://intl.cloud.tencent.com/document/product/582/9553) to see **Notes on CIFS/SMB Beta Test**.

As clients on Windows and Linux 3.10 and its previous kernel version (e.g., CentOS 6.\*) are incompatible with NFS v4.0, they cannot work normally after mount. Please use NFS v3.0 instead.

### What concepts are used in CFS?
File system: a file system is a CFS instance. After a file system is mounted to a CVM instance, you can use it in the same way as a local storage system. It can be mounted to a subdirectory.

Mount target: A mount target is an entry for the compute node to access CFS. It defines the type of network for the node and the permission to access CFS.

### How many file systems can be created for each user?
Up to 10 file systems can be created in a region for each user. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) if you need to create more.

### What if a mount target is unavailable?
You can troubleshoot the problem in the following steps:
- View the error message.
- Check whether `nfs-utils`, `nfs-common`, and `cifs-utils` are installed.
- Check whether the local mount directory exists.
- Check whether the mount target is in the same VPC as the client server and whether they are in the same region.
- Check whether the client server has a security group policy prohibiting access to external ports. For more information on the specific ports, please see [the ports that need to be opened in a file system](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F).

### What should I do if an error is reported when I use the vers=4.0 mount command?

Client generally try to mount using NFS v4.1 Protocol first. Because CFS currently only supports NFS v4.0 Protocol, a `NFS4ERR_MINOR_VERS_MIMATCH` error may be reported. This does not affect the mount and can be ignored. The client will continue to try to mount using NFS v4.0.

### I installed Windows IIS web server in Windows Server 2016 operating system, but IIS and CIFS are incompatible?
When default security policies are changed in the Windows Server 2016 OS, the following configurations are needed.

1. Modify the registry key for SMB client:
```plaintext
HKEY_LOCAL_MACHINE> SYSTEM> CurrentControlSet> Services> LanmanWorkstation> Parameters> AllowInsecureGuestAuth
```
If the value already exists, set it to `1`. Otherwise, right click to select **Create**>**DWORD (32-bit) Value**, and set it to `AllowInsecureGuestAuth` with a value of `1`.
2. Specify a local user for storage access:
Open the Internet Information Services (IIS) Manager, and under the current host:
	1. Select **Sites**>**Default Web Site**, and click **Basic Settings".
	2. In the “Edit Site” dialog box, click **Connect as** to select a specific user.
	3. Click **Set** to set the user name and password.
	4. Click **OK**.



### What if data cannot be written to CFS?
You can troubleshoot the issue as follows:
- View the error message.
- Check the client server’s network condition and run `telnet` to verify whether the port of the mount target is open. For more information on the specific ports, please see [the ports that need to be opened in a file system](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F). 
- If the file system is not mounted to the mount target's root directory, check whether the corresponding mount target directory exists (the common error message in this case is `Stale file handle`. You can check whether the subdirectory exists through a device mounted to the root directory).

### Which ports need to be opened in a file system?

File System Protocol | Port | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet file system IP 2049
NFS 4.0 | 2049 | telnet file system IP 2049
CIFS/SMB | 445 | telnet file system IP 445 

> CFS currently do not support `ping`.

### What if the configured access permission does not take effect?
For an NFS file system, multiple rules can be configured, which will take effect based on their priorities:
- If the permission of a single IP conflicts with that of an IP within an IP range in the same permission group, the permission with a higher priority will prevail. If their priority levels are the same, the permission of the single IP will prevail.
- If two overlapping IP ranges are configured with different permissions and the same priority levels, the permissions of the overlapping ranges will take effect randomly. Please avoid configuring overlapping IP ranges. 

>Priority configuration is not supported for CIFS/SMB file systems and will not take effect.

### How can I speed up copying local files to CFS?
For Linux, use the `shell` script below to accelerate copying local files to CFS. The "number of threads" in the following code can be adjusted as needed.
```bash
threads=<number of threads>; src=<source path/>; dest=<target path/>; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )

<!--Example: threads=24; src=/root/github/swift/; dest=/nfs/; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )-->
```

### What should I do if an exception occurs when renaming a file or directory on Windows?
Due to issues between the client and the supported protocols, renaming a file or directory may fail if a Windows client mounts the file system with NFS. In this case, we recommend using CIFS/SMB for CFS file systems on Windows.


### What if a file system has no write permission on Windows after being mounted with NFS?
Please strictly follow the operation guide. Add `AnonymousUid` and `AnonymousGid` to the Registry and try again after restarting the system.
For more information, please see [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524)

### What if mapped drives cannot be used with Windows IIS?
You can configure the correct NFS client program and modify the Registry (by adding users for access) as instructed in [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524).
Restart the client, open the IIS configuration page, add a site, and click **Advanced Settings**.
![](https://main.qcloudimg.com/raw/871a0b585060646f662fa4c8e111df36.png)
Set the "Physical Path" in the "Advanced Settings" to the CFS mount target.
![](https://main.qcloudimg.com/raw/44777ef4949311c8db84f972b2885af9.png)

### Mounting a CFS file system on Docker or Kubernetes sometimes succeed and sometimes fail. How can I resolve this issue?

This issue is caused by protocol compatibility. NFS v3 is recommended for mounting CFS with clients such as Docker and Kubernetes. Using NFS v4 may lead to issues with some clients.

### What if I want to use a CFS file system on Window Server 2012 R2 as IIS server directory, but the file system cannot be mounted?

IIS will convert the FSID needed for mounting with NFS v3.0 to uppercase, which prevents the file system from being mounted. We recommend using Windows Server 2016 to avoid this issue.

### How can I continue using CFS in an AZ where CFS resources are sold out?

Assume that there is a CVM instance in Guangzhou Zone 1 that needs to use CFS, but file systems cannot be directly created in Guangzhou Zone 1 as the resources are sold out there.
**In a VPC**
If the CVM instance is in the "Guangzhou Zone 1" subnet of a VPC, you can log in to the [VPC Console](https://console.cloud.tencent.com/vpc) to create a subnet whose AZ is "Guangzhou Zone 2" for the VPC.
![](https://main.qcloudimg.com/raw/8fcb0be11627236c99cef6b54d129ac6.png)
![](https://main.qcloudimg.com/raw/261ea1f31f78b0955221cc0f1288285f.png)

After the subnet is successfully created, go back to the CFS Console and select this VPC and the subnet you just created to create resources in Guangzhou Zone 2. The CFS file system can be directly mounted to the CVM instance in the subnet of Guangzhou Zone 1 in this VPC.
CIFS/SMB file system user guide:
- [Linux](https://intl.cloud.tencent.com/document/product/582/11523)
- [Windows](https://intl.cloud.tencent.com/document/product/582/11524)

**In the classic network** 
If the CVM instance resides in the classic network, you can create a VPC and a subnet in Guangzhou Zone 2, and then create a file system in this network. With Classiclink, you can connect the classic network and the VPC for access. For more information, please see [Managing Basic Networks](https://intl.cloud.tencent.com/document/product/215/31807).

### The file content update is out of sync. How can I fix this?
#### Issue
An NFS file system is mounted to two Linux-based CVM instances. Use `append` to write a file to CVM instance A, and use `tail -f` to observe the changes to the file on CVM instance B. After data is written to the file on CVM instance A, it will take 10–30 seconds for the updated content to display on CVM instance B. However, in the same scenario, if you open the file directly on CVM instance B (e.g., using the `vi` command), you can view the update immediately.

#### Cause
This issue is related to the option of the NFS mount command and the implementation of `tail -f`. You can use the following mount command:   
```bash
sudo mount -t nfs -o vers=4.0 <mount target IP>:/ <destination mount directory>
```

If CVM instance B mounts the file system with the NFS mount command, the kernel will maintain a metadata cache of the file and directory attributes (e.g., permissions, size, and timestamp) by default. The purpose of caching is to reduce the number of `NFSPROC_GETATTR` remote procedure calls (RPCs).

`tail -f` observes the changes to file attributes (mainly the file size) through `sleep+fstat` and then reads the file and outputs the content. The result of `fstat` determines whether `tail -f` can output the file content in real time. However, due to the metadata cache of file and directory attributes, `fstat` cannot poll real-time file attributes. As a result, although the file on the NFS server has been updated, `tail -f` cannot observe the change, which causes an output delay.

#### Solution
Add the `noac` option when mounting the file system with the mount command to disable the caching of file and directory attributes. The mount command is as follows:
```bash
sudo mount -t nfs -o vers=4 noac <mount target IP>:/ <destination mount directory>
sudo mount -t nfs -o vers=3,noac,nolock,proto=tcp <mount target IP>:/<FSID or subdirectory> <destination mount directory>
```

### What should I do if an error `0x800704C9` occurs when a file system is mounted with NFS to a client based on Windows 7 or Windows Server 2008 R2?

#### Cause
These clients cache the original port numbers used to communicate with nlockmgr. For details, see the help documentation on Microsoft's website [here](https://support.microsoft.com/en-us/help/2761774/0x800704c9-error-when-you-copy-files-to-an-nfs-server-from-a-windows-7).

#### Solution
Run Windows Update to upgrade the OS to the latest version to fix this issue.
