本文为您详细介绍如何在 CODING 项目协同中使用管理事项视图。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击进入左侧菜单栏中的**项目协同**功能。

## 功能介绍[](intro)

在事项（需求、任务、缺陷）列表页，以及迭代事项内，均可以根据使用习惯，在**树状视图**、**平铺视图**、**看板视图**中无缝切换视图模式。系统将默认记住上次使用的视图模式，下次使用时将应用相同的视图模式。
![](https://qcloudimg.tencent-cloud.cn/raw/41092f7e0cffa039d2ea29f261a4bcfb.png)

## 看板视图[](kanban)

### 事项看板视图[](issue)

在事项列表页右上方，可将视图展示模式切换为看板视图，支持将事项作为卡片放入不同的看板列中，可以从整体纵览整个项目的工作进展和不同阶段的工作量。
![](https://qcloudimg.tencent-cloud.cn/raw/9b852c3f6788fc32a746f9e72b028565.png)

>!在**全部事项**下，看板视图不可用。
>

在看板任意列的任意卡片中，可通过卡片右上方编辑按钮，选择**关注/取消**事项、**复制**事项链接、**新窗口打开**事项。
![](https://qcloudimg.tencent-cloud.cn/raw/1437308c02623842c921bdbc02a0c114.png)

### 迭代内看板视图[](id:statistics)

迭代的事项列表页包含**全部**、**需求**、**任务**、**缺陷**四项，在默认分组模式下，**全部** Tab ⻚中的三列看板已包含需求、任务和缺陷的所有具体状态。同时可以进行 [自定义看板](#custom) 操作。
![](https://qcloudimg.tencent-cloud.cn/raw/faf57763a6a62fea37313c6a4b19176f.png)

如切换**按子工作项分组**的看板模式，则可以看到归属当前迭代下的事项的子任务，和其所属的父事项。


同时，该分组模式下的搜索条件只作用于子任务，支持以下搜索条件:
-   所属父需求类型：全部、需求、任务和缺陷。
-   子任务标题关键字。
-   处理人、关注人。

![](https://qcloudimg.tencent-cloud.cn/raw/a7230099f7397d15b470efd62a9bb8ff.png)

### 修改事项状态和所在列[](id:edit) 

看板视图默认包含**未开始**、**进行中**和**已完成**的事项，拖动卡片即可修改事项的状态和所在列。每个卡片可放入不同的看板列，也可在同一看板列中上下拖动以改变状态。
![](https://qcloudimg.tencent-cloud.cn/raw/03830a04c541696b66d0246b5b566db1.png)

>?看板拖动需拥有以下两项权限：
> 1.  拥有事项编辑权限；
> 2.  拥有事项状态步骤执行权限。
> 
> 相关内容及权限配置请参见 [自定义用户组](https://help.coding.net/docs/project-settings/members.html#user-group-customized)。

### 自定义看板[](id:custom)

针对每个项目，可分别对需求、任务和缺陷三个模块进行看板视图功能自定义设置。在事项列表页右上方的**看板视图设置**中，可新建、排序、重命名、删除看板列，并且可将事项的状态拖进不同的看板列中。
>!仅拥有**属性与流程**配置权限的成员可对看板视图进行设置。

![](https://qcloudimg.tencent-cloud.cn/raw/38ff2ac9a2c40ddd53cd7bca3a731847.png)

1.  在**看板视图设置**中，选择**新建列**，输入新建看板列名称。
![](https://qcloudimg.tencent-cloud.cn/raw/9536191f50a7b7bb70ecc360557fd1ca.png)
>!看板列下事项状态不能为空，否则该列将不在看板显示。如果没有适合状态，请先前往项目设置中为对应事项添加状态，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768) 了解如何进行事项状态配置。
> ![](https://qcloudimg.tencent-cloud.cn/raw/0addde3761a77c7b1ca6a21928908a7d.png)
> 
2.  将事项状态拖入新建看板列，看板列也可左右拖动，根据需求进行排序。
![](https://qcloudimg.tencent-cloud.cn/raw/0f90025f0cc92aa3b1fc1ff29bb96ecc.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2353ca6dd8a6b389d956f6bc058dac3c.png)
3.  若希望某事项状态不在任意看板列中显示，可将该事项状态拖入下方。
![](https://qcloudimg.tencent-cloud.cn/raw/a632e523811dbb0264d447529ae01c65.png)
4.  任意看板列均可通过右上方的**编辑**进行重命名与删除操作。完成所有操作后，选择**恢复修改**则恢复至修改前配置；选择**保存**则完成新建，看板视图中即可显示新看板列。
![](https://qcloudimg.tencent-cloud.cn/raw/6de17b0d30cfce5774a8e4364a9d6f0a.png)

## 树状视图[](id:tree-view)

树状视图是以树状形式展示该事项下符合条件的内容，根节点为需求树中归属到当前事项内最高层级的节点。

>!
1.  在 Scrum 敏捷项目管理模式下，**全部事项**中的树状视图不可用。
2.  在经典项目管理模式下，**任务**、**缺陷**中的树状视图不可用。

![](https://qcloudimg.tencent-cloud.cn/raw/0454de2b256e578ad73f5a5e00660084.png)
## 平铺视图[](id:tile-view)

平铺视图是忽略事项的层级结构，将所有匹配搜索条件的事项（包括子任务和子需求）展示成列表。可在平铺视图选项中选择是否显示子工作项。
![](https://qcloudimg.tencent-cloud.cn/raw/08956d22744f1fbfbd51fd7ec1ed1158.png)

## 自定义事项表头[](id:header)

您可以在**树状视图**与**平铺视图**，通过事项列表右上方的设置选项，就事项列表页进行自定义配置。
![](https://qcloudimg.tencent-cloud.cn/raw/34c4bfc0b40c1788c09cd0df9c4240d8.png)

在配置页可以根据使用习惯调整属性显示密度，展示或关闭表头属性，上下拖动属性调整显示优先级。选择**恢复默认**可以将表头重置为系统初始状态。
![](https://qcloudimg.tencent-cloud.cn/raw/37d11187348941df391d6011fb1e21f5.png)

在事项详情页，可以通过拖拽边线调整各属性的显示宽度（每列存在最小和最大宽度限制）。系统将默认保存所做变更，每次设置只会应用于个人视图，不会影响团队中其他成员的视图。
![](https://qcloudimg.tencent-cloud.cn/raw/5619f6a23d68200ca5106f75982880a9.png)
