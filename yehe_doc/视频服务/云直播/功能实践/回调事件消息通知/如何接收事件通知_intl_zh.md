当直播过程中域名关联模板事件被触发时，腾讯云将主动发送请求到客户服务器，客户服务器负责应答请求。验证通过后，您可被动获取到含直播事件回调信息的 JSON 数据包。

目前直播事件触发消息通知支持事件包括：直播推流、直播断流、直播录制、直播截图、直播鉴黄事件消息通知。

## 整体流程

<img src="https://main.qcloudimg.com/raw/ea1b7cd9ac91b2d561ef045c2f6f2159.svg" data-nonescope="true">

**流程说明：**
1. 主播在控制台或直接调用云 API 配置事件消息通知 URL 以及录制、截图等相关功能。
2. 主播进行直播推断流。
3. 当直播服务内部有事件发生时，消息将会经由事件消息通知服务统一回调给观众。
<span id="protocol"></span>
## 事件消息通知协议

### 网络协议
- 请求：HTTP POST 请求，包体内容为 JSON，每一种消息的具体包体内容参见后文。
- 应答：HTTP STATUS CODE = 200，服务端忽略应答包具体内容，为了协议友好，建议客户应答内容携带 JSON： `{"code":0}`

### 通知可靠性

事件通知服务具备重试能力，重试间隔为60秒，总计重试3次。为了避免重试对您的服务器以及网络带宽造成冲击，请保持正常回包。触发重试条件如下：

- 长时间（20 秒）未回包应答。
- 应答 HTTP STATUS 不为200。

<span id="configuration"></span>
## 回调事件配置方式
回调配置主要通过两种方式实现，一种是通过 [云直播控制台](#c_callback)，另一种是通过调用 [服务端 API](#api_callback)。
>?直播回调事件消息通知 URL 支持对推流事件、断流事件、录制事件、截图事件、鉴黄事件配置独立回调 URL。



<span id="c_callback"></span>
### 云直播控制台
1. 进入云直播控制台的【功能模板】>【[回调配置](https://console.cloud.tencent.com/live/config/callback)】，创建回调模板，具体操作可参见 [创建回调模板](https://intl.cloud.tencent.com/document/product/267/31074)。
![](https://main.qcloudimg.com/raw/e487fbb21c3e7018c97f82f7055b8f8a.png)
2. 在[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)找到您需操作的推流域名，单击【管理】>【模板配置】，将此域名与转码模板进行关联。具体操作请参见 [回调配置](https://cloud.tencent.com/document/product/267/35254)。
<span id="api_callback"></span>
### 服务端 API
1. 调用 [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) 创建回调模板接口，设置您需要的回调参数信息。
2. 调用 [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) 创建回调规则，设置参数推流域名 DomainName 和 TemplateId（第1步返回），填写与推流和播放地址中一致的 AppName，实现部分直播流开启回调的效果。

## 回调信息参数说明
回调模板关联域名成功后。当直播过程中触发模板事件，腾讯云将主动发送含回调信息的 JSON 包到客户服务器，回调信息具体参数说明如下：
- [推流事件消息通知](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [断流事件消息通知](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [录制事件消息通知](https://intl.cloud.tencent.com/zh/document/product/267/38082)
- [截图事件消息通知](https://intl.cloud.tencent.com/zh/document/product/267/38083)
- [鉴黄事件消息通知](https://intl.cloud.tencent.com/zh/document/product/267/38084)






