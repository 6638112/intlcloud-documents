<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued on May 16, 2022,see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

## Overview

This document describes how to configure aggregation rules to improve query efficiency when dealing with complex query scenarios.

## Prerequisites

Before configuring aggregation rules, you need to perform the following operations:
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a self-deployed cluster.
- You have [created a TPS instance](https://intl.cloud.tencent.com/document/product/457/38824) in the VPC of the cluster.

## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** on the left sidebar.
2. On the instance list page, select an instance name that needs to create aggregation rules to go to its details page.
3. On **Aggregation Rule** page, click **Create Aggregation Rule** as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/1fabc033622083e6140e224fa3acf291.png)
4. In the pop up **Add Aggregation Rule** window, edit the aggregation rule as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/34b1c50a61924380a46752cbea9f0b18.png)
6. Click **OK**.
