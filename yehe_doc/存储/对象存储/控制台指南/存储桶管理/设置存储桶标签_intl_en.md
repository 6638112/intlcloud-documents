## Overview

A bucket tag is a key-value pair (key = value), where the tag key and tag value are connected by an equal sign (=), for example, group = IT. It can be used to identify a bucket, helping you achieve group management of buckets. You can set, query, and delete the tag for a specified bucket via the console.


>!
>- Each bucket can have up to 50 different bucket tags.
>- `qcs:` and `project` are reserved fields. Therefore, do not use them in tag keys or tag values. For more limits, please see [Bucket Tag Overview](https://intl.cloud.tencent.com/document/product/436/31509).

## Adding a Tag When Creating a Bucket

You can add a bucket tag when [creating buckets](https://intl.cloud.tencent.com/document/product/436/13309), as shown in the following figure:
![](https://main.qcloudimg.com/raw/3529ae1c392f524209cf899931aa1fef.png)

## Adding a Tag to an Existing Bucket

If you didn’t add a tag when creating a bucket, you can perform the following steps to add a tag for your bucket:

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the desired bucket to enter the bucket configuration page.
2. Click **Basic Configurations** > **Tagging**. Then, click **Add Tags**.
   ![](https://main.qcloudimg.com/raw/300e5b4439c701a5e11ab75e2d85e1bb.png)
3. Enter the tag key and tag value. Then, click **Save**.

