本文为您详细介绍在 CODING 中持续部署的基本操作。

## 前提条件
使用 CODING 项目管理的前提是，您的腾讯云账号需要开通 CODING DevOps 服务。 


## 进入项目
1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击工作台首页左侧的 <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" width="15"style ="margin:0" data-nonescope="true">，进入持续部署控制台。

## 功能介绍[](id:intro)
CODING 持续部署用于把控构建之后的项目发布与部署交付流程。能够无缝对接上游 Git 仓库、制品仓库以实现全自动化部署。在稳定的技术架构、运维工具等基础上，具备蓝绿发布，灰度发布（金丝雀发布），滚动发布，快速回滚等能力。
下文将以一个简单的 Demo 项目为例，演示如何使用 CODING 持续部署控制台将应用发布至腾讯云集群。

## 前置准备[](id:prepare)
-   开启持续部署部署设置权限。
-   一个可被 CODING 持续部署访问的 Kubernetes 集群，单击了解如何申请 [腾讯云标准集群](https://intl.cloud.tencent.com/document/product/457/40029)。
-   导入 [示例代码库](https://codingtest-cd.coding.net/public/k8sdemo/k8sDemo/git/files)。
-   Docker 制品仓库，单击了解如何使用项目中的 [Docker 制品仓库](https://intl.cloud.tencent.com/document/product/1136/44806)。

## 操作步骤
### 步骤1. 获取并关联云账号[](id:1)
因使用了腾讯云容器服务，部署后应用将发布至集群，本示例使用的团队账号已在**团队管理**>**服务集成**中关联腾讯云账号。
1. 单击首页左侧的**部署控制台**，在**云账号**中绑定腾讯云账号。云账号名称可以自拟，选择地域后将自动获取对应集群。
![](https://qcloudimg.tencent-cloud.cn/raw/764a28af113f4691251467f6efbfd7ad.png)
2. 自动生成的制品仓库访问凭证将存储于**命名空间**，您可以在腾讯云控制台中新建。
![](https://qcloudimg.tencent-cloud.cn/raw/da95fb2b4079fa3495b5776cb1224154.png)

### 步骤2. 配置应用[](id:2)
1. 成功添加云账号后，在部署控制台中单击**创建应用**，填写应用名与选择部署方式。
![](https://qcloudimg.tencent-cloud.cn/raw/28707631e7fdbcf3ff51aa88ce576ee3.png)
2. 选择**部署到 Kubernetes 集群**模板，填写名称与描述后完成创建。
![](https://qcloudimg.tencent-cloud.cn/raw/c67591415744e58508062badd7a321da.png)

### 步骤3. 初始化项目[](id:3)

1. 此步骤主要用于配置持续部署所涉及代码仓库与制品仓库。在**代码仓库**中点选导入外部仓库，访问 [示例仓库](https://codingtest-cd.coding.net/public/k8sdemo/k8sDemo/git/files) 并克隆仓库地址。
![](https://qcloudimg.tencent-cloud.cn/raw/2b431e19fc2c44be9f6830052ed364fe.png)
2. 导入完成后进行制品管理，将拟发布的 Docker 制品托管至 CODING 制品仓库，详情请单击 [参考阅读](https://intl.cloud.tencent.com/document/product/1136/44806)。
![](https://qcloudimg.tencent-cloud.cn/raw/ce33728700f2a7a808a48c773f631a75.png)
3. 推送至制品仓库后，获取制品的拉取地址并填写至代码仓库中 `/k8s/deployment.yaml` 中的 `image` 地址。
![](https://qcloudimg.tencent-cloud.cn/raw/7dcdefc706453b3df42f4dfd62947922.png)
4. 接下来需导入云账号的 `imagePullSecrets` 至代码仓库中。在**部署控制台** > **云账号**中单击查看详情后，复制名称。
5. 粘贴至代码仓库中的 `deployment.yaml` 文件中，同时需注意 `namespace` 内容是否与上文中指定的**命名空间**一致。
![](https://qcloudimg.tencent-cloud.cn/raw/9dfe5113d33b4f20966ad0272ea72c31.png)
6. 同一层级的 `service.yaml` 文件中的 `namespace` 内容也需保持一致。
![](https://qcloudimg.tencent-cloud.cn/raw/aa04ad06c0cc6d052a1d834e0e3b407f.png)

### 步骤4. 配置部署流程[](id:4)

进入部署流程配置页面，可以为此流程设定：
-   流程的执行选项（在此示例中保持默认即可）。
-   部署 Deployment 阶段以及部署 Service 阶段所需制品。
-   手动或自动触发。


1. 首先配置部署（Manifest）阶段。基础设置选择已绑定的云账号，在 Manifest 来源选择 **CODING 代码库**，填写相应的路径，镜像版本配置选择自动获取。
![](https://qcloudimg.tencent-cloud.cn/raw/55d038795fb48a4b4966fd2f70773f6d.png)
2. 配置部署 Service 阶段时步骤同上，但在文件路径处选择 `k8s/service.yaml` 文件。

### 步骤5. 触发器配置[](id:5)
1. 完成部署阶段配置后，您可以使用自动化触发器、手动提交发布单执行部署。
<dx-tabs>
::: 自动触发
在**基础配置**中点选触发器类型，选择 Docker 仓库触发器。当开发人员更新代码仓库并使用 CI 将镜像打包推送至制品库后，Docker 镜像版本的更新将自动触发部署流程并将应用发布至 Kubernetes (TKE) 集群，完成后可以在基础设施页面查看并确认应用是否发布成功。
![](https://qcloudimg.tencent-cloud.cn/raw/459a73afc64c300907372044a9823007.png)
:::
::: 手动提交发布单
若希望通过手动提交发布单的形式触发部署流程，那么可以将**应用**（如本范例的 flaskapp ）与项目关联。在部署控制台的**应用列表**中搜索项目名称进行关联：
![](https://qcloudimg.tencent-cloud.cn/raw/5c22157dfe7c90516aae9b949b7194ea.png)
:::
</dx-tabs>

2. 关联完成后，单击项目中的**持续部署** > **Kubernetes** 手动提交发布单。
![](https://qcloudimg.tencent-cloud.cn/raw/4f2483a7e0bc58b15012d60ca5559f02.png)

### 步骤6. 发布完成[](id:6)
1. 发布成功后，可以查看发布的制品及启动参数及阶段执行详情等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/29f95fba22e096ae5b5e9258a21f6caf.png)
2. 当需要查看某个资源在集群中的运行状态时，单击**集群**下的工作负载即可查看详情（如工作负载的 Pod 实例，日志等信息）。
![](https://qcloudimg.tencent-cloud.cn/raw/cee587b1f8a590293a340231647720d8.png)
3. 在腾讯云的容器服务中查看工作负载。
![](https://qcloudimg.tencent-cloud.cn/raw/a9f12cee9a5f9b615d981ca5dc50a0a0.png)
