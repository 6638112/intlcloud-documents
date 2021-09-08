## 操作场景

本文以 Java 开发的 Demo 应用程序，采用 JAR 包上传部署方式，向您展示如何将您的应用部署在弹性微服务上，并使其可以被公网访问。

## 前提条件

请确保在开始部署您的应用前，已经阅读和完成了 [准备工作](https://intl.cloud.tencent.com/document/product/1094/41383)。


## 操作步骤

### 步骤1：获取 Demo 应用

本文以 Java Spring Boot 开发的 Demo 应用为例，[点击下载应用 JAR 包](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/hello-world-0.0.1-SNAPSHOT.jar)。



### 步骤2：部署应用

1. 在弹性微服务控制台的【[应用管理](https://console.cloud.tencent.com/tem/application)】页面上方，选择应用部署地域。
2. 单击【新建】，进入新建应用页面，填写应用信息。
     ![](https://main.qcloudimg.com/raw/ee456bf7ffe1fe15554ec3399df840fe.png)
3. 选择您应用的开发语言和程序包上传方式。
   - Java 语言支持上传镜像、JAR 包和 WAR 包，其他语言只支持镜像上传。
   - 如果您在继续新建应用时选择**镜像 > 自动创建**的方式上传程序包，您上传的镜像将被推送至一个 TEM 自动创建的**命名空间**。
   - 如果您在继续新建应用时选择 **JAR包**或 **WAR包**的方式上传程序包，TEM 会自动为您构建容器镜像，并将其推送至 TEM 创建的**命名空间**。
>?如果您还未配置**容器镜像仓库**，或者在点击【下一步】时出现报错，请参考 [开通镜像仓库](https://intl.cloud.tencent.com/document/product/1094/41386)。

4. 单击【提交】，并在弹框中单击【确定】，前往部署应用。
5. 在部署应用页面，根据您的应用具体情况配置相关参数。
   ![](https://main.qcloudimg.com/raw/5cde618b2418fca282ad75ac56f8dcd0.png)
   - 上传程序包：上传您的程序包。
   - 发布环境：选择刚刚创建好的环境。
   - 如果您的应用需要配置其他高级选项，请参考 [创建并部署应用](https://intl.cloud.tencent.com/document/product/1094/40362)。
6. 单击【部署】，完成普通应用的部署。



### 步骤3：验证访问

应用部署成功后，需要为其在环境中创建访问配置，以通过公网访问该应用。

1. 在弹性微服务控制台的【[环境](https://console.cloud.tencent.com/tem/env)】页面上方，选择应用部署地域。

2. 单击您应用所部署的环境，进入详情页面，并在上方选择【访问配置】。

3. 单击【新建】，进入新建访问配置页面，填写访问配置信息。
   ![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)

   - 网络类型：公网访问。如需环境内访问，请参考 [创建并部署应用](https://intl.cloud.tencent.com/document/product/1094/40362)。
   - 负载均衡器：自动创建。
   - 协议及端口：支持 HTTP:80 和 HTTPS:443，支持 HTTPS 域名绑定证书。Demo 应用请选择HTTP:80。
   - 转发配置：
     - 域名：支持绑定已有域名，如果没有域名，则默认为您分配 IPv4 IP。Demo 应用请使用默认分配 IP。
     - 路径：默认为“/”，根据实际情况进行配置。
     - 后端应用：选择您部署的 Demo 应用。
     - 应用端口：Demo 应用请使用8201端口。
   - 服务器证书：选择 HTTP 协议时，需选择服务器证书，如现有的证书不合适，可前往 [新建服务器证书](https://console.cloud.tencent.com/clb/cert)。

4. 单击【确认】，完成新建访问配置。您可以在环境详情页中的【访问配置】下，查看应用的公网访问 IP。
   ![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)

5. 在浏览器中输入您的公网访问 IP，如果返回以下结果，则说明应用部署成功。

   ```plaintext
   	Hello World!
   ```
