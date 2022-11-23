CSS supports porn detection (based on screenshots). You can configure a screencapture and porn detection template in the console and bind it to a push domain, and CSS will take screenshots of the domain’s streams and perform porn detection on them. The results are saved to Cloud Object Storage (COS). If the push domain is also bound with a callback template, after porn detection is performed, Tencent Cloud will send a request to your server. If your sever passes the authentication, it will receive a JSON packet containing the porn detection callback.
This document describes how to create, bind, unbind, modify, and delete a screencapture and porn detection template in the console.

You can create a screencapture and porn detection template in the following ways:

- Create a template in the CSS console. For details, see [Creating a Screencapture and Porn Detection Template](#Screenshot).
- Call the `CreateLiveSnapshotTemplate` API to create a template. For information on the parameters and request sample, see [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834).


## Notes

- In addition to the porn detection feature, you also need to enable screencapture in the console in order to perform porn detection.
- The screencapture and porn detection features are priced at 0.0176 USD and 0.2294 USD per 1,000 screenshots respectively. For details, see [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607).  
- The screenshots and porn detection results are stored in your COS bucket, which will incur COS storage fees. For more information, see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).
- If you want to store the data in a COS bucket of **another account**, you need to first grant CSS the permission to write to that COS bucket. For more information, see [Authorizing CSS to Store Screenshots in a COS Bucket](https://intl.cloud.tencent.com/document/product/267/33384).
- After creating a template, you can bind it with a push domain name. For more information, see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063). The binding takes effect in about 5-10 minutes. 
- In the console, templates are managed at the domain level. To unbind a screencapture rule that was bound by an API, call [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833).
- Binding, unbinding, or modifying a template affects only new live streams and not ongoing ones. To make the change apply to ongoing live streams, you need to stop them and push them again.

## Prerequisites
- You have activated CSS and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a COS bucket. For detailed directions, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

[](id:Screenshot)
## Creating a Screencapture and Porn Detection Template
1. Log in to the CSS console, and select **Feature Configuration** > [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) on the left sidebar.
2. Click **Create Screencapture and Porn Detection Template**. If it is the first time you do so, click **Authorize Now** to create a service role and grant CSS read and write access to COS so that screenshots can be stored in COS.
![](https://qcloudimg.tencent-cloud.cn/raw/f27be286a9f3c68d96a55544a6c25b57.png)
3. Complete the template settings, and click **Save**.
    <img src="https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png" style="zoom:67%;" />
<table>
<thead><tr><th width="15%">Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Template name</td>
<td>The name of the screencapture and porn detection template, which can contain up to 30 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Template description</td>
<td>The description of the screencapture and porn detection template, which can contain up to 100 letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Screencapture interval</td>
<td>The screencapture interval, which is two seconds by default. Value range: 2-300 (seconds).</td>
</tr><tr>
<td>Intelligent porn detection</td>
<td>Whether to enable intelligent porn detection. If it is enabled, you need to configure a callback template before you can receive porn detection results.</td>
</tr><tr>
<td>Storage Account</td>
<td><b>Current Account</b> or <b>Other Account</b></td>
</tr><tr>
<td>CosAppId</td>
<td>This is required only if you select <b>Other Account</b>. You can view the `APPID` of an account on the <a href="https://console.cloud.tencent.com/developer">Account Information</a> page of the console. To save data to a COS bucket of another account, you need to first grant CSS read and write access to that bucket. For details, see <a href=" https://intl.cloud.tencent.com/document/product/267/33384">Authorizing CSS to Store Screenshots in a COS Bucket</a>.
    </td>
</tr><tr>
<td>Bucket</td>
    <td>Select a <b>COS</b> bucket to which you have granted CSS read and write access.</td>
</tr><tr>
<td>Region</td>
<td>The region of the bucket, which cannot be modified.</td>
</tr><tr>
<td>Folder</td>
<td>Click the box to select a COS folder. The default is <code>{Year}-{Month}-{Day}/</code>.<br>Note: The name of a COS folder can contain only letters, digits, placeholders, and symbols <code>-, !, _, ., *</code>.</td>
</tr><tr>
<td>File name</td>
<td><ul style="margin:0"><li>The format of screenshot filenames. The default is <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>. You can customize your own format:
			<ul style="margin:0">
					<li>{AppName}: push `AppName`</li>
					<li>{PushDomain}: push domain name</li>
					<li>{StreamID}: stream ID</li>
					<li>{Year}: screenshot time (year)</li>
					<li>{Month}: screenshot time (month)</li>
					<li>{Day}: screenshot time (day)</li>
					<li>{Hour}: screenshot time (hour)</li>
					<li>{Minute}: screenshot time (minute)</li>
					<li>{Second}: screenshot time (second)</li>
					<li>{Width}: width of the screenshot</li>
					<li>{Height}: height of the screenshot</li><li>{Ext}: extension (.jpg)</li>
			</ul>
		<li><b>Note: The filename can contain only letters, digits, placeholders, and symbols (-, !, _, ., *).</li>
    <li><b>Example: If the filename format is <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>, a screenshot captured at 14:00:00 on January 1, 2020 would be named <code>2020010114.jpg</code> in COS.</li></ul></td>
</tr>
</tbody></table>

[](id:conect)
## Binding a Domain Name

1. Log in to the CSS console, and select **Feature Configuration** > [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) on the left sidebar.
2. Bind a domain name in either of two ways:
    - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
    ![](https://qcloudimg.tencent-cloud.cn/raw/92b7542783d6d5ac59ef5faedbf53746.png)
    - **Bind a domain name after creating a screencapture and porn detection template:** After successfully [creating a screencapture and porn detection template](#Screenshot), click **Bind Domain Name** in the pop-up window.
    ![](https://qcloudimg.tencent-cloud.cn/raw/61c40816a357ce0f79677e238a1a31ba.png)
1. Select a **screencapture and porn detection template** and a **push domain** and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/5e632f4a7712256fdd3f3a282e09a9c7.png)
>? You can click **Add** to bind multiple push domains to a template.

[](id:unite)
## Unbinding a Domain Name

1. Log in to the CSS console, and select **Feature Configuration** > [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) on the left sidebar.
2. Select the target screencapture and porn detection template, find the domain you want to unbind, and click **Unbind**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e8a52af13916db8d50bc4395cfc5cc8d.png)
3. In the pop-up window, click **Confirm**.
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)

[](id:change)
## Modifying a Template

1. Select **Feature Configuration** > [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) on the left sidebar.
2. Select a screencapture and porn detection template and click **Edit** on the right to modify it.
3. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/786b4fd9630a178a0aebb65cda16a49c.png)

[](id:delete)
## Deleting a Template
>! If a template has been bound to domains, you need to [unbind](#unite) them before you can delete the template.

1. Select **Feature Configuration** > [Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh) on the left sidebar.
2. Select a screencapture and porn detection template and click **Delete** in the top right.
3. In the pop-up window, click **Confirm**.

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)

## More
For more information about **binding** and **unbinding a domain name**, see [Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31063).