## 功能简介
腾讯云 Web 应用防火墙 IP 管理功能，对经过 Web 应用防火墙防护域名的访问源 IP 进行状态查询和黑白名单设置，主要功能包括：IP 查询，IP 黑白名单设置和 IP 封堵状态查询。
- IP 查询，查询输入 IP 在防御域名中状态信息，包括是否在黑白名单中，是否处于封堵状态。
- IP 黑白名单设置，支持设置基于域名或全局的 IP 黑白名单规则。
- IP 封堵状态，实时查看 CC 攻击、自定义策略人机识别等源 IP 封堵状态信息。

## 配置步骤
- #### **示例一 IP 查询**
1.进入 [腾讯云 Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，选择【IP 管理】>【IP 查询】输入需要查询的 IP 地址查看该 IP 状态。
![](https://main.qcloudimg.com/raw/21cb18626590f9463c60a73bbabdeebf.png)
2.查询出的 IP 地址，可手动添加黑白名单。
![](https://main.qcloudimg.com/raw/20dcb9a1f8779f0541a903081d700880.png)
- #### **示例二 添加 IP 黑名单**
1.进入 [腾讯云 Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，选择【IP 管理】>【IP 黑白名单】进入配置页面。
>IP 黑名单名单模块，可以添加基于域名的黑白名单或基于全局的黑白名单，生效优先级说明说如下：
 >- 黑白名单的优先级仅低于 Web 应用防火墙自定义放行策略，高于其他检测逻辑。
 >- IP黑白名单优先级从高到低顺序：全局白名单>域名白名单>域名黑名单>全局黑名单。

![](https://main.qcloudimg.com/raw/dad2779730036766a6ce098f635731d2.png)
**配置项说明：**
类别：黑名单、白名单。
来源：CC 防护、自定义规则。
高级筛选：利用创建时间和有效截止时间进行 IP 信息筛选。

2.添加黑白名单。左上角选择需要添加防护的域名，单击【添加黑白名单】，选择黑名单添加需要加黑的 IP 地址。
![](https://main.qcloudimg.com/raw/61dbd125fcd2dd8803e7f7ac7a72779d.png)

>选择域名为 ALL 时，添加的 IP 黑白名单为全局的黑白名单。

3.黑白名单支持导入和筛选结果导出，导入 IP 信息时，请参考导出格式。
![](https://main.qcloudimg.com/raw/3786459fe465cda4a68126f575f8522f.png)
4.添加完成后，可以在 IP 查询中输入添加的源 IP，查询状态信息。
- #### **示例三 IP 封堵状态查询**
进入 [腾讯云 Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，选择【IP 管理】>【IP 封堵状态】进入查询页面，可以查询自定义规则、CC 防护模块拦截的 IP 信息。可对查询结果进行导出，对单个 IP 进行加黑加白操作。
![](https://main.qcloudimg.com/raw/ae0c778891b8fb748345458709ca6300.png)


