### What is COS?
Tencent Cloud Cloud Object Storage (COS) is a cloud-based non-hierarchical distributed storage service that provides cost-effective, fast, and reliable data storage solutions. COS stores your data across multiple AZs, incorporating redundant storage to ensure data reliability, and allows multiple clients or application threads to read or write data at the same time.

You can use web APIs to store and retrieve data through CVM instances or over the internet. You can also use the URL of a specified domain name to store and retrieve individual data object in COS through HTTP or HTTPS protocol.

For more information on COS, see [COS Product Overview](https://intl.cloud.tencent.com/document/product/436).


### What is the difference between Cloud Object Storage (COS) and Cloud File Storage (CFS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limit on directory hierarchy or data format and can store any amount of data. There is no upper limit on bucket storage capacity and no partitioning is required. It supports HA deployment to ensure the eventual consistency of data but does not support features such as file locking. COS APIs support data access using through HTTP or HTTPS protocol, and COS offers a variety of SDKs and tools that can be integrated into your business. Objects uploaded to COS can also be accessed or downloaded directly via a URL.

[Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582) uses common network file transfer protocols, can create file systems and implement large-scale expansion, but needs to be mounted onto CVM. It can store data for a wide range of applications such as websites, online distributors, and archives. Featuring high computing throughput and extremely high availability and persistence, it is also suitable for scenarios demanding high concurrence or shared storage.

### What is the difference between COS and Cloud Block Storage (CBS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limits on file systems, directory structure, file number, or storage capacity and needs to be managed and accessed via web APIs. COS offers various SDKs and tools for business integration, which can be used independently without CVM. COS supports access to massive amounts of data but is not suitable for scenarios involving millisecond-level response or random I/O.

[Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) needs to be used together with CVM and can only be mounted and used after the file system is partitioned or formatted. It comes in different types with various performance metrics such as IOPS and throughput for different scenarios.


### Why does the access link of a public-read file expire?

You can go to the object details page on the [COS Console](https://console.cloud.tencent.com/cos) to get the object address and signature link.

If your file is public-read:

- If you want to make it accessible to others all the time, we recommend directly using the object address.
- If you want to make it accessible to others for only a certain period of time, we recommend directly copying the signature link, which carries the signature parameter and is valid for 1 hour.

If your file is private:

- If you want to make it accessible to others all the time, we recommend changing its access permission to public-read/private-write and using the object address.
- If you want to make it accessible to others for only a certain period of time, we recommend directly copying the signature link, which carries the signature parameter and is valid for 1 hour.


### What is a "folder" or "directory" in COS?

Strictly speaking, the concepts of folders and directories do not apply to COS. However, taking into account the usage habits of different users, COS can display “folders” on the console just like the directory structure of a traditional file management system. For more information, see [Folder and directory](https://intl.cloud.tencent.com/document/product/436/13324).

### Can COS files be recovered after being deleted?

The data redundancy storage mechanism of COS is designed for scenarios where it is necessary to recover data in case of hardware failure. If you manually delete your data from COS or configure automated deletion, Tencent Cloud will delete the data as requested after which the data is irrecoverable.

You can proactively delete files in the following ways:

- Deleting files via the COS Console by deleting a single file, deleting files in batches, clearing incomplete multipart uploads, or emptying buckets.
- Deleting files using COSCMD or COSBrowser.
- Deleting files using the COS APIs or SDKs.
- Configuring the system to delete files regularly through the COS lifecycle management feature.
- Syncing the CRUD operations between buckets in different regions using the COS cross-region replication sync feature, so that existing files with the same name will be overwritten or deleted.

### How can I avoid accidental deletion?

- The best way to avoid accidental deletion is to back up the files in your bucket on a regular basis. You can protect your data in the following ways:
  - Downloading COS objects to your local file system or third-party servers using the [COSCMD tool](https://intl.cloud.tencent.com/document/product/436/10976).
  - Performing intra-region or cross-region bucket data backup using the [COS Migration Tool](https://intl.cloud.tencent.com/document/product/436/30585) or the cross-region replication feature.
  - Regularly backing up your data to other COS buckets using COS APIs or SDKs.
  - Saving your past versions of data using versioning.
- Using COS permission management. For more information, see [Cloud Access Management Practices](https://intl.cloud.tencent.com/document/product/436/12469):
  - Separating read permission and write permission. For businesses where it is only necessary to read data, use a sub-account with read permission or a temporary key to access the data.
  - Separating permissions for different buckets. For different businesses, only authorize permissions for buckets, directories, and operations within the scope of that particular business.
  - Not using a root account to access COS.
  - Accessing COS using a temporary key.
  - Properly managing your data access credentials, such as your Tencent Cloud account password, CAM sub-account access credentials, and TencentCloud API key.


### Does COS support statistics collection?

COS is capable of monitoring stored data and displaying the details and trends of various metrics in the monitoring window. To view general data trends, go to the **Overview** page on the [COS Console](https://console.cloud.tencent.com/cos5), and you can view data such as storage size, request number, and traffic for each storage class.
To view the statistics of a single bucket, see [Querying Monitoring Data](https://intl.cloud.tencent.com/document/product/436/31634).

In addition to the COS Console, you can also view the monitoring information of different buckets on the [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) page where you can also configure different alarm policies to fit your business needs.

### Does COS support image processing?

The COS console has integrated Cloud Infinite features, which enable you to scale, crop, and add watermarks to your images. For more information, see [Enabling Image Processing](https://intl.cloud.tencent.com/document/product/436/36569).



### Does COS support image compression?

COS is a distributed storage service for unstructured data and cannot support image compression on its own. For more information on image compression, see [Cloud Infinite](https://intl.cloud.tencent.com/product/ci).

### Does COS support thumbnails?

COS is a distributed storage service for unstructured data and cannot support thumbnails on its own. For more information on thumbnails, see [Cloud Infinite](https://intl.cloud.tencent.com/product/ci).

### Does COS support transcoding video files?

COS is a distributed storage service for unstructured data and cannot support video transcoding on its own. For information on how to transcode video files, see [Media Processing Service](https://intl.cloud.tencent.com/product/mps).

### Does COS support the auto decompression of uploaded files?

COS is a distributed storage service for unstructured data and does not support file decompression on its own. To enable this feature, please use the integrated SCF service. For more information, see [File Decompression](https://intl.cloud.tencent.com/document/product/436/35663).

### What are the specifications and limits of COS?

For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Which version of COS should I use, an earlier version or the current version?

The implementation of earlier versions of COS is quite different than that of the current version. The current version has more features than earlier versions, and earlier versions are not updated with the latest features. **We recommend that you use the current version** for a better experience. If you are using an earlier version, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to activate the current version.

The current version comes with different APIs and SDK APIs than those in earlier versions. JSON APIs are used in earlier versions and XML APIs are used in the current version. JSON APIs have the same underlying architecture as XML APIs. Their data is interoperable and can intersect, but they are ultimately not compatible with each other and have different domain names.

### How do I monitor error code information?

You can use [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) to get different types of HTTP error code messages. For more information, see [Monitoring and Alarming](https://intl.cloud.tencent.com/document/product/436/31649). For information on how to use Cloud Monitoring to obtain relevant data, see Cloud Monitoring’s [Console Guide](https://intl.cloud.tencent.com/document/product/248) .  


### How do I calculate the availability of COS?
Please reference the following example for information on how to calculate COS availability:
Tom uses Tencent Cloud COS to run his e-commerce business. Assume that his business consumed a total of 100 USD in the service period from Nov. 1 to Nov. 30, 2018, during which two unavailability events occurred, as shown below:

<table>
   <tr>
      <th>Unavailability Event No.</th>
      <th>Duration</th>
      <th>5-Minute Record of Unavailability Event</th>
      <th>HTTP Return Code</th>
      <th>Number of Failing Requests</th>
      <th>Number of Valid Requests</th>
   </tr>
   <tr>
      <td rowspan=3><center>1<center></td >
      <td rowspan=3>15 min</td>
      <td>November 15, 2018, 10:00 - 10:05</td>
      <td>503</td>
      <td>100</td>
      <td>100</td>
   </tr>
   <tr>
      <td>November 15, 2018, 10:05 - 10:10</td>
      <td>503</td>
      <td>99</td>
      <td>100</td>
   </tr>
   <tr>
      <td>November 15, 2018, 10:10 - 10:15</td>
      <td>503</td>
      <td>98</td>
      <td>100</td>
   </tr>
   <tr>
      <td rowspan=3><center>2<center></td>
      <td rowspan=3>15 min</td>
      <td>November 20, 2018, 16:00 - 16:05</td>
      <td>500</td>
      <td>150</td>
      <td>150</td>
   </tr>
   <tr>
      <td>November 20, 2018, 16:05 - 16:10</td>
      <td>500</td>
      <td>148</td>
      <td>150</td>
   </tr>
   <tr>
      <td>November 20, 2018, 16:10 - 16:15</td>
      <td>500</td>
      <td>140</td>
      <td>150</td>
   </tr>
</table>

In all other periods, Tom's requests **were successful and a 200 status code was returned**.

In this case, the overall availability for the service period is as follows:

**(1) Calculate the per-5-minute error rate for the current month**

According to the case details: when Tom's business is normal, the per-5-minute error rate is 0%.

Unavailability event 1: This event occurred on November 15, 2018 and lasted from 10:00 - 10:15. The per-5-minute error rate was: 
- **100 / 100 \* 100% = 100%** from 10:00 - 10:05
- **99 / 100 \* 100% = 99%** from 10:05 - 10:10
- **98 / 100 \* 100% = 98%** from 10:10 - 10:15

Unavailability event 2: This event occurred on November 20, 2018 and lasted from 16:00 - 16:15. The 5-minute error rate was:
- **150 / 150 \* 100% = 100%** from 16:00 - 16:05
- **148 / 150 \* 100% = 98.67%** from 16:05 - 16:10
- **140 / 150 \* 100% = 93.33%** from 16:10 - 16:15

**(2) Calculate the service availability for the current month**

In this case:

- Total duration of the service period: 30 days \* 24 hours/day \* 60 minutes/hour=43,200 minutes.
- Total number of 5-minute periods: 43,200 minutes / 5 minutes = 8,640.
- Total number of unavailable 5-minute periods: (15 + 15) minutes / 5 minutes = 6.
- Sum of the per-5-minute error rates: (100% + 99% + 98% + 100% + 98.67% + 93.33%) + (8640 - 6) \* 0% = 589%

The service availability for this month: **(1 - 589% / 8640) \* 100% = 99.93%**

**(3) Calculate relevant compensation**

In this example, the service availability is 99.93%, which is lower than the standard 99.95% but higher than 99.9%. According to compensation standards, Tom is eligible for compensation equivalent to 20% of the total monthly service fees, i.e., 20 USD.
Tom only needs to submit a ticket to apply for compensation within sixty (60) calendar days after the end of the service period, i.e., prior to January 29, 2019, and Tencent Cloud will compensate Tom for his losses by issuing a voucher.

### How do I disable and/or stop being billed for COS services?


There is no one-click option for disabling COS. If there are long periods of time in which you do not use COS, you can save storage costs by transitioning your data to the ARCHIVE storage class. For more information on the transition operation, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).

If you decide to stop using COS, you can avoid any further billing by permanently deleting all of your COS data (including incomplete multipart uploads and object versions). There is no need to de-register your account, and if you use other Tencent Cloud products, please avoid doing so as it will affect your other services.

>?To delete your COS data and incomplete multipart uploads, see [Deleting Objects](https://intl.cloud.tencent.com/document/product/436/13323), and [Deleting Incomplete Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/31632).

Before the you complete the deletion process, please note the following:

- Data, once deleted from COS, cannot be recovered, so please make backups accordingly.
- Check your billing cycle to avoid overdue payment in your account. For more information, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).
- If your account has overdue payment (i.e., your account balance is below 0), COS services will be suspended after 24 hours, regardless of whether your storage pack is within the effective period.
- If your account has overdue payment and COS services are suspended, the free tier for which your account is eligible won’t be available.
