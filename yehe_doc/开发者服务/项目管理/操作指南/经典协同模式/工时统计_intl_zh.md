本文为您介绍经典项目管理模式下的工时统计功能。


## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。

## 功能介绍

当团队在进行协作时，往往对事项的工作时间有所要求，CODING 支持在创建事项（需求、任务、缺陷）时设置预估工时，并在创建完成后进行记录工时、登记任务进度等操作。通过填写使用工时（已经工作的时间）和预计剩下的工时，系统将自动生成完整的工时记录，有助于团队在迭代结束后进行复盘与效率分析。下文将以需求为例，演示如何设置并编辑**工时**。
![](https://qcloudimg.tencent-cloud.cn/raw/ffada2e2fc61fba1241d39ad51826167.jpeg)

## 预估工时[](#predict)

创建事项时，可以在右侧**预估工时**内填写该事项的预估工作时间，单位为小时（必须小于 10000，最多保留 2 位小数）。
![](https://qcloudimg.tencent-cloud.cn/raw/b71ec33058a51fcf4c9be31fb983696d.jpeg)

## 登记工时[](#register)

1.  在事项详情页中，可以在右侧**工时记录**中登记工时。
![](https://qcloudimg.tencent-cloud.cn/raw/074bbe067cf927380ad719a24225eb70.jpeg)
2.  在**登记工时**详情页中，可以输入或修改已使用工时，剩余工时将会实时增减，也可以手动修改剩余工时。
![](https://qcloudimg.tencent-cloud.cn/raw/12eafa6743ed52ccf9d4ff9d8199c0ad.jpeg)
3.  开始时间默认为当前时间，您也可以根据实际情况进行修改，可以精确到分钟。
![](https://qcloudimg.tencent-cloud.cn/raw/8132344125f46a39387a358edb9de311.jpeg)
4.  工作描述非必填，您可以简要概括描述所做工作，以便迭代结束后进行复盘。
![](https://qcloudimg.tencent-cloud.cn/raw/4680fdabf24be74d69697b83a61a00a8.jpeg)
5.  填写完毕并**确定登记**后，将会更新事项的剩余工时，并自动在**工时日志**中新增记录。
![](https://qcloudimg.tencent-cloud.cn/raw/263c64bf7476e0b3dbe7ebb3e6d60e19.jpeg)

## 进度统计[](#progress)

在创建事项或事项详情页内，可以在右侧**进度**中，填写数据，对事项进度进行调整。注意，若在需求内含有子事项，则当前进度不可修改，进度由以下公式自动计算：父事项进度 = SUM（直接子事项进度）÷ SUM（直接子事项数）。
![](https://qcloudimg.tencent-cloud.cn/raw/e3986d993b2f4d3a7e6cc386208151fe.jpeg)

### 进度自动更新[](#automatically-update )

进度统计支持当事项流转至**已完成**时，进度自动更新为 100%。需要在**项目设置** > **项目协同**中，对需求/任务的**工作流**分别进行配置。在**配置规则**中选择**更改属性值**，将当前步骤设置为**任何状态 > 已完成**，将更改的属性设置为**进度**，填写进度为**100**，应用配置后即可实现进度自动更新。

![](https://qcloudimg.tencent-cloud.cn/raw/5f9eea688f0ed9e5b6813940fb0999a0.png)
>!仅有开启**管理权限**的用户组成员才能修改或添加自定义状态。详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
>
## 管理工时日志[](#management)

### 查看工时日志[](#check)

可以在**工时记录**中选择**查看工时日志**，可以在事项详情页**活动/工时日志**中切换。工时日志内展示了当前事项工时记录的历史操作，根据登记工时内填写的**开始时间**排序，登记工时的成员、开始时间、实际工时、工作描述一目了然。
![](https://qcloudimg.tencent-cloud.cn/raw/fa1e72308989bfa6bc5f60b8f23adf5d.jpeg)

### 删除工时日志[](#delete)

1.  工时日志可以被该日志的登记成员删除。在**工时日志**中，选择指定日志的下方**删除**选项。
![](https://qcloudimg.tencent-cloud.cn/raw/94f231f8f2e6fd0cc9287de7ae2f65ba.png)
2.  删除时需要选择是否调整剩余工时，若勾选，剩余工时中将会加上删除工时。
![](https://qcloudimg.tencent-cloud.cn/raw/206a75f35ec0da845dce605a478907aa.jpeg)
例如：删除日志内已登记 69 小时，剩余工时 26.92 小时。若勾选**调整剩余工时**，则剩余工时将更新为 26.92 + 69 = 95.92 小时；若不勾选，则剩余工时仍为 26.92 小时。
>!记录删除后不可恢复，请谨慎操作。

