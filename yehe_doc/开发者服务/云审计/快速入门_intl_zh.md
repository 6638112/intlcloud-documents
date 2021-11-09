您可以通过腾讯云控制台快速了解云审计服务。通过控制台，您可以查看操作记录，创建一个跟踪集并编辑其存储位置，还可以对已创建的跟踪集进行删除操作，以及关闭跟踪集记录日志。


## 注册与登录
- 如果您还没完成腾讯云账户的注册，请先 [注册](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F%3FfromSource%3Dgwzcw.184926.184926.184926%26gclid%3DEAIaIQobChMIoaGVwcT21gIVFSNoCh3VxAi-EAAYASAAEgId7PD_BwE)，注册完成后您需要进行实名认证，具体操作可参考 [实名认证指引](https://intl.cloud.tencent.com/document/product/378/3629)。
- 如果您已注册腾讯云账户，并进行了实名认证，可直接登录 [腾讯云](https://console.cloud.tencent.com/)， 选择**云产品** > **管理与审计** > **云审计**，进入云审计页面。

##  查看操作记录
### 列表
1. 登录 [云审计控制台](https://console.cloud.tencent.com/cloudaudit)。
2. 在左侧导航中，单击**操作记录**，进入操作记录页面。
3. 在操作记录页面中，您可以根据用户名称、操作类型、资源事件名称、资源名称、请求 ID 、API 错误码、密钥 IP 及对应操作事件时间，获取相关的操作记录信息，您需要查询的操作记录将会以列表的形式展示出来，默认情况下只展示部分数据。

### 详情
您在获取到相关的操作记录列表后，如果想更进一步了解单个操作记录，可以单击该操作记录左侧的 <img src="https://main.qcloudimg.com/raw/be1649be0251749641c35e81db22535e.png" style="margin:-3px 0px;">，您就会得到此操作记录的详情，包括事件时间、用户名、事件名称、访问密钥、事件 ID、源 IP 地址、资源区域、CAM 错误码、事件区域、 事件源、请求 ID。同时，可以单击**查看事件**，进行了解事件的相关信息。如下图所示：
![](https://main.qcloudimg.com/raw/48d2fabf59096d2839b7924dadfd7394.jpg)

## 使用跟踪集
1. **创建跟踪集**
 1. 登录 [云审计控制台](https://console.cloud.tencent.com/cloudaudit)，选择左侧导航栏中的**跟踪集** > **创建**，进入跟踪集创建页面。 
 2. 在“跟踪集”页面中，单击**创建**。如下图所示：
![](https://main.qcloudimg.com/raw/ee793193029d08b873d46186b98039df.jpg)
<dx-alert infotype="notice" title="">
最多支持创建5个跟踪集。
</dx-alert>
 2. 在页面上填写跟踪集名称、存储位置等相关信息，单击**完成新建**即可。如下图所示：
![](https://main.qcloudimg.com/raw/022556d2c29e653523f5d5d4615683cf.jpg)
2. **关闭或开启跟踪集记录日志**
 1. 当您成功创建跟踪集后，跟踪集的状态显示默认为**开启**。如下图所示：
![](https://main.qcloudimg.com/raw/653c413004625b1add79a1eb4d6b5c3d.jpg)
 2.  单击“名称”下的跟踪集名称，或跟踪集所在行右侧的**编辑**，进入跟踪集详情页面。如下图所示：
![](https://main.qcloudimg.com/raw/76376149a048ab52a7ce479287573a0a.jpg)
 3.  单击页面右上角“开启日志记录”右侧的 <img src="https://main.qcloudimg.com/raw/9d9892843390a003afe42d52123fd500.png" style="margin:-3px 0px">（图示为开启状态），即可**关闭或开启**跟踪集记录日志。
3. **投递存储位置**
单击跟踪集详情页面“投递位置”中的**编辑**，可以选择投递存储桶（COS）或者投递到日志服务（CLS），编辑完成后单击**保存**即可。如下图所示：
![](https://main.qcloudimg.com/raw/1f720f70cccb6daf0e7bcea5affc8aba.jpg)
4. **删除跟踪集**
在“跟踪集”页面中，单击跟踪集所在行右侧的**删除**，或在跟踪集详情页面单击**删除跟踪集**即可。

