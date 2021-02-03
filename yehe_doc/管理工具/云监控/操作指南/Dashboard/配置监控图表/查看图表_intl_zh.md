

本文将为您介绍如何查看监控图表。

## 准备工作


1. 登录 [云监控控制台](https://console.cloud.tencent.com/monitor)。
2. 在左侧导航栏中单击【Dashboard列表】，进入 Dashboard 列表页。
3. 在 Dashboard 列表中找到您需要查看的 Dashboard ，单击面板名，进入 Dashboard 管理页。

## 使用指标排序功能查看图表
单击图表中单击【<img src="https://main.qcloudimg.com/raw/bc2e0e986ee5ad450e8a090582ca0697.png" width="2.4%">】，一键开启 TOPN 功能。调整排序规则、展示数量。方便您大批量查看机器高低负载。
![](https://main.qcloudimg.com/raw/06e8a0f40b9717da9daaae11298b111a.png)

若您在 [新建指标](https://intl.cloud.tencent.com/document/product/248/38477) 时开启了排序功能，您还可以单击图表中的 TOPN 按钮，调整排序规则、展示数量和关闭排序功能。方便您大批量查看机器高低负载。
![](https://main.qcloudimg.com/raw/3e7cd162733479cd853a11f225ea8f8d.png)

## 全屏查看图表

单击图表右上方的更多图标【<img src="https://main.qcloudimg.com/raw/7aa3947e6678d2e035766c2cc912aab3.png"  style="margin:0;" width="3%">】>【全屏浏览】即可全屏查看图表。
![](https://main.qcloudimg.com/raw/35b85b5a1d17ac67277ac1fbbfb255af.png)
退出全屏可按【ESC】或单击右上方的【<img src="https://main.qcloudimg.com/raw/0be3daafc00fb030f84ed2123e05e083.png"  style="margin:0;" width="3%">】图标。

## 查看实例详情

单击图表右上方的【<img src="https://main.qcloudimg.com/raw/497169f09047d1435cf8fedb6fb12b39.png" style="margin:0;" width="3%">】图标（下图中红圈1位置处），展开实例详情。您还可以单击实例详情右上角的【<img src="https://main.qcloudimg.com/raw/9f49988ef96508fb071de4a6950c4a12.png" style="margin:0;" width="3%">】图标（下图中红圈2位置处），勾选实例详情需要展示的字段和最值。
![](https://main.qcloudimg.com/raw/f0b3ab4361e60fcf462d3815e8948908.png)



## 图表缩放和移动

- 图表缩放：您可以把鼠标移动到图表右下方，当出现如下图所示的直角图标时，进行图表缩放。
![](https://main.qcloudimg.com/raw/c72680059f222810059717ebea194993.png)
- 图表移动：您可以把鼠标移动到图表名称处，当出现如下图所示的移动图表时，对图表进行移动。
![](https://main.qcloudimg.com/raw/3eacae042692b3a686eb6ab9f21f0fa3.png)

## 查看某时刻监控数据

您可以把鼠标移动到监控图表处，查看某一时刻的监控数据。如下图所示：
![](https://main.qcloudimg.com/raw/5fc295ca3a8578bc6dec8d6e6a28eb16.png)

## 使用变量选择器查看

当您实例数量过多时，可以定义一个模板变量进行动态切换标签，在同一个监控图表中查看不同实例的监控数据。
![](https://main.qcloudimg.com/raw/e1dbd073718dbf503f32bf686f4faf57.png)

>?如需创建模板变量请参见 [Dashboard 全局配置](https://intl.cloud.tencent.com/document/product/248/38472)。

## 调整图表时间跨度查看监控数据

Dashboard 默认展示近12小时的数据。

通过 Dashboard 右上角的时间选择控件，可调整 Dashboard 中所有图表展示的数据区间和粒度。用户可回顾历史监控数据、进行排障定位问题。
![](https://main.qcloudimg.com/raw/8684005a0e3b9f07759d2660a593cb03.png)

**时间周期和图表颗粒度对照表**

| 时间范围    | 默认统计周期 |
| ----------- | ------------ |
| <=1h        | 1min         |
| (1h，12h]   | 1min         |
| (12h，3d]   | 5min         |
| (3d，30d]   | 1h           |
| (30d，186d] | 1d           |
