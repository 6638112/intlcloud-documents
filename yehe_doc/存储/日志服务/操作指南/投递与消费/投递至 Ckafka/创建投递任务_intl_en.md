## Overview

You can ship log topic data to CKafka for real-time stream computing and storage. If you haven't purchased a CKafka instance, you can consider using the [consumption over Kafka feature](https://intl.cloud.tencent.com/document/product/614/42752) that comes with CLS. These two options have the same price.

## Prerequisites

- You have activated CKafka.
- Make sure that the current account has the permission to enable shipping to CKafka. If your account is a sub-account, it needs to be authorized by the root account first. For more information, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).


## Directions

1. Create a CKafka instance in the same region as the log topic. For more information, see [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718).
2. In the same region, configure the following parameters to create a topic. For more information, see Creating Topic.

 - **Preset ACL Policy**: Disable the preset ACL policy.
 - **Show advanced configuration**:
    - **CleanUp.policy**: Select **delete**; otherwise, shipping will fail.
    - **max.message.bytes**: Set this value to 8 MB or above. If the value is below 8 MB, when the size of a single message in CLS exceeds the specified limit, the message cannot be written to the CKafka topic, and shipping will fail.
3. Go to the [CLS console](https://console.cloud.tencent.com/cls) and enter the shipping task management page or log topic management page as needed.
 - On the left sidebar, click **Shipping Task Management** and select a region, logset, and log topic.

 - On the left sidebar, click **Log Topic** and select a log topic to be shipped to CKafka to enter the log topic management page.

4. Click the **Ship to Ckafka** tab.
5. Click **Edit* on the right to enable shipping to CKafka. Then, select the target CKafka instance and topic as well as the log field to be shipped.

6. Click **OK** to start shipping to CKafka. If the task status is **Enabled**, the feature is enabled successfully.
>! To cleanse the log data before shipping to CKafka, see [Log Filtering and Distribution](https://intl.cloud.tencent.com/document/product/614/46135).
>

## FAQs

#### What should I do if the log data cannot be shipped to CKafka?

If ACL authentication is enabled in CKafka, the log data cannot be shipped. In this case, you need to disable the ACL of the topic.

#### What should I do if the system prompts that I have no permissions to read/write the CKafka topic?

If you directly use an API to ship data to CKafka, you may not have the read/write permissions of the CKafka topic. If you ship data in the console, the system will guide you through the authorization process, but if you directly call an API for shipping, you need to authorize manually. For more information, see [Viewing and Configuring Shipping Permissions](https://intl.cloud.tencent.com/document/product/614/46142).

