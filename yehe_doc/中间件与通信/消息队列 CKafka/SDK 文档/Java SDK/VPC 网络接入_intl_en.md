## Overview

This document describes how to access CKafka to receive/send messages with the SDK for Java in a VPC.

## Prerequisites

- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo/VPC)

## Directions

### Step 1. Prepare configurations

1. Upload the `javakafkademo` in the downloaded demo to the Linux server.
2. Log in to the Linux server, enter the `javakafkademo` directory, and configure related parameters.
    1. Add the following dependencies to the `pom.xml` file: 
    <dx-codeblock>
    :::  xml
      <dependency>
          <groupId>org.apache.kafka</groupId>
          <artifactId>kafka-clients</artifactId>
          <version>0.10.2.2</version>
      </dependency>
    :::
    </dx-codeblock>
   2. Create a Kafka configuration file named `kafka.properties`.
    <dx-codeblock>
    :::  bash
      ## Configure the accessed network by copying the information in the **Network** column in the **Access Mode** section on the instance details** page in the console
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
    <tbody>
    <tr>
        <td>bootstrap.servers</td>
        <td>Accessed network, which can be copied in the **Network** column in the <strong>Access Mode</strong> section on the instance details page in the console.<br><img
                src="https://main.qcloudimg.com/raw/6b12eca18662d26a334d55b743c825ef.png" referrerpolicy="no-referrer">
        </td>
    </tr>
    <tr>
        <td>topic</td>
        <td>Topic name, which can be copied from the <strong>Topic Management</strong> page in the console.<br><img
                src="https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png" referrerpolicy="no-referrer">
        </td>
    </tr>
    <tr>
        <td>group.id</td>
        <td>You can customize it. After the demo runs successfully, you can see the consumer on the <strong>Consumer Group</strong> page.</td>
    </tr>
    </tbody>
</table>
3. Create a configuration file loading program named `CKafkaConfigurer.java`. 
<dx-codeblock>
:::  java
      public class CKafkaConfigurer {
   
          private static Properties properties;
          
          public synchronized static Properties getCKafkaProperties() {
              if (null != properties) {
                  return properties;
              }
              //Obtain the content of the configuration file `kafka.properties`
              Properties kafkaProperties = new Properties();
              try {
                  kafkaProperties.load(CKafkaProducerDemo.class.getClassLoader().getResourceAsStream("kafka.properties"));
              } catch (Exception e){
                  System.out.println("getCKafkaProperties error");
              }
              properties = kafkaProperties;
              return kafkaProperties;
          }
      }  
:::
</dx-codeblock>


### Step 2. Send messages

1. Write a message production program named `CKafkaProducerDemo.java`.
<dx-codeblock>
:::  java
public class CKafkaProducerDemo {

    public static void main(String args[]) {
        //Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties properties = new Properties();
        //Set the access point. Obtain the access point of the topic via the console.
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        
        //Set the method for serializing Kafka messages. `StringSerializer` is used in this demo.
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        //Set the maximum request wait time
        properties.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
        //Set the number of retries for the client
        properties.put(ProducerConfig.RETRIES_CONFIG, 5);
        //Set the retry interval for the client.
        properties.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
        //Construct a producer object
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
        
        //Construct a Kafka message
        String topic = kafkaProperties.getProperty("topic"); //Topic of the message. Enter the topic you created in the console.
        String value = "this is ckafka msg value"; //Message content.
        
        try {
            //Batch obtaining future objects can speed up the process, but the batch size should not be too large.
            List<Future<RecordMetadata>> futureList = new ArrayList<>(128);
            for (int i = 0; i < 10; i++) {
                //Send the message and obtain a future object
                ProducerRecord<String, String> kafkaMsg = new ProducerRecord<>(topic,
                        value + ": " + i);
                Future<RecordMetadata> metadataFuture = producer.send(kafkaMsg);
                futureList.add(metadataFuture);
        
            }
            producer.flush();
            for (Future<RecordMetadata> future : futureList) {
                //Sync the future object obtained
                RecordMetadata recordMetadata = future.get();
                System.out.println("produce send ok: " + recordMetadata.toString());
            }
        } catch (Exception e){
            //If the sending still fails after client internal retries, the system needs to report and handle the error
            System.out.println("error occurred");
        }
    }
}
:::
</dx-codeblock>
2. Compile and run `CKafkaProducerDemo.java` to send the message.
3. View the execution result.
<dx-codeblock>
:::  bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
:::
</dx-codeblock>
4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.intl.cloud.tencent.com/ckafka), select the topic, and click **More** > **Message Query** to view the message just sent.
    ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)


### Step 3. Consume messages

1. Create a program named `CKafkaConsumerDemo.java` for a consumer to subscribe to messages.
<dx-codeblock>
:::  java
public class CKafkaConsumerDemo {

    public static void main(String args[]) {
        //Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties props = new Properties();
        //Set the access point. Obtain the access point of the topic via the console.
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        //Set the maximum interval between two polls
        //If the consumer does not return a heartbeat message within the interval, the broker will determine that the consumer is not alive, and then remove the consumer from the consumer group and trigger rebalancing. The default value is 30s.
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        //Set the maximum number of messages that can be polled at a time
        //Do not set this parameter to an excessively large value. If polled messages are not consumed before the next poll, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        //Set the method for deserializing messages
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        //The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        //Create a consumer object, which means generating a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        //Set one or more topics to which the consumer group subscribes
        //You are advised to configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics = new ArrayList<>();
        //If you want to subscribe to multiple topics, add the topics here
        //You must create the topics in the console in advance.
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic : topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);
        
        //Consume messages in loop
        while (true) {
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                //All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
                //You are advised to create a separate thread to consume messages and then return the result in async mode
                for (ConsumerRecord<String, String> record : records) {
                    System.out.println(
                            String.format("Consume partition:%d offset:%d", record.partition(), record.offset()));
                }
            } catch (Exception e){
                System.out.println("consumer error!");
            }
        }
    }
}
:::
</dx-codeblock>
2. Compile and run `CKafkaConsumerDemo.java` to consume messages.
3. View the execution result.
<dx-codeblock>
:::  bash
Consume partition:0 offset:298
Consume partition:0 offset:299
:::
</dx-codeblock>
4. On the **Consumer Group** tab page in the [CKafka console](https://console.intl.cloud.tencent.com/ckafka), select the consumer group name, enter the topic name, and click **View Details** to view the consumption details.
    ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
