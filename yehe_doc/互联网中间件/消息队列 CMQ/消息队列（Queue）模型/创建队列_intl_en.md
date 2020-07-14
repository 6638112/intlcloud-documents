On the **CMQ** > **Queue Service** > **[Queue](https://console.cloud.tencent.com/mq/index?rid=1)** page, click **Create** in the top-left corner to create a message queue.
You need to specify the following attributes when creating a queue:
<style>
table th:first-of-type {  
    width: 200px;
}
</style>
| Attribute | Description | Value |
|---------|---------|---------|
| Queue name | `QueueName`, which is the name of queue. | It is a unique identifier of a resource and is used to specify a queue when APIs are called for operations. It cannot be modified after the queue is created. To avoid confusion, queues that have the same name in the same letter case cannot be created. When entering the name, pay attention to the letter case. |
| Long-polling waiting time for message receipt | `PollingWaitSeconds`, which is the long-polling waiting time. Just like with long polling of Ajax requests, a message consumption request will return a response only after a valid message is fetched or the long-polling time elapses. | It is measured in seconds and ranges from 200 milliseconds to 30 seconds. The default value is 200 milliseconds. |
| Hidden duration of fetched messages | `VisibilityTimeout` attribute of queue. Each message has a default `VisibilityTImeout`, which starts counting after a worker receives the message. If the worker fails to complete processing the message within the period specified by this attribute, the message will be sent to and processed by another worker. | It is measured in seconds and ranges from 1 second to 43,200 seconds (12 hours). The default value is 30 seconds. |
| Maximum message size | `MaxMsgSize` attribute of queue. It specifies the maximum length of the message body that can be sent to the queue. | It is measured in bytes and ranges from 1,024 to 65,536 bytes (i.e., 1–64 KB). The default value is 64 KB. |
| Message lifecycle | `msgRetentionSeconds` attribute of queue. It specifies the maximum period of time during which a message can be retained in the queue. After the period specified by this parameter has elapsed since a message is sent to the queue, the message will be deleted no matter whether it has been fetched. | It is measured in seconds and ranges from 60 to 1,296,000 seconds (i.e., 1 minute to 15 days). |
| Maximum retained messages | It specifies the maximum number of retained (undeleted) messages in a queue. | The maximum number of retained messages in a queue is 100 million, and the minimum number is 1 million. If you need to increase the upper limit, please contact technical support. |
| Message rewind | If the "message rewind" feature is not enabled, a message consumed by a consumer and confirmed for deletion will be deleted immediately. When enabling this feature, you need to specify the "rewind time range". | The rewind time range must be equal to or shorter than the message lifecycle. You are recommended to set it to the same as the message lifecycle to facilitate troubleshooting. The unit price of message rewind is 0.01 CNY/million messages/hour. For more information, please see [Message Rewind](https://intl.cloud.tencent.com/document/product/406/8129). |
| Specified time range | You can configure this item after enabling message rewind, which is disabled by default in the console. After it is enabled, the default value will be the same as the message lifecycle value. | It ranges from 1 to 15 days. The maximum rewindable time is the current time minus the configured rewindable time range. The messages cannot be rewound if produced before this time. |



