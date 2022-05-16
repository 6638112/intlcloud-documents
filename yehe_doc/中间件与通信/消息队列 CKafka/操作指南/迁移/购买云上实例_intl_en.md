## Overview

This document describes how to use the **Specification Calculator** in the CKafka console to find the appropriate CKafka instance specification for your self-built Kafka cluster that needs to be migrated to the cloud.

## Directions
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the left sidebar, select **Migration to Cloud**, select the region you want to migrate to, and click **Specification Calculator**.
3. Enter the specification of your self-built Kafka cluster on the specification calculator page.
	 ![](https://main.qcloudimg.com/raw/15b721ef605d238f01f888b6a54a334e.png)

   | Parameter         | Description                                                         |
   | ------------ | ------------------------------------------------------------ |
   | Kafka Version | Select the version of your self-built Kafka cluster. For more information on CKafka version selection, please see [Suggestions for CKafka Version Selection](https://intl.cloud.tencent.com/document/product/597/40964). |
   | Peak Business Bandwidth | Peak business bandwidth = max (production peak bandwidth * number of replicas, consumption peak bandwidth). |
   | Disk | Estimate according to the current peak value of actual disk usage. |
   | Total Partitions | Total number of partitions of the topic to be migrated. The number of replicas should be considered. For example, if one topic replica has 5 partitions, then two replicas have 10 partitions in total. CKafka does not support single-replica topics. |
   | Multi-AZ Deployment | Select whether to deploy in multiple AZs according to your business needs. For more information, see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243). |
   | Data Compression | CKafka does not support the Gzip compression format. For more information, see [Data Compression](https://intl.cloud.tencent.com/document/product/597/34004). |

4. Click **Next** to get the recommended CKafka instance specification.
5. Click **Buy Now** to redirect to the instance purchase page.
6. Confirm the purchase information, click **Buy Now**, wait 5–10 minutes, and you can see that the instance is created on the instance list page.
	 ![](https://main.qcloudimg.com/raw/30fd507fc0be892eb5467c8ff83723a1.png)
