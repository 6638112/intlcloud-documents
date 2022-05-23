## 功能简介

支持自定义回源 HTTP 请求头部，携带真实客户端 IP 信息回源。

## 操作步骤

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**站点加速** > **网络优化**。
> ?目前边缘安全加速平台控制台仅对部分用户开放，如需访问控制台，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 开通权限。
> 
3. 在网络优化页面，选择所需站点，单击![](https://qcloudimg.tencent-cloud.cn/raw/8d3e9bac718473e40a340843b4cc7fb8.png)，开启“真实客户端 IP 头部”功能。
![](https://qcloudimg.tencent-cloud.cn/raw/975479021d5c361b038c2339a1709bba.png)
3. 在弹窗中，自定义设置该头部的名称，例如 Tencent-Client-IP，单击**保存**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6a5b5cf7584ca3f8fd76270f8371b19e.png" style="zoom:80%;" />
>?此页面配置均对当前所选站点的全部请求生效，为全局配置。如不同子域名或请求路径配置不同，请在左侧菜单栏中前往 [规则引擎](https://intl.cloud.tencent.com/document/product/1145/46151) 创建更细粒度的自定义配置。

