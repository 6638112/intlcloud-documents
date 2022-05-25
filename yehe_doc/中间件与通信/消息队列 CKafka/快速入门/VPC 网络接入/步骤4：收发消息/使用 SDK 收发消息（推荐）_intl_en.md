## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Java in a VPC.

If you need to use SDKs for other languages, see [SDK Documentation](https://intl.cloud.tencent.com/document/product/597/40049).

## Prerequisites

- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo.](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo)

## Directions

### Step 1. Prepare configurations

1. Upload the downloaded demo to the Linux server under the same VPC, log in to the server, and enter the VPC directory under `javakafkademo`.
2. Modify `kafka.properties` in the `resources` directory under the VPC project.
<dx-codeblock>
:::  bash
## Configure the accessed network by copying the information in the **Network** column in the **Access Mode** section on the instance details page in the console
bootstrap.servers=xx.xx.xx.xx:xxxx
## Configure the topic by copying the information on the **Topic Management** page in the console
topic=XXX
## Configure the consumer group as needed
group.id=XXX
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>bootstrap.servers</td>
<td>Accessed network, which can be copied in the **Network** column in the <strong>Access Mode</strong> section on the instance details page in the console.<br><img src="https://main.qcloudimg.com/raw/6b12eca18662d26a334d55b743c825ef.png" alt=""></td>
</tr>
<tr>
<td>topic</td>
<td>Topic name, which can be copied from the <strong>Topic Management</strong> page in the console.<br><img src="https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png" alt=""></td>
</tr>
<tr>
<td>group.id</td>
<td>You can customize it. After the demo runs successfully, you can see the consumer group on the <strong>Consumer Group</strong> page.</td>
</tr>
</tbody></table>

### Step 2. Send a message

1. Compile and run the message producing program `CKafkaProducerDemo.java`.
<dx-codeblock>
:::  java
public class CKafkaProducerDemo {

    public static void main(String args[]) {
        // Load `kafka.properties`.
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties properties = new Properties();
        // Set the access point. Get the access point of the corresponding topic in the console.
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        
        // Set the method for serializing Kafka messages. `StringSerializer` is used in this demo.
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        // Set the maximum request wait time.
        properties.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
        // Set the number of retries for the client.
        properties.put(ProducerConfig.RETRIES_CONFIG, 5);
        // Set the internal retry interval for the client.
        properties.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
        // Construct a producer object.
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
        
        // Construct a CKafka message.
        String topic = kafkaProperties.getProperty("topic"); // Topic of the message. Enter the topic you created in the console
        String value = "this is ckafka msg value"; // Message content
        
        try {
            // Batch getting future objects can speed up the process. Note that the batch size should not be too large.
            List<Future<RecordMetadata>> futureList = new ArrayList<>(128);
            for (int i = 0; i < 10; i++) {
                // Send the message and get a future object.
                ProducerRecord<String, String> kafkaMsg = new ProducerRecord<>(topic,
                        value + ": " + i);
                Future<RecordMetadata> metadataFuture = producer.send(kafkaMsg);
                futureList.add(metadataFuture);
        
            }
            producer.flush();
            for (Future<RecordMetadata> future : futureList) {
                // Sync the future object obtained.
                RecordMetadata recordMetadata = future.get();
                System.out.println("produce send ok: " + recordMetadata.toString());
            }
        } catch (Exception e) {
            // If the sending still fails after client internal retries, the system needs to report and handle the error.
            System.out.println("error occurred");
        }
    }
}
:::
</dx-codeblock>
2. View the execution result.
<dx-codeblock>
:::  bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
:::
</dx-codeblock>
3. On the **Topic Management** tab on the instance details page in the [CKafka console](https://console.intl.cloud.tencent.com/ckafka), select the target topic, and click **More** > **Message Query** to view the message just sent.
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)


### Step 3. Consume messages

1. Compile and run the message subscribing program `CKafkaConsumerDemo.java`.
<dx-codeblock>
:::  java
public class CKafkaConsumerDemo {

    public static void main(String args[]) {
        // Load `kafka.properties`.
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties props = new Properties();
        // Set the access point. Get the access point of the corresponding topic in the console.
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        // Set the maximum interval between two polls.
        // If the consumer does not return a heartbeat message within the interval, the broker will determine that the consumer is not alive, and then remove the consumer from the consumer group and trigger rebalancing. The default value is 30s.
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        // Set the maximum number of messages that can be polled at a time.
        // Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        // Set the method for deserializing messages.
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        // The instances in the same consumer group consume messages in load balancing mode.
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        // Construct a consumer object. This generates a consumer instance.
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        // Set one or more topics to which the consumer group subscribes.
        // We recommend you configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics.
        List<String> subscribedTopics = new ArrayList<>();
        // If you want to subscribe to multiple topics, add the topics here.
        // You must create the topics in the console in advance.
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic : topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);
        
        // Consume messages in loop.
        while (true) {
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                // All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`.
                // We recommend you create an independent thread to consume messages and then return the result in async mode.
                for (ConsumerRecord<String, String> record : records) {
                    System.out.println(
                            String.format("Consume partition:%d offset:%d", record.partition(), record.offset()));
                }
            } catch (Exception e) {
                System.out.println("consumer error!");
            }
        }
    }
}
:::
</dx-codeblock>
2. View the execution result.
<dx-codeblock>
:::  bash
Consume partition:0 offset:298
Consume partition:0 offset:299
:::
</dx-codeblock>
3. On the **Consumer Group** tab in the [CKafka console](https://console.intl.cloud.tencent.com/ckafka), select the consumer group name, enter the topic name, and click **View Details** to view the consumption details.
 ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
