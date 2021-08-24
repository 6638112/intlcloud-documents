## 操作场景
为腾讯云资源绑定标签后，您可以通过标签快速查看与其绑定的云资源。

本文介绍三种便捷的方法，供您查看标签下绑定的资源。

## 前提条件
已创建标签并绑定资源（参考 [创建标签](https://intl.cloud.tencent.com/document/product/651/41684)、[绑定资源](https://intl.cloud.tencent.com/document/product/651/41685) ）

## 操作步骤
>?您可以点击以下页签，查看对应查看方式的操作步骤。

<dx-tabs>
::: 通过标签控制台（标签列表）
1. 登录 [标签控制台](https://console.cloud.tencent.com/tag)。
2. 在左侧导航栏中，单击【标签列表】，进入标签列表页面。
3. 在标签列表中，单击目标标签资源数列的数值，查看标签绑定的云资源。
![](https://main.qcloudimg.com/raw/366552d20e7a7c5c1c721152843b9d9f.png)
结果如下：
![](https://main.qcloudimg.com/raw/c4fd0d759c45db2705d40b6555f6f3b7.png)
:::
::: 通过标签控制台（资源标签）
1. 登录 [标签控制台](https://console.cloud.tencent.com/tag)。
2. 在左侧导航栏中，单击【资源标签】，进入资源标签页面。
3. 在资源标签页面，选择以下信息设置筛选规则。
	- 地域：需要查询资源所属地域。             
	- 资源类型：需要查询资源所属类型，仅支持标签的产品，详情请参见 [支持标签的产品](https://intl.cloud.tencent.com/document/product/651/32577)。
	- 标签：需要查询资源所属标签键和标签值，标签值可为空、多选。单击【添加】，填写标签值，可查询多个标签下的资源。
	- 所属项目：单击【更多查询条件】展开所属项目筛选框，选择项目名称过滤资源，仅可查询支持项目管理的产品。
4. 单击【查询资源】，页面下方会以列表形式展示出对应的资源，完成资源查询操作。
![](https://main.qcloudimg.com/raw/bb15cb86716d7861f39affc638068081.png)
:::
::: 通过云产品控制台
对于支持标签的云产品，您可以登录对应云产品的控制台，通过标签查找该云产品的资源。
<dx-alert infotype="explain" title="">
以下步骤以云服务器为例进行介绍。
</dx-alert>
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)。
2. 在左侧导航栏，单击【实例】，进入实例列表页。
3. 单击搜索框，选择标签。
![](https://main.qcloudimg.com/raw/f8c645ff03f2e85485ed1c361288f158.png)
4. 选择一个标签键和标签值，查看该标签绑定的云服务器实例。
:::
</dx-tabs>












