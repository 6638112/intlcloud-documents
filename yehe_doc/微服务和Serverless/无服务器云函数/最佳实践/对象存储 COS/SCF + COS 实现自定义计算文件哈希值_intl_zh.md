## 概述

数据在客户端和服务器间传输时可能会出现错误，对象存储（Cloud Object Storage，COS）结合云函数（Serverless Cloud Function，SCF）可以通过数据校验的方式保证上传数据的完整性，例如 MD5 码校验。用户在 COS 上传文件过程中，SCF 将帮助校验用户上传的对象，保证上传数据的完整性与正确性。

## 实践背景

业内现存公有云对象存储服务均不存在 MD5 码，用户上传文件后可能会出现以下情况：

- 文件重复、成本上升
- 文件错误、降低业务效率
- 文件缺失


## 方案优势

- 可视化操作：一键配置，简化开发流程，无需编码工作，大幅提升研发效率
- 多样化选择：支持 MD5 、SHA1 、SHA256、CRC64，满足各场景用户需求
- 自动化执行：文件上传到 COS 后，即可触发工作流开始计算校验码


## 操作步骤

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。
2. 创建工作流，自定义格式过滤规则，及创建自定义函数节点。详细操作请参见 [配置工作流](https://intl.cloud.tencent.com/document/product/436/46408)。
![](https://qcloudimg.tencent-cloud.cn/raw/9d4a303445da7e91b5e5dd9cd42585c8.png)
3. 在函数节点弹窗中，单击**新增函数**。 
3. 在 SCF 的创建页面，选择**计算COS对象的哈希值**模板。
![](https://qcloudimg.tencent-cloud.cn/raw/dda0680b33565addb4973207941cb6b2.png)
4. 根据用户文件大小，在基础配置项中配置执行超时时间，在高级配置中配置足够的内存。
5. 配置函数代码，该函数模板支持以下两个环境变量：
  - hashTypeList 指定要计算的算法，该项为可选，默认为["crc64", "md5", "sha1", "sha256"]。
  - caseType 指定哈希值大小写，该项为可选，默认为 lowercase，可以传入 uppercase。
6. 启用权限配置，绑定包含当前存储桶读写权限的角色，创建运行角色请参见 [角色与策略](https://intl.cloud.tencent.com/document/product/583/38176)。
7. 单击**完成**。
8. 返回刚才的工作流页面，选中刚创建的自定义转码函数，并保存工作流。
![](https://qcloudimg.tencent-cloud.cn/raw/86cd43267e8e9a1e84ba7e5227be7f25.png)
9. 上传文件，待工作流处理成功后，即可看到上传的文件已成功添加多个哈希头部。
![](https://qcloudimg.tencent-cloud.cn/raw/b87689705cd3382098796383e2876400.png)  



