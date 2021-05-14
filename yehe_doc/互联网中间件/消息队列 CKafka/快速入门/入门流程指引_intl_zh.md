根据网络类型不同，CKafka 快速入门的操作流程有一定差异：

- 私有网络访问时，可以选择一个和已有 CVM 相同的私有网络，不需要额外添加路由即可连接到 CKafka 服务。
- 公网路由访问时，需要单独开通一条公网路由，并且对 Topic 进行 ACL 策略的设置。

### 操作流程

![](https://main.qcloudimg.com/raw/30e64181949f2df1bc21cb81dbf2d020.png)

