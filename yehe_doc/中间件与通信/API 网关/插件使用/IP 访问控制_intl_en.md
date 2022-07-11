## Overview

IP access control is a security protection capability provided by API Gateway. It is mainly used to restrict the source IPs of API callers. You can allow/reject API requests from a certain source by configuring the IP allowlist/blocklist of an API.

>?The original IP access control policy data has been migrated to the IP access control plugin, which can be managed on the [Plugin](https://console.cloud.tencent.com/apigateway/plugin) page.

## Directions

### Step 1. Create the plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. Click **Plugin** on the left sidebar to open the plugin list page.
3. Click **Create** in the top-left corner to create an IP access control plugin.
	![](https://qcloudimg.tencent-cloud.cn/raw/fd057884f8e573035360566d4e79132b.png)

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
    ![](https://qcloudimg.tencent-cloud.cn/raw/29ae4fe59d4d76ad47da75cc819ab600.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.


## PluginData
<dx-codeblock>
:::  json
{
    "type":"white_list",    // IP access control type. Valid values: white_list: allowlist; black_list: blocklist
    "blocks":"1.1.1.1\n1.1.1.0/24"    // IP ranges separated with `\n`
    "descriptions":{"1.1.1.1":"desc", "1.1.1.0/24":"desc"} // IP description, which is optional
}
:::
</dx-codeblock>

## Notes

- The IP access control plugin supports blocklist and allowlist modes. When the allowlist is used, requests from IPs not in the allowlist will be rejected by API Gateway; when the blocklist is used, requests from IPs in the blocklist will be rejected by API Gateway.
- Multiple IPs or CIDR blocks can be entered in the IP access control plugin, which should be separated with semicolons.
- You can add descriptions to IPs in the IP access control plugin in the `descriptions` field, which is optional.


## Limits

Currently, a shared instance does not support access control of client IPs on the **private network**.
