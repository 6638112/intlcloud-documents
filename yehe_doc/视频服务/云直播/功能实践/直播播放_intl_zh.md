## 准备工作
1. 开通 [腾讯云直播服务](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)。
2. 访问 [云直播控制台](https://console.cloud.tencent.com/live/livestat)，获取推流地址，实现直播推流，具体操作请参见 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558) 。
3. 选择 [域名管理](https://console.cloud.tencent.com/live/domainmanage)，单击【添加域名】，填写您已备案成功的域名，选择类型为【播放域名】，单击【保存】即可。

4. 登录 [域名服务控制台](https://console.cloud.tencent.com/domain)，对已添加成功的播放域名进行 CNAME 配置，具体操作请参见 [配置域名 CNAME](https://intl.cloud.tencent.com/document/product/267/31057)。

## 获取播放地址
进入云直播控制台的【直播工具箱】>[【地址生成器】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) 获取播放地址，在该页面进行如下配置：
-  选择生成类型为：**播放域名**。
- 选择您在域名管理中已添加的播放域名。
- 填写与推流地址相同的 StreamName，播放地址 StreamName 要与推流地址 StreamName 一致才能播放对应的流。
- 选择地址过期时间，例如：`2019-12-13  23:59:59`。
- 单击 【生成地址】即可。
![](https://main.qcloudimg.com/raw/22849cdba8e95de22b9fbc2dbe6bf4eb.png)
>?除上述方法，您还可以在云直播控制台的[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)中，选择播放域名单击【管理】，选择【播放配置】，选择播放地址的过期时间，输入与推流地址相同的 StreamName，单击【生成播放地址】即可。

## 直播播放
您需要先进行 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558)，推流成功后才能通过播放地址查看直播画面。您可以根据业务场景使用以下方式进行直播测试。

### 场景一： PC 端播放
您可使用[ VLC](https://intl.cloud.tencent.com/document/product/267/32483)、FFmepg 及 [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html)  等工具进行播放。
![](https://main.qcloudimg.com/raw/10aa7116cbfb227f28ef5e6cf850d02f.png)
### 场景二：移动端播放
1. 下载安装 [腾讯云工具包 App](https://intl.cloud.tencent.com/document/product/1071/38147)。
2. 打开选择【移动直播】>【标准直播播放】或【快直播播放】。
3. 在输入框中填入播放地址，或者扫描播放地址的二维码录入。

### 场景四：Web 端播放
建议您选用播放器 SDK 的 [TCPlayerLite](https://cloud.tencent.com/document/product/881/20207) 进行播放，它基于腾讯云强大的后台能力与 AI 技术，提供视频直播和点播的强大播放能力，Player+ 深度融合腾讯视频云直播、点播服务，拥有流畅稳定的播放性能，集广告植入、数据监测等功能于一身。
>! 目前市面上大多数手机浏览器不支持 HTTP-FLV 播放，因此腾讯云建议您在 Web 播放时的协议选择最好是 PC 浏览器用 HTTP-FLV 协议播放直播流，手机浏览器用 HLS 播放直播流。


## 常见问题
- [支持哪些播放协议？](https://intl.cloud.tencent.com/document/product/267/7968)
- [播放地址由什么组成？](https://intl.cloud.tencent.com/document/product/267/7968)
- [如何使用播放转码？](https://intl.cloud.tencent.com/document/product/267/35598)
- [如何使用时移回看？](https://intl.cloud.tencent.com/document/product/267/35598)
- [如何使用 HTTPS 播放？](https://intl.cloud.tencent.com/document/product/267/35598)
- [如何使用海外加速节点播放？](https://intl.cloud.tencent.com/document/product/267/35598)
- [如何开启播放防盗链？](https://intl.cloud.tencent.com/document/product/267/35598)

