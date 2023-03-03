本文为您介绍如何创建 VPN 网关。

## 操作步骤
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧目录中单击 **VPN 连接** > **VPN 网关**，进入管理页。
3. 选择地域，如示例中的**广州**，单击 **+新建** 。
>? 若 **+新建** 显示灰色，且鼠标移至上方时显示“无可用私有网络”，请 [创建私有网络](https://intl.cloud.tencent.com/document/product/215/31805) 后再进行新建 VPN 网关。 
>

4. 填写 VPN 网关名称（如 TomVPNGw），选择关联网络、所属网络、带宽上限、标签、计费方式，单击**创建**即可。VPN 网关创建完成后，系统随机分配公网 IP，如：`203.195.147.82`。
>?
>- 200Mbps、500Mbps、1000Mbps和3000Mbps带宽目前仅华北地区（北京）、华东地区（上海）、华南地区（广州）、西南地区（成都）、港澳台地区（中国香港）、华东地区（南京）等可用区开放，如需请 <a href="https://console.cloud.tencent.com/workorder/category">提交工单</a>。
>- 200Mbps、500Mbps、1000Mbps和3000Mbps带宽仅支持新建网关，存量网关暂不支持。
>- 如果 VPN 网关使用200Mbps、500Mbps、1000Mbps和3000Mbps规格的带宽，VPN 通道加密协议建议使用 AES128+MD5。
>

<img src="https://qcloudimg.tencent-cloud.cn/raw/000302a4f734a94744f70bf552308ddc.png" width="70%">

>?标签为选配，请保持默认。
>

## 相关文档
[步骤2：创建对端网关](https://intl.cloud.tencent.com/document/product/1037/32691)
[步骤3：创建 VPN 通道](https://intl.cloud.tencent.com/document/product/1037/32692)
[步骤4：本地网关加载配置](https://intl.cloud.tencent.com/document/product/1037/32693)
[步骤5：配置路由表](https://intl.cloud.tencent.com/document/product/1037/32694)
[步骤6：激活 VPN 隧道](https://intl.cloud.tencent.com/document/product/1037/32695)
