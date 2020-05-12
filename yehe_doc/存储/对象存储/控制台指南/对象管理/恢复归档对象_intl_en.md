## Overview
You can restore archived objects in the COS Console for further access and operations. For more information about object storage classes, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925).

>The restoration operation will create a copy of the object in standard storage class, which can be read and downloaded. The object copy will be billed as a standard storage object. For pricing details, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket name to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b270a42c40ed049811168072818fba1e.png)
3. Click **File List**, select a single object or multiple objects you want to restore, and click **Restore** under **More Actions**.
![](https://main.qcloudimg.com/raw/2d34eaee99c4bcb469025f857ed983f1.png)
4. In the **Restore Archived Objects** pop-up window, configure the restoration mode and the validity period in days of the copy. The related configuration items are detailed below.
	- **Recovery Mode**: Standard, Expedited, or Batch.
 - Expedited mode: This is the fastest mode. Files below 256 MB can be restored in 1 to 5 minutes. When you need to access the archival data urgently, using this mode can greatly reduce the time required.
 - Standard mode: Restoration can be completed generally in 3 to 5 hours.
 - Batch mode: If your need for the archival data is not urgent, this mode can help retrieve massive amounts of data generally in 5 to 12 hours with the lowest cost.
	- **Validity**: set the number of days after which the copy would automatically expire and be deleted. The value range is 1 to 365 days. After the object is successfully restored, you can click **Restore** again to change the validity period of the copy in the pop-up window.
 See the figure below:
![](https://main.qcloudimg.com/raw/3d3163c09213423aa959b179237ab137.png)
5. Click **OK** after configuration, and the object restoration will start. You can click **Details** to enter the object details page and check whether the restoration has been completed.
![](https://main.qcloudimg.com/raw/4686bc71f95d7178a8690f3eb49721e6.png)
6. After confirming that the object has been successfully restored, you can click **Restore** again to modify the validity period of its copy.
![](https://main.qcloudimg.com/raw/e794f58d2593df1ecb675fc7ffa5019c.png)
7. Enter the object details page where you can access, download, and do more with the object.
![](https://main.qcloudimg.com/raw/c464c9fa3e83213f7cf8692f32fa72ab.png)
