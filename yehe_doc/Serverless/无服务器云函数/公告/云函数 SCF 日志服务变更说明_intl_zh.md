# 云函数 SCF 日志服务变更说明

>说明：
>
>云函数 SCF 计划于 2021 年 1 月 25 日进行日志服务升级，接入腾讯云日志服务 CLS，在此之后新增函数需要指定日志投递主题，SCF 后台不再存储函数调用日志。具体操作请参考[指引文档](https://intl.cloud.tencent.com/document/product/583/34876)。
>
>本次变更对存量函数没有影响，存量函数日志迁移到 CLS 预计在 2021 年 2 月中下旬启动，届时会另行通知。
>

## 背景

腾讯云[日志服务 CLS](https://intl.cloud.tencent.com/document/product/614) 提供一站式的日志数据解决方案。您无需关注扩缩容等资源问题，五分钟快速便捷接入，即可享受从日志采集、日志存储到日志内容搜索、统计分析等全方位稳定可靠的日志服务。帮助您轻松解决业务问题定位，指标监控、安全审计等日志问题。大大降低日志运维门槛。

SCF 接入 CLS 后，函数日志可支持：

- **实时索引**：采集的日志数据实时建立索引，构建成功即可检索；
- **灵活检索**：包括全文检索、多关键词检索、范围检索、模糊检索等功能；
- **灵活投递**：可自定义日志投递位置和日志存储周期，支持将指定日志投递至其他云产品中，满足存储或其他计算需求。如指定的 COS 存储桶中，对日志进行生命周期管理等，满足日志审计需求。

## SCF 日志服务升级详情

1. 自 2021 年 1 月 25 日起，通过 SCF 控制台和 API 创建的函数均需指定日志投递主题，SCF 后台不再进行额外存储，函数调用日志将按照函数日志配置投递到指定主题。

2. SCF 提供了日志默认投递的能力，通过控制台创建函数将会默认投递函数调用日志到 SCF 专用日志集 SCF\_logset 下的日志主题 SCF\_logtopic 中，如不存在将创建；通过 api 创建函数请指定函数日志投递主题或选择默认投递，详情请参考[API文档-创建函数](https://intl.cloud.tencent.com/document/product/583/18586)。默认投递下，函数调用日志默认保留 7 天，您可在[日志服务控制台](https://console.cloud.tencent.com/cls/logset)查看及管理。

3. 腾讯云日志服务 CLS 商业化后，腾讯云仍旧为所有用户在每个地域提供一定量的免费额度，SCF 日志专用主题将会占用该免费额度，日志计费详情请参考[CLS计费指引](https://intl.cloud.tencent.com/document/product/614/37889)。

4. 在升级窗口期（2021 年 1 月 18 日 - 2021 年 1 月 25 日）SCF 投递至 CLS 的日志格式将按地域逐步调整，更新后的日志格式请[参考文档](https://intl.cloud.tencent.com/document/product/583/34876)，相比于当前投递到 CLS 的函数日志格式，增加了字段`SCF_LogTime`，`SCF_Duration`，`SCF_MemUsage`，`SCF_StatusCode`和`SCF_RetryNum`，下线了字段`SCF_Index`。

5. SCF 日志接入 CLS 后，仍旧为异步调用的函数保留了返回数据。返回数据将写入 `SCF_Message`，格式为 `Response RequestId:xxx RetMsg:xxx` 。

>! 
>SCF_Message 的值长度限制为 8KB，超出将截取前 8KB。



