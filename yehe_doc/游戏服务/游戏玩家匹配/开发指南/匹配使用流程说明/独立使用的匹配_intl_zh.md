>!由于产品逻辑已无法满足游戏行业技术发展，游戏玩家匹配 GPM 将于2022年6月1日下线，请您在2022年5月31日前完成服务迁移。
本文向您介绍如何独立使用 GPM 匹配服务。

## 前提条件
已完成 [匹配创建](https://intl.cloud.tencent.com/document/product/1072/39203) ，并选择“**无需自动连接对战的匹配**”类型进行匹配创建。

## 流程架构
独立使用 GPM 匹配服务架构图如下：
![](https://main.qcloudimg.com/raw/575fe64bddcdf7155c4e7c5685304d6f.png)

## 匹配状态流转

独立使用 GPM 匹配服务，您的匹配票据状态将会经历如下过程：
>?关于匹配票据的详细说明，详情请参见 [匹配票据参数说明](https://intl.cloud.tencent.com/document/product/1072/39214)。
>
![](https://main.qcloudimg.com/raw/ef69b3a6f56174deae5c6bdead0ec644.png)


## 操作步骤

### 步骤1：在客户端服务器发起匹配请求

您需要准备一个后端服务来处理来自客户端的玩家请求，并通过此客户端服务器调用 GPM 的 [StartMatching](https://chttps://intl.cloud.tencent.com/document/product/1072/39904) 接口，向 GPM 请求匹配服务。一次成功的 [StartMatching](https://intl.cloud.tencent.com/document/product/1072/39904) 调用，将会生成一个唯一的匹配票据，您需要跟进这个匹配票据的状态，来完成您的匹配流程。

您也可以通过客户端服务器调用 GPM 的 [CancelMatching](https://intl.cloud.tencent.com/document/product/1072/39908) 接口，用于取消正在匹配中的匹配票据。

### 步骤2：通过匹配事件通知，跟进匹配状态

成功发起匹配后，您配置过接收事件通知的地址，将会收到来自 GPM 的匹配事件推送。您可以设置一个定时器，周期性的处理事件推送。关于不同类型匹配事件推送的详细介绍，详情请参见 [事件推送](https://intl.cloud.tencent.com/document/product/1072/39219)。

### 步骤3：处理已完成的匹配票据

- 匹配搜索到潜在的对战组合票据后，您需要解析 [推送协议](https://intl.cloud.tencent.com/document/product/1072/39219) 里的匹配票据信息，以获得被匹配到同一个对战的玩家 ID。
- 对于匹配到符合对战要求的票据，您需要为这些票据内的玩家请求对战服务器，并将这些玩家连接到同一个对战进程里。由于您独立使用 GPM 服务，匹配完成后的玩家连接、对战逻辑需要您自行处理。
- 对于**被取消/匹配超时/匹配失败**的票据，您可以根据实际的业务逻辑自行对玩家进行通知，或在客户端服务器上为票据内的玩家重新发起匹配。


### 步骤4：（可选）利用查询匹配进度接口，作为匹配事件推送的补充机制

如果您没有配置接收匹配事件进度的服务器地址，或因为某些原因无法接受到匹配事件通知，您可以通过 GPM 的 [DescribeMatchingProgress](https://intl.cloud.tencent.com/document/product/1072/39907) 接口来定向跟进指定匹配票据的状态。关于不同匹配票据的不同状态说明，详情请参见 [匹配票据状态说明](https://intl.cloud.tencent.com/document/product/1072/39214)。

