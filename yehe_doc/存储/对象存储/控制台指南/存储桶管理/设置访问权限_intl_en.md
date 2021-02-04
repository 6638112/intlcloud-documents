## Overview

You can use the COS console to set or modify bucket access permissions of the following two types.

- **Public permissions**: include private read/write, public read/private write and public read/write. For more information, see **Types of Permission* under [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
- **User ACLs**: the root account has all bucket permissions (full control) by default. You can add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.

## Granting Permissions for a Single Bucket

**Directions**

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Bucket List**.
2. Locate the bucket for which you want to set or modify access permissions, and then click the bucket name.
3. Select **Permission Management** > **Bucket ACL** and you can set both public permissions and user ACLs for the bucket. For example, you can add a sub-account, whose ID can be viewed in the [CAM Console](https://console.cloud.tencent.com/cam).
   ![](https://main.qcloudimg.com/raw/34e464b33c4b9bffe72c734d1c1dcb2d.png)
4. Click **Save** under **Operation**.

## Granting Permissions for Multiple Buckets

**Directions**

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Bucket List**.
2. Click **Authorize Management** above the bucket list.
![](https://main.qcloudimg.com/raw/9bfbb2948c61a9b3a522d61331d90a51.png)
3. In the pop-up window, select the buckets which you want to grant permissions for. Then, scroll down to set both public permissions and user ACLs. For example, you can add a sub-account, whose ID can be viewed in the [CAM Console](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/23eff9055312eaa122e247f9cf0ebf53.png)
4. Once completed, Click **OK**.
