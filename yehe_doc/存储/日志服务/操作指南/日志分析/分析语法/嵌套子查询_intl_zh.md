本文介绍嵌套子查询的语法使用与操作示例。

>? 当前日志服务已支持大部分地域使用 CLS 函数。上海、广州地域部分用户暂未开通，如有需要，请联系 [在线客服](https://intl.cloud.tencent.com/contact-sales

## 操作场景

针对一些复杂的查询场景，一层 SQL 无法满足需求，通过 SQL 嵌套查询可以满足复杂的需求。

嵌套子查询和无嵌套查询的区别在于，要在 SQL 中指定 from 条件。在查询中要指定 from log 这个关键字，表示从日志中读取原始数据。


## 操作示例

```
* | select sum(status) from 
(
select status, count(1) as pv from log group by status limit 2000
)
```

