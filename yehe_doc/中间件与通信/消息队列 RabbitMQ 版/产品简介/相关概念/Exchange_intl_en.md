This document describes the concept, types, and usage of exchange in TDMQ for RabbitMQ. 

## Concept

Exchange acts as an agent for message routing in TDMQ for RabbitMQ. It receives a message sent from a producer and routes the message to one or more queues based on its attributes or content (or discards it), so that the message can be pulled for consumption by a consumer.

TDMQ for RabbitMQ currently supports three types of exchange: direct, fanout, and topic.

- Direct: a direct exchange will route messages to the queue whose binding key exactly matches the routing key.

- Fanout: a fanout exchange will route messages to all queues bound to it.

- Topic: a topic exchange supports multi-condition match and fuzzy match; that is, it will route messages to the queues bound to it by using routing key pattern match and string comparison.

## Direct Exchange

**Routing rule**: a direct exchange will route messages to the queue whose binding key exactly matches the routing key.

**Use case**: this type of exchange is suitable for filtering messages by simple character identifiers and is often used for unicast routing.

**Sample**:

![](https://qcloudimg.tencent-cloud.cn/raw/6a6778594b75bb6df62859c89becb745.svg)

| Message   | Routing Key | Binding Key | Queue   |
| :-------- | :---------- | :---------- | :------ |
| Message 1 | `bizA`      | `bizA`      | Queue 1 |
| Message 2 | `bizB`      | `bizB`      | Queue 2 |

## Fanout Exchange

**Routing rule**: this type of exchange will route messages to all queues bound to it.

**Use case**: this type of exchange is suitable for broadcast message scenarios. For example, a distribution system can use a fanout exchange to broadcast various status and configuration updates.

**Sample**:

![](https://qcloudimg.tencent-cloud.cn/raw/30e985b41f7d9406879f7d4ac6e8aa3a.svg)

| Message   | Routing Key       | Binding Key                 | Queue            |
| :-------- | :---------------- | :-------------------------- | :--------------- |
| Message 1 | `bazA.wechat_pay` | `bazA.credit`, `bazB.credit` | Queue 1, Queue 2 |
| Message 2 | `bazA.alipay`     | `bazA.credit`, `bazB.credit` | Queue 1, Queue 2 |
| Message 3 | `bazC.credit`     | `bazA.credit`, `bazB.credit` | Queue 1, Queue 2 |

## Topic Exchange

**Routing rule**: this type of exchange supports multi-condition match and fuzzy match; that is, it will route messages to the queues bound to it by using routing key pattern match and string comparison.

- The wildcards supported by topic exchanges include asterisk "*" and pound sign "#".

- "*" represents a word, such as `sh`.

- "#" represents zero, one, or more words separated by period ".", such as `cn.hz`.

**Use case**:

This type of exchange is often used for multicast routing. For example, you can use a topic exchange to distribute data about specific geographic locations.

**Sample**:

![](https://qcloudimg.tencent-cloud.cn/raw/8463036d7d681fbe184abe4a310e1162.svg)

| Message   | Routing Key   | Binding Key             | Queue            |
| :-------- | :------------ | :---------------------- | :--------------- |
| Message 1 | `cn.hz`       | `cn.hz.#`               | Queue 1          |
| Message 2 | `cn.hz.store` | `cn.hz.#`, `cn.*.store` | Queue 1, Queue 2 |
| Message 3 | `cn.sz.store` | `cn.*.store`            | Queue 2          |
