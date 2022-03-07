如果您无法通过内外网正常访问 MySQL 实例，连接检查工具可协助您轻松排查内外网的连接问题。

当您通过云服务器 CVM 访问 MySQL 遇到访问异常问题时，可以通过 MySQL 控制台所提供的连接检查工具进行内外网连接相关问题的排查，仅需简单的操作便能轻松解决内外网无法连接的问题。

## 内网连接检查
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，选择需要排查的实例，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**连接检查**>**内网检查**页面。
3. 检查内网连接问题时，需单击**添加访问此实例的云主机**，添加访问此 MySQL 的 CVM。
>?选择 CVM 时，默认仅提供同地域 CVM，如果您需要跨地域访问，请通过 [云联网](https://intl.cloud.tencent.com/document/product/1003) 实现网络互通。
>
4. 添加完成后，单击**开始检查**，检查任务完成后，会生成检查报告。
![](https://qcloudimg.tencent-cloud.cn/raw/654edb2725bfa39830429678c3927460.png)

5. 在检查报告的“状态”列，单击**查看报告**可查看检查结果。
 - 若检查状态为**正常**，则表示 CVM 可以通过内网正常访问该 MySQL 实例。
 - 若检查状态为**异常**，则表示 CVM 无法通过内网正常访问该 MySQL 实例，请参考处理建议调整后再进行连接。
<table>
<thead><tr><th>检查项</th><th>异常及处理方法</th></tr></thead>
<tbody><tr>
<td>MySQL 实例状态</td>
<td>检测到您的 MySQL 实例已销毁，如果您并非有意销毁实例，可通过 <a href="https://console.cloud.tencent.com/mysql/recycle">回收站</a> 进行恢复</td></tr>
<tr>
<td rowspan=2>CVM 实例状态</td>
<td>检测到您的 CVM 实例已销毁，如果您并非有意销毁实例，可通过 <a href="https://console.cloud.tencent.com/cvm/recycler/cvm">回收站</a> 进行恢复</td></tr>
<tr>
<td>检查到您的 CVM 实例已关机，如您需要继续使用该 CVM 实例，请前往 <a href="https://console.cloud.tencent.com/cvm/instance">控制台</a> 启动该 CVM 实例</td></tr>
<tr>
<td rowspan=2>CVM 与 MySQL 处于同一 VPC</td>
<td>检测到您的 CVM 与 MySQL 的网络类型不同，CVM 需要与MySQL 处于相同的网络类型，请参考 <a href="https://intl.cloud.tencent.com/document/product/236/37864">网络问题</a> 修改网络类型</td></tr>
<tr>
<td>检测到您的 CVM 与 MySQL 不在同一 VPC 网段，CVM 需要与 MySQL 处于同一地域的同一 VPC 中，请参见 <a href="https://intl.cloud.tencent.com/document/product/236/37864#wlwt">网络问题</a> 修改 VPC</td></tr>
<tr>
<td>CVM 安全组策略</td>
<td>检测到您 CVM 所绑定安全组的<strong>出站规则</strong>未放通对 IP 端口的访问，请参见 <a href="https://intl.cloud.tencent.com/document/product/236/37864#caqzpzyw">CVM 安全组配置有误</a> 放通出站规则</td></tr>
<tr>
<td>MySQL 安全组策略</td>
<td>检测到您 MySQL 实例所绑定安全组的<strong>入站规则</strong>未放通对 IP 端口的访问，请参见 <a href="https://intl.cloud.tencent.com/document/product/236/37864#maqzpzyw">MySQL 安全组配置有误</a> 放通入站规则</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/26017a06eee625078778be7d49a598cf.png">

## 外网连接检查
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，选择需要排查的实例，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**连接检查**>**外网检查**页面。
2. 检查外网连接问题时，需单击**添加访问此实例的外网服务器**，添加访问此 MySQL 实例的外网服务器。
3. 添加完成后，单击**开始检查**，检查任务完成后，会生成检查报告。
![](https://qcloudimg.tencent-cloud.cn/raw/f778cf24c66a1b3dbbacc744cddae743.png)
4. 在检查报告的“状态”列，单击**查看报告**可查看检查结果。
 - 若检查状态为**正常**，则表示外网服务器可以通过外网正常访问该 MySQL 实例。
 - 若检查状态为**异常**，则表示外网服务器无法通过外网正常访问该 MySQL 实例，请参考处理建议调整后再进行连接。
<table>
<thead><tr><th>检查项</th><th>异常及处理方法</th></tr></thead>
<tbody><tr>
<td>MySQL 实例状态</td><td>检测到您的 MySQL 实例已销毁，如果您并非有意销毁实例，可通过 <a href="https://console.cloud.tencent.com/mysql/recycle">回收站</a> 进行恢复</td></tr>
<tr>
<td>外网开通状态</td>
<td>检测到您的 MySQL 实例未开启外网，可参考 <a href="https://intl.cloud.tencent.com/document/product/236/37788">开启外网</a></td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c2eca23c3ceba00e8a890f9eea682c52.png">
