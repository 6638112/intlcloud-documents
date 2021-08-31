腾讯云网络探测是监控 VPC 网络连接质量的服务，可为您监控网络连接的时延、丢包率等关键指标。

在混合云网络架构下，您将使用 VPN/专线连接云上 VPC 和您的自有 IDC，为了实时监控连接的网络质量，您可以在需要与 IDC 通信的子网内创建网络探测对象，探测对象创建后将返回探测的链路的丢包率及时延，帮助您实现如下功能：

- 连接质量实时监控。
- 连接故障实时告警。

## 使用说明

- 网络探测为 Ping 探测，频率：20次/分钟。
- 每个私有网络内最多可创建50个网络探测实例。
- 同一个 VPC 下最多20个子网可以创建网络探测。

## 创建网络探测

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在左侧目录中，选择【诊断工具】>【网络探测】。
3. 在管理页面上方单击【+新建】。
4. 在“新建网络探测”弹窗中，填写相关字段。
>?
>- 网络探测路由为系统路由，不可修改。
>- 在子网切换路由时，原子网关联路由表将删除此系统路由，子网新关联的路由表将添加此系统路由。

![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**字段说明**：

<table>
<thead>
<tr>
<th>字段</th>
<th>含义</th>
</tr>
</thead>
<tbody><tr>
<td>名称</td>
<td>网络探测名称。</td>
</tr>
<tr>
<td>私有网络</td>
<td>探测源 IP 所在的私有网络。</td>
</tr>
<tr>
<td>子网</td>
<td>探测源 IP 所在的子网。</td>
</tr>
<tr>
<td>探测目的 IP</td>
<td>网络探测最大支持两个目的 IP 地址，请为网络探测的目的主机开通 ICMP 防火墙策略。</td>
</tr>
<tr>
<td>源端下一跳路由</td>
<td>可选择“不指定”和“指定”。<ul><li>若选择“不指定”，则默认不选择下一跳路由。<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>注意：
</div>
<p>不指定源端下一跳路由功能为白名单功能，如需使用请 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC&level3_id=185&radio_title=%E5%85%B6%E4%BB%96%E9%97%AE%E9%A2%98&queue=96&scene_code=16314&step=2">提交工单</a> 进行申请。</p></li><li>若选择“指定”，则需选择下一跳类型和具体实例，配置下一跳对象后，系统将自动在子网所关联的路由表中添加对应的32位路由。</li></ul></td>
</tr>
</tbody></table>
5. 字段填写完成后，在“探测目的 IP”后，单击【验证】：
	- 若连接成功，单击【确定】即可。
	- 若连接失败，请检查子网路由是否配置正确或目的探测对象是否放通了网络 ACL、安全组等防火墙，详情请参见 [管理网络 ACL](https://intl.cloud.tencent.com/document/product/215/31852) 及 [修改安全组规则](https://intl.cloud.tencent.com/document/product/215/35515)。

## 查看网络探测时延和丢包率

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在左侧目录中，选择【诊断工具】>【网络探测】。
3. 在目标网络探测实例的“监控”列，单击监控图标，即可查看网络探测时延及丢包率。
   ![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## 修改网络探测

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在左侧目录中，选择【诊断工具】>【网络探测】。
3. 在网络探测实例列表中，找到需要修改的网络探测实例，在右侧操作列，单击【编辑】。
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. 在“编辑网络探测”弹窗中（下图以不指定“源端下一跳路由”实例为例），输入需要修改的信息，并单击【确定】。
![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## 删除网络探测
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在左侧目录中，选择【诊断工具】>【网络探测】。
3. 在网络探测实例列表中，找到需要删除的网络探测实例，在右侧操作列，单击【删除】。
4. 在弹出的确认框中，单击【删除】即可。
 >!删除网络探测实例，其相关路由将一并删除。

 ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)
