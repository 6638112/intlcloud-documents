## 操作场景

Datahub 提供数据流出能力，您可以将 CKafka 数据分发至 Elasticsearch Service（ES）便于海量数据存储搜索、实时日志分析等操作。
>?只支持7.0以上版本的 Elasticsearch Service。

## 前提条件

该功能目前依赖 Elasticsearch Service 服务，使用时需开通相关产品功能。

## 操作步骤

### 创建数据流出任务

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，选择好地域后，单击**新建任务**。
3. 目标类型选择 **Elasticsearch Service**，单击**下一步**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/da6a3b99adf759d3d5c8726bb6a0e7f5.png)
   - 任务名称：只能包含字母、数字、下划线、"-"、"."。
   - CKafka 实例：选择数据源 CKafka。
   - 源 Topic：选择源 Topic。
   - 源数据：支持拉取源数据。
   - 起始位置：转储时历史消息的处理方式，topic offset 设置。
   - 实例集群：选取腾讯云 Elasticsearch Service 实例集群信息。
   - 实例用户名：输入 Elasticsearch 实例用户名，腾讯云 Elasticsearch 默认用户名为 elastic，且不可更改。
   - 实例密码：输入 Elasticsearch 实例密码。
   - 丢弃解析失败消息：消息解析失败原因一般是转储到 ES 的消息超过了32kb 或者消息与目标 index 的 schema 不一致。若不丢弃解析失败消息，则任务异常，转储不再继续。
4. 单击**提交**，完成任务创建。

### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，单击目标任务的**ID**，进入任务基本信息页面。
3. 在任务详情页顶部，单击**监控**，选择要查看资源，设置好时间范围，可以查看对应的监控数据。



## 产品限制和费用计算

转储速度与 CKafka 实例峰值带宽上限有关，如出现消费速度过慢，请检查 CKafka 实例的峰值带宽。

  
