## 操作场景

Datahub 提供数据流出能力，您可以将 CKafka 数据分发至日志管理 CLS 便于解决业务问题定位，指标监控，安全审计等日问题。

## 前提条件

该功能目前依赖 CLS 服务。使用时需提前开通云函数 CLS 等相关服务及功能。

## 操作步骤

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，选择好地域后，单击**新建任务**。
3. 目标类型选择**事件总线（Event Bridge）**，单击**下一步**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/165add1957b06dbd7684fe9f68658fd3.png)

> ?通过云函数和事件总线处理，需要确认同意[云函数使用说明](https://intl.cloud.tencent.com/document/product/583)和[云函数计费说明](https://intl.cloud.tencent.com/document/product/583/17299)。

4. 在任务设置页面，填写任务详情。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8041c40a6129d2b325cd2346272d0e5c.png)
   - 任务名称：只能包含字母、数字、下划线、"-"、"."。
   - CKafka 实例：选择数据源 CKafka。
   - 源 Topic：选择源 Topic。
   - 事件目标：选择 **CLS**。
   - 起始位置：转储时历史消息的处理方式，topic offset 设置。
   - 日志集：选择日志集，日志集日志服务的项目管理单元，用于区分不同项目的日志。
   - 日志主题：自动创建日志主题或者选择已有日志主题。一个 [日志集](https://intl.cloud.tencent.com/document/product/614/32849) 可以包含多个日志主题，一个日志主题对应一类应用或服务，建议将不同机器上的同类日志收集到同一个日志主题。
   - 角色授权：使用事件总线（EventBridge）产品功能，您需要授予一个第三方角色代替您执行访问相关产品权限。
4. 单击**提交**，完成任务创建。

### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，单击目标任务的**ID**，进入任务基本信息页面。
3. 在任务详情页顶部，单击**监控**，选择要查看资源，设置好时间范围，可以查看对应的监控数据。



## 产品限制和费用计算

- 转储速度与 CKafka 实例峰值带宽上限有关，如出现消费速度过慢，请检查 CKafka 实例的峰值带宽或增加 CKafka partition 数。
- 转储速度与 CKafka 单个文件大小相关，如超过该500M，会自动分包上传。
- 该功能基于云函数 SCF 服务提供。SCF为用户提供了一定 [免费额度](https://intl.cloud.tencent.com/document/product/583/12282) ，超额部分产生的收费，请以 SCF 服务的 [计费规则](https://intl.cloud.tencent.com/document/product/583/17299) 为准。
