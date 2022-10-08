### Expanding cloud system disks
- [Expanding cloud system disks via the CVM console](https://intl.cloud.tencent.com/document/product/362/5747)




### Expanding cloud data disks

To expand a data disk, the following three methods are provided.
- [Expanding via the CVM console](https://intl.cloud.tencent.com/document/product/362/5747)
- [Expanding cloud disks via the CBS console](https://intl.cloud.tencent.com/document/product/362/5747)
- [Expanding cloud disks via API](https://intl.cloud.tencent.com/document/product/362/5747)




Based on the **attaching** status of CBS data disks, you can expand their capacity by different methods.
- If the current CBS data disk **can be detached**, you can expand its capacity in the CBS console or via the [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310) API.
- If the current CBS data disk **cannot be detached**, you can expand its capacity in the CVM console or via the [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310) API.



<dx-alert infotype="notice" title="">
If the maximum capacity of the cloud disk cannot meet your business needs, try [building up RAID groups](https://intl.cloud.tencent.com/document/product/362/2932) or [building LVM logical volumes with multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).
</dx-alert>


Once the data disk capacity is expanded, you must perform the following operations for the instance to recognize and use the data disk:
<table>
     <tr>
         <th nowrap="nowrap">Before Expansion</th>  
         <th nowrap="nowrap">After Expansion</th>  
		 <th>Subsequent operations</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">File system not created</td>
         <td>Disk capacity < 2 TB</td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (<2 TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Disk capacity ≥ 2 TB</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (≥2 TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">File system created</td>
         <td>Disk capacity < 2 TB</td>
    		 <td><ul><li>Cloud disks attached to a Windows CVM: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li>
			 <li>Expanded cloud disk attached to a Linux CVM: <a href="https://intl.cloud.tencent.com/document/product/362/39995">extending partitions and file systems (Linux)</a></li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Disk capacity ≥ 2 TB</td>
         <td>
				 <ul><li>GPT partition format: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a> or <a href="https://intl.cloud.tencent.com/document/product/362/39995">extending partitions and file systems (Linux)</a></li>
				 <li>MBR partition format: Not supported.</li>MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and attach a new data disk and use the GPT partition format to copy data.</ul>
				 </td>
     </tr>
</table>


