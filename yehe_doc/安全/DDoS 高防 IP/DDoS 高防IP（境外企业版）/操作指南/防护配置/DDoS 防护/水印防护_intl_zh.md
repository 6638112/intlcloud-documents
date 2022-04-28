DDoS 高防 IP（境外企业版）支持对业务端发出的报文增加水印防护，在您配置的 UDP 和 TCP 报文端口范围内，业务端和 DDoS 防护端共享水印算法和密钥，配置完成后，客户端每个发出的报文都嵌入水印特征，而攻击报文无水印特征，借此甄别出攻击报文并将其丢弃。通过接入水印防护能高效全面防护4层 CC 攻击，如模拟业务报文攻击和重放攻击等。

## 前提条件
您需要成功 [购买 DDoS 高防 IP（境外企业版）](https://intl.cloud.tencent.com/document/product/297/41154)  ，并设置防护对象。
>?此功能为额外付费功能，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 进行开通。

## 操作步骤
1.  登录 [DDoS 高防 IP（境外企业版）](https://console.cloud.tencent.com/ddos/ddos-basic) 控制台 ，在左侧导航中，单击 **DDOS 高防 IP** > **防护配置** > **DDoS 防护**。
2.  在左边的列表选中高防 IP 的 ID，如“xxx.xx.xx.xx bgpip-000003n2”。
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. 在水印防护卡片中，单击**设置**。
4. 在水印防护列表中，单击**新建**，填写相关字段，单击**确定**，创建水印防护规则。
![](https://qcloudimg.tencent-cloud.cn/raw/4423cab4c25ca96695f2072d3eefe139.png)
5. 新建完成后，水印防护列表将新增了一条水印防护规则，可以在右侧操作列，单击**密钥配置**，可以查看和配置密钥。
![](https://qcloudimg.tencent-cloud.cn/raw/2e595085a08a622e9340e66e603405ce.png)
6. 在密钥信息窗口中，用户可以查看或复制密钥。
![](https://main.qcloudimg.com/raw/248b74becc853b238793c466a5635cce.png)
7.  在密钥信息窗口中，可以添加或删除密钥，只有在两个密钥时可以删除一个密钥，最多只能有两个水印密钥。
![](https://main.qcloudimg.com/raw/2bf90364cfc8bf00ee43646a8e0d30e0.png)
