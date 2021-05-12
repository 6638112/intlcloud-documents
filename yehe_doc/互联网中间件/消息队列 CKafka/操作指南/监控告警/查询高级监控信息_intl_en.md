CKafka Pro Edition supports advanced monitoring. You can view metrics such as core services, production, consumption, and broker GC in the console, making it easier for you to troubleshoot CKafka issues.

This document describes how to view advanced monitoring metrics in the console and explains their meanings.

## Descriptions of Monitoring Metrics

### Core service monitoring

| Monitoring Metric     | Description                                                     | Normal Range                                                   |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Network busyness | This value is used to measure the current remaining I/O resources for concurrent request processing. The closer to 1 it is, the idler the instance is.    | This value generally fluctuates between 0.5 and 1. If it is below 0.3, the load is high.               |
| Request queue depth | This value indicates the number of production requests that have not been processed. If this value is too large, it may be because that the number of concurrent requests is high, the CPU load is high, or the disk I/O hits a bottleneck. | If this value stays at 2000, the cluster load is high; if it is below 2000, it can be ignored.   |
| Number of unsynced replicas | This value indicates the number of unsynced replicas in the cluster. When there are unsynced replicas of an instance, there may be a health problem with the cluster. | If this value stays above 5 (this is because that some built-in topic partitions of Tencent Cloud may be offline and has nothing to do with the business), the cluster needs to be fixed. In case that the broker occasionally fluctuates, this value may surge and then become stable, which is normal. |
| Number of ZK reconnections   | This value indicates the number of reconnections of the persistent connection between the broker and ZooKeeper. Network fluctuations and high cluster loads may cause disconnections and reconnections, thus leading to leader switching. | There is no normal range for this metric. The number of ZK reconnections is cumulative, so a large number does not necessarily mean that there is a problem with the cluster. This metric is for reference only. |
| Number of ISR expansions  | This value is the number of Kafka ISR expansions. It will increase by 1 when an unsynced replica catches up with the data from the leader and rejoins the ISR. | There is no normal range for this metric. Expansions occur when the cluster fluctuates. No attention is required unless this value stays above 0. |
| Number of ISR shrinks  | This value is the number of Kafka ISR shrinks. It is counted when the broker is down and ZooKeeper reconnects. | There is no normal range for this metric. Shrinks occur when the cluster fluctuates. No attention is required unless this value stays above 0. |

### Production monitoring

| Monitoring Metric     | Description                                                     | Normal Range                                                   |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Total production duration  | This value indicates the total duration of a production request, which is based on metrics such as the request queue duration, local processing duration, and delayed response duration. <br/>At each point in time, the total duration is not equal to the sum of the following five metrics, because each metric is averaged. | This value generally ranges between 0 and 100 ms. A value of 0–1000 ms is normal when the data volume is high. No action is required unless this value stays above 1000 ms. |
| Request queue duration | This value indicates the amount of time a production request waits in the queue of requests to be received. It means that the request packet waits for subsequent processing. | This value generally ranges between 0 and 50 ms. A value of 0–200 ms is normal when the data volume is high. No action is required unless this value stays above 200 ms. |
| Local processing duration | This value indicates the amount of time a production request is processed by the leader broker, i.e., the duration between the request packet is obtained from the request queue and it is written to the local page cache. | This value generally ranges between 0 and 50 ms. A value of 0–200 ms is normal when the data volume is high. No action is required unless this value stays above 200 ms. |
| ack wait duration | This value indicates the amount of time a production request waits for data to be synced. It is greater than 0 only when the client ack is -1; in other words, it is 0 as long as ack is 1 or 0. | This value generally ranges between 0 and 200 ms. A value of 0–500 ms is normal when the data volume is high. No action is required unless this value stays above 500 ms. This value for a multi-AZ instance is greater than that for a single-AZ instance when ack is -1. For more information, please see [Multi-AZ Deployment](https://cloud.tencent.com/document/product/597/52786). |
| Delayed response duration | This value indicates the amount of time it takes the system to delay returning a packet to a production request. This value will always be 0 as long as the traffic of the instance does not exceed the purchased traffic, and it will be greater than 0 if the traffic is throttled. | This value will be 0 as long as the instance does not exceed the limit. If the limit is exceeded, there will be a delay of 0–5 minutes proportional to the excess; in other words, the maximum value is 5 minutes. |
| Response queue duration | This value indicates the amount of time a production request waits in the response queue. It means that the request packet waits to be sent to the client. | This value generally ranges between 0 and 50 ms. A value of 0–200 ms is normal when the data volume is high. No action is required unless this value stays above 200 ms. |

### Consumption monitoring

| Monitoring Metric     | Description                                                     | Normal Range                                                   |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Total consumption duration   | This value indicates the total duration of a consumption request, which is based on metrics such as the request queue duration and local processing duration. <br/>At each point in time, the total duration is not equal to the sum of the following five metrics, because each metric is averaged. | This value generally ranges between 500 and 1000 ms (the default `fetch.max.wait.ms` on the client is 500 ms). A value of 500–5000 ms is normal when the data volume is high. |
| Request queue duration | This value indicates the amount of time a consumption request waits in the request queue. It means that the request packet waits for subsequent processing. | This value generally ranges between 0 and 50 ms. A value of 0–200 ms is normal when the data volume is high. No action is required unless this value stays above 200 ms. |
| Local processing time | This value indicates the amount of time it takes a consumption request to pull data from the leader broker, i.e., reading data from the local disk. | This value generally ranges between 0 and 500 ms. A value of 0–1000 ms is normal when the data volume is high. No action is required unless the value stays above 1000 ms, because the consumer sometimes may read cold data, which will consume a lot of time. |
| Consumption wait duration | The default `fetch.max.wait.ms` on the client is 500 ms. This value indicates the amount of time the client allows the server to wait before returning any packet to the client when the client cannot read any data. | This value is generally around 500 ms (the default `fetch.max.wait.ms` on the client is 500 ms), subject to the client's parameter settings. |
| Delayed response duration | This value indicates the amount of time it takes the system to delay returning a packet to a consumption request. This value will always be 0 as long as the traffic of the instance does not exceed the purchased traffic, and it will be greater than 0 if the traffic is throttled. | This value will be 0 as long as the instance does not exceed the limit. If the limit is exceeded, there will be a delay of 0–5 minutes proportional to the excess; in other words, the maximum value is 5 minutes. |
| Response queue duration | This value indicates the amount of time a consumption request waits in the response queue. It means that the request packet waits to be sent to the client. | This value generally ranges between 0 and 50 ms. A value of 0–200 ms is normal when the data volume is high. No action is required unless this value stays above 200 ms. |

### Broker GC monitoring

| Monitoring Metric       | Description             | Normal Range                                           |
| -------------- | -------------------- | ---------------------------------------------------- |
| Young GC count | Young GC count of the broker | This value generally ranges between 0 and 300. If it stays above 300, the GC parameters need to be adjusted. |
| Full GC count | Full GC count of the broker | This value is generally 0, and actions are required if it is greater than 0.         |

## Viewing Monitoring Data

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the instance list, click the **ID/Name** of the target instance to enter the instance details page.
3. At the top of the instance details page, click **Monitoring** > **Advanced Monitoring**, select the metric to be viewed, and set the time range to view the monitoring data.
