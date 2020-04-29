This document describes how to create a [callback configuration](https://intl.cloud.tencent.com/document/product/267/31065) in the [LVB Console](https://console.cloud.tencent.com/live). After the configuration is successfully created, you need to associate it with the corresponding push domain name. The association will take effect in about 5–10 minutes. You can also create callback templates for live channels through APIs. 


## Creating a Callback Template
Log in to the LVB Console, select **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)** on the left sidebar, click **+** to create a callback template, enter the callback information in the callback settings pop-up window, and click **Save**.
![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)

>
>- The **callback key** is a user-defined string of up to 32 uppercase and lowercase letters and digits.
>- For more information on how to use a callback key, please see [Event Message Notification Parameter Description](https://intl.cloud.tencent.com/document/product/267/31566).
>- For more information on callback protocol, please see [Event Message Notification Protocol](https://intl.cloud.tencent.com/document/product/267/31566).

## Associating a Domain Name
After creating a callback template, you need to select the corresponding push domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** or click **Manage** on its right and go to **Template Configuration** to specify the callback template for the domain name.
![](https://main.qcloudimg.com/raw/e18e4c7f58950bd2dbe74f038c455cd9.png)

>
>- To unbind the callback configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the APIs related to callback and want to unassociate them, you need to call the [callback template deletion API](https://intl.cloud.tencent.com/document/product/267/30813) to do so.
