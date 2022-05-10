This document shows you how to configure an IP allowlist/blocklist to filter requests and control access to streaming content.

## Overview
- IP **allowlist**: Only IP addresses on the list can access your streaming content.
- IP **blocklist**: IP addresses on the list cannot access your streaming content.

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:set)
## Configuring IP Allowlist/Blocklist
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, and click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. Click **Access Control** and find **IP Allowlist/Blocklist**.
![](https://qcloudimg.tencent-cloud.cn/raw/de64819fab139753ecde2ee7f20a5f63.png)
3. Click ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png) to enable IP allowlist/blocklist and complete the following settings:
![](https://qcloudimg.tencent-cloud.cn/raw/a9cc1a4e8f9485c9fb057c0edaba177b.png)

<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Authenticate By</td>
<td>Allowlist or blocklist:<ul style="margin:0">
<li>You cannot select both.</li>
<li>If you configure an allowlist, only IP addresses on the list will be able to access your streaming content.</li>
<li>If you configure a blocklist, IP addresses on the list cannot access your streaming content.</li></ul></td>
</tr><tr>
<td>IP List</td>
<td>You can add up to 200 items. Separate them with line breaks.<ul style="margin:0">
<li>Supports IP addresses and CIDR (/8/16/24) but not port numbers.</li>
<li>Does not support IPv6 currently.</li></ul></td>
</tr>
</tbody></table>

4. Click **Save** to save the configuration (it takes a while for the configuration to take effect).
![](https://qcloudimg.tencent-cloud.cn/raw/8a0bf90247475062eef4aa43d34eb08f.png)

[](id:change)
## Modifying IP Allowlist/Blocklist Configuration
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, and click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. Click **Access Control** and, in the **IP Allowlist/Blocklist** area, click **Edit**.
3. Modify the configuration and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f60c0cdf3fe6cb94f15867f349bc4cc3.png)

[](id:close)
## Disabling IP Allowlist/Blocklist
Follow the steps below to disable IP allowlist/blocklist:
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, and click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. Click **Access Control** and find **IP Allowlist/Blocklist**.
3. Click ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) to disable IP allowlist/blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/226d47604696996735ec23b887931d35.png)
