DDoS 高防 IP 支持通过配置 IP 黑名单和白名单，实现对访问 DDoS 高防 IP 已接入防护的网站业务封禁或者放行，从而限制访问您业务资源的用户。配置 IP 黑白名单后，当白名单中的 IP 访问时，将被直接放行，不经过任何防护策略过滤。当黑名单中的 IP 访问时，将会被直接阻断。
>?当发生 CC 攻击时，IP 黑白名单的过滤才会生效。
>- 白名单中的 IP，访问时将被直接放行，不经过任何防护策略过滤。
>- 黑名单中的 IP，访问时将会被直接阻断。


## 前提条件
您需要成功 [购买 DDoS 高防 IP](https://intl.cloud.tencent.com/document/product/297/37241) ，并设置防护对象。


## 操作步骤
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) ，在左侧导航中，单击**防护配置** > **CC 防护**。
2. 在 CC 防护页面的左侧列表中，选中高防 IP 的 ID 下面的域名。
![](https://qcloudimg.tencent-cloud.cn/raw/3db9584e9adc4c083500f47612012d77.png)
3. 在右侧 IP 黑白名单卡片中，单击**设置**，进入 IP 黑白名单列表。
![](https://qcloudimg.tencent-cloud.cn/raw/a2847abc25fdf6848a669a529c8950df.png)
4. 单击**新建**，填写相关字段，填写完成后，单击**保存**。
![](https://qcloudimg.tencent-cloud.cn/raw/4dbda8f53e7404a6bc2e7156591ac0b6.png)
5. 新建完成后，IP 黑白名单列表将新增一条 IP 黑白名单规则，可以在右侧操作栏中，单击**删除**，删除 IP 黑白名单规则。
![](https://qcloudimg.tencent-cloud.cn/raw/e3a320a3a5f2aa400bd06bc1ea80f13b.png)
