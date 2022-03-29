CKafka not only provides a number of monitoring metrics for running CKafka clusters to monitor their health, but also allows you to configure alarms for key metrics, so that you can identify cluster problems and address them in a timely manner. For more information, see [Viewing Monitoring Information](https://intl.cloud.tencent.com/document/product/597/12167) and [Configuring Alarm](https://intl.cloud.tencent.com/document/product/597/40976).

This document describes some metrics that require special attention during your use of CKafka, as well as recommended alarm configurations:


| Metric | Recommended Alarm Configuration | Description |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Disk utilization (%) | The statistical period is 1 minute, and if this value is above 80% in 5 consecutive periods, an alarm will be triggered once every 30 minutes. | The average disk utilization refers to the average of the disk utilization values of all nodes in the cluster. If the disk utilization is too high, the node will not have enough disk space to sustain messages assigned to it, making it unable to store messages. We recommend you clear the data or scale the cluster in time when this value exceeds 75%. |
| Unconsumed messages (count) | The statistical period is 5 minutes, and if this value is above 8,000 in 10 consecutive periods, an alarm will be triggered once every 30 minutes. | Too many retained messages will cause the broker node disk utilization to soar up, so no more messages can be received, and the service will stop. In this case, you should perform scaling. |
| Production peak bandwidth (MB/s) | The statistical period is 1 minute, and if this value is above the purchased bandwidth specification of the instance in 5 consecutive periods, an alarm will be triggered once every 10 minutes. | This refers to the maximum value of traffic per second within one minute. You can determine whether the purchased traffic cap is exceeded and upgrade the specification accordingly. |

