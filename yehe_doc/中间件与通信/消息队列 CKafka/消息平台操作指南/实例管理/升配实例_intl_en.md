## Overview

If the current instance specifications cannot meet your business needs, you can upgrade them in the console.

> ? The instance specifications you can upgrade include peak bandwidth, disk capacity, and the number of topics/partitions. You can also increase the disk capacity only. The upgrade is smooth without suspending your services.

## Prerequisites

Check the following items before upgrading:

1. Check whether the instance has unavailable public network routes, supporting networks, VPC networks, etc. For more information, see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
2. Check whether the instance has unsynced replicas. For more information, see [Topic Management](https://intl.cloud.tencent.com/document/product/597/47583).
3. Check whether the instance has unfinished tasks (data migration), abnormally created topics, abnormally deleted topic data, etc.
If there are unfinished tasks, we recommend you wait for all the tasks to be completed before upgrading. If task execution is abnormal, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.

## Directions

<dx-tabs>
::: Scenario 1: Upgrading Standard Edition instance specification
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Operation** column on the instance list page, select **More** > **Upgrade** to enter the upgrade page.
3. Select the target specification for the instance.
4. Click **Submit** to complete the instance upgrade.
:::
::: Scenario 2: Upgrading from Standard Edition to Pro Edition
Due to architecture optimizations, the advanced specification of Standard Edition was deactivated on September 9, 2021. You can smoothly upgrade Standard Edition instances purchased afterwards to Pro Edition in the console.
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Operation** column on the instance list page, select **More** > **Upgrade** to enter the upgrade page.
3. Select **Pro Edition** as the target specification type.
   - Product Specification: Select a model based on the peak bandwidth and disk capacity.
   - Instance Price: You need to pay for the upgrade based on the number of days.
   - Rebalance Time:
     - If the backend detects that data migration is required during the upgrade, you can choose to upgrade right away or at specified time (upgrade at night is recommended to reduce the impact on your business). The estimated upgrade duration is calculated by backend APIs.
     - If the backend detects that data migration is not required during the upgrade, you will see the message "Rebalancing will not occur during the upgrade".
   - Upgrade Mode: If the backend detects that instance migration is required during the upgrade, you can select an upgrade mode as needed. Otherwise, you do not need to select one.
     - Stable: CKafka will limit the speed of data migration during the upgrade to ensure that instances have optimal bandwidth performance. This option is recommended if you don't want to affect business operations.
     - High-speed: CKafka will not limit the speed of data migration during the upgrade, thus affecting the bandwidth available for data production and consumption of instances. This option is recommended for off-peak hours or when service suspension is allowed.
4. Click **Submit** to complete the instance upgrade. You can view the upgrade progress in the **Status** column.
5. If you choose to upgrade at the specified time, you can modify the time you specified in the **Status** column.
   :::
   ::: Scenario 3: Upgrading Pro Edition instance specification
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Operation** column on the instance list page, select **More** > **Upgrade** to enter the upgrade page.
3. Select the target specification for the instance.
- Product Specification: Select a model based on the peak bandwidth and disk capacity.
- Instance Price: You need to pay for the upgrade based on the number of days.
- Rebalance Time:
  - If the backend detects that data migration is required during the upgrade, you can choose to upgrade right away or at specified time (upgrade at night is recommended to reduce the impact on your business). The estimated upgrade duration is calculated by backend APIs.
  - If the backend detects that data migration is not required during the upgrade, you will see the message "Rebalancing will not occur during the upgrade".
- Upgrade Mode: If the backend detects that instance migration is required during the upgrade, you can select an upgrade mode as needed. Otherwise, you do not need to select an upgrade mode.
  - Stable: CKafka will limit the speed of data migration during the upgrade to ensure that instances have optimal bandwidth performance. This option is recommended if you don't want to affect business operations.
  - High-speed: CKafka will not limit the speed of data migration during the upgrade, thus affecting the bandwidth available for data production and consumption of instances. This option is recommended for off-peak hours or when service suspension is allowed.
4. Click **Submit** to complete the instance upgrade. You can view the upgrade progress in the **Status** column.
5. If you choose to upgrade at the specified time, you can modify the time you specified in the **Status** column.
   :::
   </dx-tabs>

## Possible Causes of Upgrade Failures

1. The disk resources in the current AZ cannot meet the requirements of this upgrade. We recommend you contact the Tencent Cloud customer service to check whether there are sufficient resources.
2. If the high-speed mode is selected during instance upgrade, and there are production tasks that use a lot of bandwidth resources in the cluster, the data migration delay will increase. You can view the [monitoring data](https://intl.cloud.tencent.com/document/product/597/12167) to see whether there are excessive peaks of the production and consumption traffic during the upgrade.
3. The upgrade process takes too long. The maximum acceptable message byte size of the migrated server configuration is 1 MB, but the broker configuration that needs to be migrated is 8 MB, so the broker cannot receive oversized message migration, resulting in prolonged data migration. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
4. During the upgrade or migration between the new and old clusters, the broker IP update is abnormal, causing the broker IP of the new cluster to fail to pull data. You can view the [monitoring data](https://intl.cloud.tencent.com/document/product/597/12167) to see that there is no monitoring data for a period of time. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
