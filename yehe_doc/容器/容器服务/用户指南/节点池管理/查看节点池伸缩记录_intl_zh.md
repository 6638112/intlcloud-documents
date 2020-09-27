## 操作场景
本文介绍如何查看节点池的伸缩记录，适用于以下场景：
- 您可以通过伸缩活动了解自己业务的流量变化，更有效的按需配置节点池。
- 您可以通过节点池内节点扩缩容活动来了解自己的花费来源，进行更高效的成本管理。
- 您可以了解扩缩容活动失败的原因（例如扩容时由于地域资源售罄导致扩容失败），进行风险管理。

## 前提条件
- 已创建可用节点池。详情请参见 [创建节点池](https://intl.cloud.tencent.com/document/product/457/35901)。
- 已进入“节点池列表”页面。详情请参见 [查看节点池](https://intl.cloud.tencent.com/document/product/457/35902)。

## 操作步骤
社区开源组件 CA 会把任何一次扩缩活动的相关信息，以 Kubernetes event 的形式存储到特定的 Pod 或者 Node 下，但存在 Kubernetes events 资源默认后端只存储1小时的限制。若您想对节点池的扩缩记录进行查询及复盘，建议您开启集群的事件持久化功能，对 Kubernetes Events 进行持久存储。

### 开启事件持久化
1. 登录 [腾讯云容器服务控制台](https://console.cloud.tencent.com/tke2)。
2. 选择左侧导航栏中的【集群运维】>【功能管理】，进入“功能管理”页面。
3. 在“功能管理”页面上方选择地域，单击需开启事件持久化的集群右侧的【设置】。如下图所示：
![](https://main.qcloudimg.com/raw/fe3dfb31a348328eb0403a9a9e2602da.png)
4. 在弹出的“设置功能”窗口中，单击“事件存储”功能右侧的【编辑】。
5. 勾选【开启事件存储】，选择事件持久化日志的日志集和日志主题。如下图所示：
![](https://main.qcloudimg.com/raw/15b2e524a205e68444ce358b58aead84.png)
6. 单击【确定】即可开启事件持久化功能。

### 查看事件持久化
1. 登录 [腾讯云日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 选择左侧导航栏中的【检索分析】，进入【检索分析】管理页面。
3. 在“检索分析”页面上方选择地域，选择希望查看事件持久化的日志集和日志主题。
4. 勾选【event.source.component:cluster-autoscaler】，单击【检索分析】。如下图所示：
![](https://main.qcloudimg.com/raw/05988378bc0ff79d3aaad6d0db3b601b.jpg)
5. 在右侧的【列设置】可配置数据列，对关注的列进行可视化。如下图所示：
![](https://main.qcloudimg.com/raw/57bb00bb42163c87cdf4d63bd08ead88.png)
指定某类事件，例如只关心扩容事件，可选择 TriggeredScaleUp 类型进行检索。如下图所示：
![](https://main.qcloudimg.com/raw/adc93647a5053ab4a74710de1ff0fe02.png)
6. 扩缩容记录查询结果如下 （包含所有节点池的扩容记录）如下图所示：
![](https://main.qcloudimg.com/raw/fc0acdbd1d910ad65ba0085cba329e16.png)

### 检索指引
您可参考以下文档，查看更具体的扩缩容活动列表：
- [CLS 检索语法](https://intl.cloud.tencent.com/document/product/614/30439)
- [CA FAQ](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md)
- CA 扩缩容 Event 的 Reason 字段可能有如下取值：TriggeredScaleUp、NotTriggerScaleUp、ScaledUpGroup、FailedToScaleUpGroup、ScaleDown、ScaleDownFailed、ScaleDownEmpty。详情请参见 [字段详细介绍](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-events-are-emitted-by-ca)。

## 相关操作
您可参考以下文档，了解节点池更多功能及操作：
- [创建节点池](https://intl.cloud.tencent.com/document/product/457/35901)
- [查看节点池](https://intl.cloud.tencent.com/document/product/457/35902)
- [调整节点池](https://intl.cloud.tencent.com/document/product/457/35903)

  
