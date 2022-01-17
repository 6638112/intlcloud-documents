全部业务安全状态展示 ，您可以在 DDoS 防护控制台的防护概览页查看全量实时、业务指标和 DDoS 攻击事件的防护情况，包括基础防护业务、DDoS 高防包防护业务、DDoS 高防 IP 防护业务，便于您分析与溯源。

## 查看攻击态势
1.	登录 [DDoS 防护（新版）控制台](https://console.cloud.tencent.com/ddos/dashboard/overview)，在左侧导航栏中，单击**防护概览** > **防护总览**，进入防护总览页面。
![](https://qcloudimg.tencent-cloud.cn/raw/4fe3a32d876b5824e21b6a67353203c5.png)
2.	在攻击态势模块中，可查看当前业务是否存在风险，和最近一次攻击的时间的攻击类型。当有攻击存在时，单击**升级防护**可进入购买页。
![](https://qcloudimg.tencent-cloud.cn/raw/d1f79eaea3612f82d76fe2772f8d2809.png)
3. 在攻击态势模块中，还可以直观查看各项数据情况。
![](https://qcloudimg.tencent-cloud.cn/raw/ac7c41ff52efbdfabe1aa83eaaeea126.png)
**字段说明：**
 - 被攻击 IP 数：受到攻击的业务 IP 总数。包括基础防护被攻击 IP 数、接入高防包后被攻击的业务 IP 数、高防 IP 实例被攻击数。
 - 已防护 IP 数：接入高防包的业务 IP 和高防 IP 实例。
 - 被封堵 IP 数：被屏蔽所有外网访问的业务 IP 数。包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
 - 被攻击域名数：高防 IP 被攻击的域名数、被攻击的端口所影响的域名数。
 - 已防护域名数：高防 IP 实例的域名接入数量。
 - 攻击峰值：当前攻击事件中的最高攻击带宽。


## 查看防御态势
1.	登录 [DDoS 防护（新版）控制台](https://console.cloud.tencent.com/ddos/dashboard/overview)，在左侧导航栏中，单击**防护概览** > **防护总览**，进入防护总览页面。
2. 在防御态势模块的统计图中，展示业务 IP 状态数据，可以快速了解业务 IP 健康状态。
![](https://qcloudimg.tencent-cloud.cn/raw/db4d712c7e6654124f6f98c4c79404ba.png)
**字段说明：**
 - IP 总数：当前全部业务 IP 总数，包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
 - 已防护 IP 数：接入高防包的业务 IP 和高防 IP 实例。
 - 封堵 IP 数：被屏蔽所有外网访问的业务 IP 数。包括基础防护的业务 IP、接入高防包的业务 IP 和高防 IP 实例。
3. 在防御态势模块的防护趋势中，展示一周内全量业务受攻击总次数的，可以快速了解近期攻击状态分布情况。
![](https://qcloudimg.tencent-cloud.cn/raw/d7059a7f5481277cd08996b1e9f0ba5d.png)
3. 在防御态势模块的防护建议中，展示基础防护状态下受到攻击的业务 IP，提示接入高级防护。方便用户快速为被攻击 IP 接入高级防护，保证业务安全。
![](https://qcloudimg.tencent-cloud.cn/raw/3b6be9d490b7bace48b070c05a8cffd0.png)

## 查看高防实例统计
1.	登录 [DDoS 防护（新版）控制台](https://console.cloud.tencent.com/ddos/dashboard/overview)，在左侧导航栏中，单击**防护概览** > **防护总览**，进入防护总览页面。
2. 在高防实例统计模块中，展示高防 IP 资源的安全状态，可以快速全面了解风险业务分部。
![](https://qcloudimg.tencent-cloud.cn/raw/11ba29a29bad74e00901940d67baddcd.png)

## 查看近期安全事件
1.	登录 [DDoS 防护（新版）控制台](https://console.cloud.tencent.com/ddos/dashboard/overview)，在左侧导航栏中，单击**防护概览** > **防护总览**，进入防护总览页面。
2. 在近期安全事件模块中，展示最近全量的攻击事件。单击**查看详情**，进入事件详情页面，供用户进行 DDoS 攻击分析及溯源支撑。
![](https://qcloudimg.tencent-cloud.cn/raw/1508fe253dcb5ca662e30420cd3b0160.png)
3. 在事件详情页面的攻击信息模块，查看该时间范围内的 IP 遭受的攻击情况，包括被攻击 IP、状态、攻击类型（采样数据）、攻击带宽峰值和攻击包速率峰值、开始时间结束时间基础信息。
![](https://qcloudimg.tencent-cloud.cn/raw/59954cd20d11225c2091f230029317b3.png)
4. 在事件详情页面的攻击趋势模块，可查看网络攻击流量带宽或攻击包速率趋势。当遭受攻击时，在流量趋势图中可以明显看出攻击流量的峰值。
>?此处数据为该攻击时间段全量实时数据。

![](https://qcloudimg.tencent-cloud.cn/raw/e5cd5fbfff7e44ae17ebef0cdac5ba3d.png)
5. 在事件详情页面的攻击统计模块，可通过攻击流量协议分布、攻击类型分布，查看这两个数据维度下的攻击分布情况。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/d7027893c00493c7afe81781dd188efc.png)
**字段说明：**
 - 攻击流量协议分布：查看该时间范围内，所选择的高防 IP 实例遭受攻击事件中各协议总攻击流量的占比情况。
 - 攻击类型分布：查看该时间范围内，所选择的高防 IP 实例遭受的各攻击类型总次数占比情况。
6. 在事件详情页面 “TOP5 展示”模块，可查看攻击源 IP TOP5 和攻击源地区TOP5，准确把握攻击源的详细情况便于精准防护策略的制定。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/00ad52855a7f57c635f2c45259d13c25.png)
7. 在事件详情页面的攻击源信息模块，可查看该攻击时间段内攻击详情的随机采样数据，尽可能详细的展示出此次攻击的细节，主要包括攻击源 IP、地域、累计攻击流量、累计攻击包量。
>?此处数据为该攻击时间段内攻击采样数据，非全量数据。

![](https://qcloudimg.tencent-cloud.cn/raw/4cc6ac3e4efc13b9a130b70c35173485.png)
