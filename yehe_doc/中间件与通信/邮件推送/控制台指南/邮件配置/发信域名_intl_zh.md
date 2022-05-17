## 操作场景
通过邮件推送控制台，您可以配置发信域名的操作。本文将为您介绍如何新建发信域名。

## 前提条件
- 您必须对发信域名拥有管理权限。
- 如果您的域名托管在腾讯云，请进入 [DNS 解析 DNSPod ](https://console.cloud.tencent.com/cns) 配置。如果您的域名托管在其它域名服务商，请自行按照清单详情来配置。

## 操作步骤
1. 登录 [邮件推送控制台](https://console.cloud.tencent.com/ses/domain)，选择**邮件配置**>**发信域名**，进入“发信域名” 配置页面，单击**新建**。
![](https://qcloudimg.tencent-cloud.cn/raw/50a47b56343acb2cb2289f705bd7514e.png)
2. 进入新建发信域名配置，请输入您的域名地址，单击**提交**即可完成保存。
![](https://qcloudimg.tencent-cloud.cn/raw/7e53b2e8ecfaf818c8cb56bb38b9ed4e.png)
3. 返回到“发信域名”配置界面，对域名完成验证后才可以使用该域名发送邮件，验证方法请参见 [身份验证和配置相关问题](https://intl.cloud.tencent.com/document/product/1084/42371)。
![](https://qcloudimg.tencent-cloud.cn/raw/040ac5bd4115f1739c65e01629a5f51b.png)
<table>
   <tr>
      <th width="0px" >属性</td>
      <th width="0px" >含义</td>
   </tr>
   <tr>
      <td>发信域名</td>
      <td>配置的发信域名地址</td>
   </tr>
   <tr>
      <td>状态</td>
      <td>待验证：需要验证通过才可以通过此域名发送邮件。<br>已验证：已完成验证后，此域名具备发送邮件的使用条件。</td>
   </tr>
   <tr>
      <td>操作</td>
      <td>如状态为待验证，您可单击<b>验证</b>进行修改，或者单击<b>删除</b>移除该条发信域名配置。</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
- 不可使用企业邮箱域名，以免产生 SPF、MX 记录的冲突。
- 如果您需要更换发信域名，请[提交工单](https://console.cloud.tencent.com/workorder/category)。
</dx-alert>

