## 功能简介
EdgeOne 以站点 (site，又称二级域名) 为维度提供服务购买和接入，支持如下 2 种 [接入方式](https://intl.cloud.tencent.com/document/product/1145/45967)：
- NS 接入（推荐）：用户将 DNS 解析转移至 EdgeOne，支持一键开启安全/加速服务。
- CNAME 接入：用户维持既有 DNS 服务商，通过在 DNS 服务商处添加指定 CNAME 来开启 EdgeOne 的安全/加速服务。

## NS 接入（推荐）
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**服务概览**。
2. 在服务概览页面，单击右上角的**添加站点**。
3. 在添加站点页面，请输入合法的二级域名，单击**下一步**。
>?站点不可重复添加，如果站点已被其他账户接入，需通过 [站点验证](https://intl.cloud.tencent.com/document/product/1145/45969) 取回站点。

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
4. 在 DNS 配置页面，系统会自动扫描并导入站点的原有 DNS 记录，可以对 DNS 记录进行增删改，并配置 [代理模式](https://intl.cloud.tencent.com/document/product/1145/45968)，单击**下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/aa62a8c7d2247738bd21d85cb370d019.png)
5. 在修改 NS 服务器页面，需要登录站点对应的域名注册商，将 NS 服务器记录修改为 EdgeOne 指定的值。具体操作详情请参见 [NS 修改指南](#NSXG)。
6. 修改后，单击**完成**自动跳转到站点概览页面。
>?NS 记录修改生效时间取决于您的域名注册商，生效后系统会通过邮件/短信/站内信通知。


## CNAME 接入
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**服务概览**。
2. 在服务概览页面，单击右上角的**添加站点**。
3. 在添加站点页面，请输入合法的二级域名，单击**下一步**。
>?站点不可重复添加，如果站点已被其他账户接入，需通过 [站点验证](https://intl.cloud.tencent.com/document/product/1145/45969) 取回站点。

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
5. 在 DNS 配置页面，可以对记录进行增删改，并配置 [代理模式](https://intl.cloud.tencent.com/document/product/1145/45968)，单击**采用 CNAME 接入**。
![](https://qcloudimg.tencent-cloud.cn/raw/93f56859b479d239090ef7f0698057a9.png)
6. 在站点验证页面，按要求在 DNS 服务商处添加一条 TXT 记录，以证明对站点的所有权后，单击**完成验证**。
![](https://qcloudimg.tencent-cloud.cn/raw/c6e5de739623bc1a8758318c9a29665d.png)


## NS 修改指南[](id:NSXG)
1. 确定站点对应的域名注册商并登录。如果不确定您的域名注册商，可前往 [ICANN WHOIS](https://lookup.icann.org/) 查询。
2. 登录后关闭 DNSSEC 配置。
3. 删除原有 NS 配置并修改为 EdgeOne 指定的值。
4. 等待 NS 生效，生效时系统将会通过邮箱/站内信/短信通知

部分域名注册商的配置指导链接：
- [Amazon](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-name-servers-glue-records.html#domain-name-servers-glue-records-adding-changing)
- [GoDaddy](https://sg.godaddy.com/zh/help/change-nameservers-for-my-domains-664)
- [Google Domains](https://support.google.com/domains/answer/3290309?hl%3Den)
- [Name.com](https://www.name.com/support/articles/205934547-changing-nameservers-for-dns-management)
- [Yahoo!](http://support.hostgator.com/articles/how-to-change-name-servers-with-yahoo-com)
