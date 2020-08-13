本文档主要指导您如何通过监控查看服务器舰队、游戏服务器队列、实例监控等信息。

## 前提条件

已完成 [创建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675)。

## 操作步骤

1. 登录 [游戏服务器引擎控制台](https://console.cloud.tencent.com/gse/asset)，单击左侧菜单【服务器舰队】。
2. 单击服务器舰队【ID】，进入服务器舰队详情页。
![](https://main.qcloudimg.com/raw/42c96a345b41ae2545c10534cf8aee1e.png)
3. 在服务器舰队详情页，单击右上角【查看监控】，即可进入监控面板。
![](https://main.qcloudimg.com/raw/99e7932d115505db65079bd78ad71335.png)
4. 单击监控面板上的【添加监控图表】，即可创建监控图表。
![](https://main.qcloudimg.com/raw/bf9242f2c4c272732f95a341d65fd9d7.png)
5. 左上侧产品类型选择：【游戏服务器引擎】，根据您需要监控的对象可选择【服务器舰队】、【游戏服务器队列】、【实例监控】。
![](https://main.qcloudimg.com/raw/40bfdf27116e1b8ebf6a16a33f840116.png)


 - 【游戏服务器引擎-服务器舰队】可供选择的监控指标说明：

<table>
<thead>
<tr>
<th width="30%">监控指标</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>激活中的游戏服务器会话数(Count)</td>
<td>具有 ACTIVATING 状态的游戏服务器会话（表示正在启动）</td>
</tr>
<tr>
<td>活跃的游戏服务器会话数(Count)</td>
<td>具有 ACTIVE 状态的游戏服务器会话（表示能够托管玩家，并且正在托管零个或多个玩家）</td>
</tr>
<tr>
<td>活跃实例数(Count)</td>
<td>具有 ACTIVE 状态的实例（表示正在运行活动服务器进程）</td>
</tr>
<tr>
<td>空闲实例数(Count)</td>
<td>当前托管0个游戏服务器会话的活动实例</td>
</tr>
<tr>
<td>空闲实例数占比(%)</td>
<td>处于空闲状态的所有活动实例的百分比</td>
</tr>
<tr>
<td>最大实例数(Count)</td>
<td>服务器舰队允许的最大实例数</td>
</tr>
<tr>
<td>最小实例数(Count)</td>
<td>服务器舰队允许的最小实例数</td>
</tr>
<tr>
<td>期望实例数(Count)</td>
<td>服务器舰队维护的活动实例的目标数量</td>
</tr>
<tr>
<td>健康服务器进程数(Count)</td>
<td>运行正常的活动服务器进程</td>
</tr>
<tr>
<td>异常关闭的服务器进程数(Count)</td>
<td>自上次报告以来因异常情况而被关闭的服务器进程</td>
</tr>
<tr>
<td>转化为活跃的服务器进程数(Count)</td>
<td>自上次报告以来，从 ACTIVATING 成功转换为 ACTIVE 状态的服务器进程</td>
</tr>
<tr>
<td>关闭的服务器进程数(Count)</td>
<td>自上次报告以来关闭的服务器进程</td>
</tr>
<tr>
<td>活跃服务器进程数(Count）</td>
<td>具有 ACTIVE 状态的服务器进程（表示它们正在运行并且能够托管游戏服务器会话）</td>
</tr>
<tr>
<td>健康服务器进程数占比(%)</td>
<td>运行正常的所有活动服务器进程的百分比</td>
</tr>
<tr>
<td>可用的游戏服务器会话数(Count)</td>
<td>活动、运行正常的服务器进程上当前未使用的游戏服务器会话槽</td>
</tr>
<tr>
<td>可用的游戏服务器会话数占比(%)</td>
<td>所有活动服务器进程（运行正常或不正常）上当前未使用的游戏服务器会话槽的百分比</td>
</tr>
<tr>
<td>活跃的玩家会话数(Count)</td>
<td>具有 ACTIVE 状态（玩家已连接到活动游戏服务器会话）或 RESERVED 状态 （已在游戏服务器会话中为玩家分配槽，但玩家尚未连接）的玩家会话</td>
</tr>
<tr>
<td>转化为活跃的玩家会话数(Count)</td>
<td>自上次报告以来（一段时间内），从 RESERVED 状态转换为 ACTIVE 状态的玩家会话</td>
</tr>
<tr>
<td>购买失败实例数(Count)</td>
<td>未购买成功的实例数</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/610777f8db2c951e732fc3ac0b181633.png)

 - 【游戏服务器引擎-游戏服务器队列】可供选择的监控指标说明：

<table>
<thead>
<tr>
<th width="25%">监控指标</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>放置等待平均时长(s)</td>
<td>游戏服务器队列中具有 PENDING 状态的游戏服务器会话放置请求等待执行的平均时长</td>
</tr>
<tr>
<td>首选非可用放置数(Count)</td>
<td>成功放入游戏服务器会话，但不是首选服务器舰队，因为该服务器舰队被视为不可行（例如，具有较高中断率的 Spot 队组）</td>
</tr>
<tr>
<td>首选无可用资源放置数(Count)</td>
<td>成功放入游戏服务器会话，但不是首选服务器舰队，因为该服务器舰队没有可用资源</td>
</tr>
<tr>
<td>最低延迟地域放置数(Count)</td>
<td>游戏服务器会话成功放入为玩家提供最低延迟的区域</td>
</tr>
<tr>
<td>取消放置数(Count）</td>
<td>自上次报告以来，在超时前被取消的游戏服务器会话放置请求</td>
</tr>
<tr>
<td>失败放置数(Count）</td>
<td>自上次报告以来，因任何原因失败的游戏服务器会话放置请求</td>
</tr>
<tr>
<td>新放置请求数(Count)</td>
<td>自上次报告以来，添加到队列中的新的游戏服务器会话放置请求</td>
</tr>
<tr>
<td>成功放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话放置请求导致了新的游戏服务器会话</td>
</tr>
<tr>
<td>超时放置数(Count)</td>
<td>自上次报告以来，达到队列超时限制而未执行的游戏服务器会话放置请求</td>
</tr>
<tr>
<td>队列深度(Count)</td>
<td>队列中状态为 PENDING 的游戏服务器会话放置请求的数量</td>
</tr>
<tr>
<td>上海区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入上海区域中的服务器舰队</td>
</tr>
<tr>
<td>硅谷区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入硅谷区域中的服务器舰队</td>
</tr>
<tr>
<td>弗吉尼亚区域放置数(Count）</td>
<td>自上次报告以来，游戏服务器会话成功放入弗吉尼亚区域中的服务器舰队</td>
</tr>
<tr>
<td>北京区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入北京区域中的服务器舰队</td>
</tr>
<tr>
<td>广州区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入广州区域中的服务器舰队</td>
</tr>
<tr>
<td>香港区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入香港区域中的服务器舰队</td>
</tr>
<tr>
<td>孟买区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入孟买区域中的服务器舰队</td>
</tr>
<tr>
<td>首尔区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入首尔区域中的服务器舰队</td>
</tr>
<tr>
<td>东京区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入东京区域中的服务器舰队</td>
</tr>
<tr>
<td>法兰克福区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入法兰克福区域中的服务器舰队</td>
</tr>
<tr>
<td>新加坡区域放置数(Count)</td>
<td>自上次报告以来，游戏服务器会话成功放入新加坡区域中的服务器舰队</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/036fef271e25a599a9d50ad769f10614.png)



 - 【游戏服务器引擎-实例监控】可供选择的监控指标说明：

<table>
<thead>
<tr>
<th width="20%">监控指标</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>外网出流量(MBytes)</td>
<td>外网网卡的平均每秒出流量</td>
</tr>
<tr>
<td>内网入包量(Count/s)</td>
<td>内网网卡的平均每秒入包量</td>
</tr>
<tr>
<td>内网入带宽(MBit/s)</td>
<td>内网网卡的平均每秒入流量</td>
</tr>
<tr>
<td>内网出包量(Count/s）</td>
<td>内网网卡的平均每秒出包量</td>
</tr>
<tr>
<td>内网出带宽(MBit/s)</td>
<td>内网网卡的平均每秒出流量</td>
</tr>
<tr>
<td>内存利用率(%)</td>
<td>用户实际使用的内存量百分比，不包括缓冲区与系统缓存占用的内存</td>
</tr>
<tr>
<td>内存使用量(MBytes)</td>
<td>用户实际使用的内存量，不包括缓冲区与系统缓存占用的内存</td>
</tr>
<tr>
<td>CPU 使用率(%)</td>
<td>实例运行期间实时占用的 CPU 百分比</td>
</tr>
<tr>
<td>TCP 连接数(Count)</td>
<td>处于 ESTABLISHED 状态的 TCP 连接数量</td>
</tr>
<tr>
<td>外网入包量(Count/s）</td>
<td>外网网卡的平均每秒入包量</td>
</tr>
<tr>
<td>外网出包量(Count/s)</td>
<td>外网网卡的平均每秒出包量</td>
</tr>
<tr>
<td>外网入带宽(MiBit/s)</td>
<td>外网网卡的平均每秒入流量</td>
</tr>
<tr>
<td>外网出带宽(MiBit/s)</td>
<td>外网网卡的平均每秒出流量</td>
</tr>
<tr>
<td>CPU 一分钟平均负载</td>
<td>一分钟内正在使用和等待使用 CPU 的平均任务数</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/08cae6d15fca6e92cf20ec14c567eb75.png)

6. 右侧【地域】选择您所要监控对象所在的地域，即可显示监控对象名称列表，供您勾选。
![](https://main.qcloudimg.com/raw/ee27d25d7e8e91e2713b1cd475aa0149.png)
7. 您可根据自身业务需求，单击【图表名称】修改图标名称，单击【确定】，即可创建监控图表。
![](https://main.qcloudimg.com/raw/d486150aca8a7ae1afb716748628a4ca.png)
8. 后续您可对该图表进行复制图表、编辑、导出数据、导出图片、删除等操作。
![](https://main.qcloudimg.com/raw/59b55a60695cd9652db14a9fd016f6f3.png)

