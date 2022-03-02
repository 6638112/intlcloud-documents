本文为您介绍 Scrum 敏捷管理模式中的需求功能。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。 

## 功能介绍

**项目协同**中的需求模块包含**用户故事**与**需求**两种事项类型，团队可以创建并将较大粒度的需求分解为较小的子需求，并在需求下新建或关联任务、缺陷，实现开发任务的快速分解和分配。

由于用户故事是敏捷框架中最小的工作单元，是从用户角度描述软件如何为其带来特定的价值，是敏捷研发模式中需求敏捷化的重要手段，因此默认仅开启**用户故事**。如需使用**需求**，需前往**项目设置** > **项目协同** > **事项类型**页面，单击右上方**添加事项类型**，选择**需求**事项类型进行勾选，单击**添加**创建需求。

![](https://qcloudimg.tencent-cloud.cn/raw/af4f816a6f2082a4fcfc8600e3e95605.png)

下文将以**用户故事**为例，演示如何管理需求。

## 创建需求[](#create)

1.  进入任意项目后，在**项目协同** > **需求**页面，单击模块右上方**创建用户故事**，填写用户故事标题、描述等基本信息后即可完成创建。一个好的用户故事包括以下三个要素：
 -   角色：谁要使用这个功能。
 -   活动：需要完成什么样的功能。
 -   商业价值：为什么需要这个功能，这个功能带来什么样的价值。
![](https://qcloudimg.tencent-cloud.cn/raw/b9064a55c8ec9df8c5a6cbc3c24871c7.png)
2.  创建完成后，可以进行设置处理人、规划所属迭代、[设置故事点](https://intl.cloud.tencent.com/document/product/1133/44761)、调整优先级、设置截至日期等操作。
![](https://qcloudimg.tencent-cloud.cn/raw/eb91b60d25d57d2003da85e74fb733b0.png)

## 需求分解[](#decompose)

子工作项是为实现**需求**（用户故事、需求）所进行的具体活动，通过在需求下创建子工作项即可实现对需求的分解和分配。

1.  在用户故事详情页选择**添加子工作项**。
![](https://qcloudimg.tencent-cloud.cn/raw/026c94d8622739b5d681cede0dcd76fd.png)
2.  可以仅输入子工作项标题后按回车键快速创建。

也可以在**创建**下拉菜单中选择**完整创建**（快捷键：shift + 回车），填写子工作项详情后完成创建。

3.  子工作项创建成功后，可以在用户故事详情页中查看，也可以在**需求**列表页查看该子工作项。
![](https://qcloudimg.tencent-cloud.cn/raw/0bc2f825badebe08d9a604be475193ae.png)
![](https://qcloudimg.tencent-cloud.cn/raw/5db197420f4e5d2cb6d65b363484fd2f.png)
4.  在用户故事详情页内，通过指定子工作项后方****`···`****菜单内的选项，可以**更改父事项**，或**删除**当前子工作项。
![](https://qcloudimg.tencent-cloud.cn/raw/429b01afafd1be11d98c0f2336eef9d3.png)

## 关联资源[](#resource)

### 关联缺陷[](#bugs)

**需求**内可以关联相同项目内的多个缺陷，但一个缺陷只能关联一个**需求**事项。关于缺陷创建及管理，可参见 [管理缺陷](https://intl.cloud.tencent.com/document/product/1133/44760)。

1.  在用户故事列表页，通过**关联缺陷**选项可以关联已有缺陷，或者快速创建新缺陷与之关联。
![](https://qcloudimg.tencent-cloud.cn/raw/f48b333c433354bf174a26a8d53eec45.png)
2.  已关联缺陷右侧的****`···`****菜单内可以**取消关联**。
![](https://qcloudimg.tencent-cloud.cn/raw/dfe505fde8de7272057abad9b2dd7e57.png)
进入该缺陷详情页，在右侧菜单内也可以查看当前关联的需求，并解除或切换关联。
![](https://qcloudimg.tencent-cloud.cn/raw/ca578d17dd567b61876c467e54f9c567.png)

### 关联测试用例[](#cases)

**需求**可以关联已有测试用例。在用户故事详情页内，通过上方****`···`****菜单内的**关联测试用例**，输入测试用例 ID 或标题，即可查找并完成关联。关于测试用例的创建与管理，可参见 [测试用例](https://help.coding.net/docs/test-management/cases/create.html)。
![](https://qcloudimg.tencent-cloud.cn/raw/bec1aebdf0b93c69c523596e5ccde458.png)

### 引用资源[](#references)

在用户故事详情页的描述或评论中，可通过 `# + 引用 ID/标题` 形式选择资源，引用的资源将会在引用列表中展示；如果当前需求被其他资源引用，那么其他资源将会显示在该需求的被引用列表中。
还支持将**代码提交**与事项进行关联，可以在代码执行提交时，在提交信息中插入关联事项 `# + 引用 ID/标题` 信息（例如：这是一次提交 #3）。详情可参见 [引用资源和上传附件](https://intl.cloud.tencent.com/document/product/1133/44770)。


## 需求状态流转[](#status)

需求状态是指需求在生命周期中所处的阶段，用于组织和跟踪需求。

1.  创建用户故事后，进入该用户故事详情页，状态默认为**未开始**，可在右侧下拉菜单中手动切换状态。
![](https://qcloudimg.tencent-cloud.cn/raw/2020d90ae2f80eaa2f6da29adac21908.png)
2.  在需求列表页，也可以在**状态**栏中，根据进行阶段切换状态。
![](https://qcloudimg.tencent-cloud.cn/raw/547e364a8e9ad69ef19e224df542dc99.png)
3.  在**项目设置** > **项目协同** > **事项类型**页面中，可以自定义用户故事和需求的工作流，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
![](https://qcloudimg.tencent-cloud.cn/raw/7b84c904ad8384fc24b18de7d7cdb7c2.png)

## 需求视图[](#view)

需求列表是产品相关人员的主要工作界面，可以根据使用习惯在**树状视图**、**平铺视图**、**看板视图**中无缝切换视图模式，帮助您对目前项目内的所有需求及工作进度建立全局概念。系统将默认记住上次使用的视图模式，下次使用时将应用相同的视图模式。

当存在大量需求时，配合使用搜索框与筛选器，便可以在繁杂的信息中快速筛选出需要的内容。具体操作及管理可参见 [事项视图管理](https://intl.cloud.tencent.com/document/product/1133/44773)。
![](https://qcloudimg.tencent-cloud.cn/raw/6c82b27cf6ac701a6caf37ae939ff017.png)

## 版本回溯[](#backdate)

需求内所有变更都会记录在活动日志中，可以通过详情页内右上方****`···`****菜单内的**历史版本**按时间顺序查看所有版本。支持版本回溯，可以选择任意历史版本进行恢复，详情可参见 [版本管理](https://intl.cloud.tencent.com/document/product/1133/44771)。
![](https://qcloudimg.tencent-cloud.cn/raw/345295d33524129e1fc3479627e867e0.png)

## 导入/导出需求[](#import)

需求支持批量导入和导出，可在需求列表页右上角****`···`****菜单中导入或导出用户故事和需求，具体操作可参见 [导入和导出事项](https://intl.cloud.tencent.com/document/product/1133/44765)。
![](https://qcloudimg.tencent-cloud.cn/raw/865d445e5a951267907ba811a49d9f09.png)

## 删除需求[](#delete)

在用户故事详情页内，可以通过右上方****`···`****菜单进行**删除**操作。如果含有子工作项，将全部删除，但不会影响所关联缺陷的状态，请谨慎操作。
![](https://qcloudimg.tencent-cloud.cn/raw/57040954f1245c3acbe8d155f4e9644d.png)

如仅需删除子工作项，可在用户故事详情页或指定子工作项详情页内，通过****`···`****菜单进行**删除**操作。
