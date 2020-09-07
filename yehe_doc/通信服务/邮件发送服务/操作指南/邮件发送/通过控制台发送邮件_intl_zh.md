## 通过控制台发送邮件
**邮件发送任务列表**

在[邮件发送服务控制台](https://console.cloud.tencent.com/dms)中的 【邮件发送】 页面，您可以查看所有通过控制台发送的邮件发送任务。发送任务列表展示了每个发送任务的详细信息，包括任务名称、调用模板名称、发信地址、发送状态、请求数量和创建时间。

单击 【普通邮件】和 【模板邮件】 可以分类查看普通邮件发送任务和模板邮件发送任务。
[![Image from Gyazo](https://i.gyazo.com/e79ccf1900a81b7db0c90a54495cfeea.png)](https://gyazo.com/e79ccf1900a81b7db0c90a54495cfeea)

**通过控制台发送模板邮件**
通过使用邮件模板发送邮件，每一个收件人都可以收到个性化的邮件内容。在发送模板邮件前，请确认您已创建邮件模板并且有通过验证的发信域名。
[![Image from Gyazo](https://i.gyazo.com/2d440a7219febdd330abf2d6b083cb6f.png)](https://gyazo.com/2d440a7219febdd330abf2d6b083cb6f)
1. 登录[腾讯云 DMS 控制台](https://console.cloud.tencent.com/dms)。
2. 在左侧导航栏中单击 【邮件发送】，进入 【邮件发送】 页面。
3. 单击 【发送模板邮件】，进入模板邮件内容编辑页面，输入或上传任务名称、收件人地址、发信地址、发信人名称以及回信地址。
4. 选择模板来源，上传模板自定义值的JSON文件，有关JSON文件的格式要求，请参见[邮件模板相关问题](https://intl.cloud.tencent.com/document/product/1070/38234)。
5. 确认内容无误后，单击 【确定】。

新的模板邮件发送任务将被添加在邮件任务列表中，发送完毕后，您可以查看任务总请求数和成功数。

**通过控制台发送普通邮件**
有关如何通过控制台发送普通邮件，请前往[通过控制台发送普通邮件](https://intl.cloud.tencent.com/document/product/1070/38226)。