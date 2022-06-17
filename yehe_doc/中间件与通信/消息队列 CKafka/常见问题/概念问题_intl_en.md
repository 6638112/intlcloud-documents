### Which version of open-source Kafka is compatible with CKafka?
Currently, CKafka is fully compatible with open-source Kafka API 0.9, 0.10, 1.1, 2.4, and 2.8, allowing users to migrate data to the cloud at zero cost.

### Which version of open-source Kafka is the current CKafka based on?
The current CKafka is based on Apache Kafka 0.10, 1.1, 2.4, and 2.8. We recommend you use the SDK of the corresponding version for production and consumption.

### Does CKafka expose ZooKeeper?
CKafka does not expose ZooKeeper or its address.

### Does CKafka support public network access?
Currently, CKafka transfers data over the private network by default. As public network access runs the risk of issues such as delay and network environment security, we do not recommend long-term use of public network transfer.
If you have a temporary need for public network transfer, please contact your Tencent Cloud account manager for evaluation and assistance.

### Does CKafka support message compression?
Currently, CKafka supports open-source Snappy and LZ4 message compression formats. Because gzip compression consumes more CPU resources, it is currently not supported.
We recommend you disable message compression when testing.
Configuration Method: in the configuration file of the producer, set the `compression.type` parameter to `snappy` or `lz4`. The default value is `none`, indicating that the feature is disabled.


### Can a Kafka client directly connect to the CKafka service?
CKafka is compatible with open-source Kafka 0.9, 0.10, 1.1, 2.4, and 2.8. You can connect to the message center via a Kafka client and deploy codes to Tencent Cloud services to produce or consume messages.

### What are the restrictions on a CKafka instance?
Different instance specifications have different restrictions on peak throughput, disk capacity, number of topics at the instance level, and number of partitions at the instance level. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).




### Will CKafka lose messages?
- Open-source Apache Kafka does not guarantee no message loss. As CKafka is optimized for availability, Tencent Cloud promises a CKafka availability of over 99.95%.
- CKafka users can enable ACK during production to avoid message loss and improve message reliability.
- Cluster changes and upgrades complete in seconds and will not affect user experience.
- CKafka is mainly used in big data processing scenarios that require high throughput and high performance but relatively low data reliability. In extreme cases, a small number of messages may be lost. If you require zero message loss and have relatively performance requirements, we recommend TDMQ.


### How does CKafka guarantee security?
CKafka guarantees security by using following features:
- Tenant isolation: the network access of instances is isolated among different accounts by default.
- Permission control: CKafka adds an additional authentication mechanism based on the source IP allowlist at the application layer and supports [SASL authentication](https://intl.cloud.tencent.com/document/product/597/39084).
- Security protection: services such as multi-dimensional security protection and anti-DDoS attacks are provided.


