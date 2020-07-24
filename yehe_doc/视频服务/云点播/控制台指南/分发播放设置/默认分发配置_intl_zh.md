## 操作场景
添加并解析域名后，您可以通过新域名访问您的视频资源，但使用 API 接口和控制台获取到的视频 URL 中，Host 仍保持为原始域名。因此，您需要登录控制台，在默认分发配置中更新 URL 的 Host 信息。
## 操作步骤
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod/overview)，选择左侧导航栏的【分发播放设置】>【默认分发配置】，进入“默认分发配置”页面。
2. 单击右上角的【编辑】，设置相应参数：
 - 主分发协议类型：支持 HTTP 和 HTTPS。
 - 默认分发域名：默认使用系统分配的`xxx.vod2.myqcloud.com`，也可以选择自定义 [添加](https://intl.cloud.tencent.com/document/product/266/35572) 并完成 [解析](https://intl.cloud.tencent.com/document/product/266/35572) 的域名作为默认分发域名。
 
