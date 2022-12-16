For Android phones, the opened badge capabilities vary by vendor. The support of Tencent Push Notification Service for push badge is as detailed below for your reference.

## Overview

| Vendor | Support for Display of Badge/Red Dot | Require Configuration | Badge/Red Dot Display Rule                                                     |
| ---- | --------------------- | ------------ | ------------------------------------------------------------ |
| Huawei/HONOR | Badge              | Yes           | See [Huawei Phone Badge Adaptation Guide](#huawei).                               |
| Mi | Badge              | No           | Compliant with the default system logic. Perceive the number of notifications in the notification bar and automatically increase or decrease the badge number by 1 accordingly.          |
| Meizu | Red dot              | No           | Compliant with the default system logic. Supports only red dot display. If there is a notification, a red dot will be displayed, and vice versa.   |
| OPPO | Red dot              | No           | Display of red dot needs to be manually enabled in notification settings, which is compliant with the default system logic. If there is a notification, a red dot will be displayed, and vice versa.<br>Display of the notification number is available only to specified applications such as QQ and WeChat and requires permission application. No adaption instructions are provided currently. |
| vivo | Badge              | Yes           | See [vivo Phone Badge Adaptation Guide](#vivo).                             |



## Configuring the Server Delivery Badge

You can configure the server delivery badge in the Tencent Push Notification Service console or through the push API.

<dx-tabs>
::: Method 1: Configure on the push page in the console
1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns).
2. Locate the target Android product and click **Push Management** in the **Operation** column of the product to go to the push **Task List** page.
3. Click the push to configure to go to the push configuration page.
4. In the **Advanced settings** area, enable badge number.
  ![]()
  :::
  ::: Method 2: Configure through the push API
    In the push message body, add the `badge_type` field with the following attributes under `body.message.android`.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Parent Item</th>
<th>Required</th>
<th>Default Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>badge_type</td>
<td>int</td>
<td>android</td>
<td>No</td>
<td>-1</td>
<td>Notification badge:<li>-2: auto increased by 1 (for Huawei devices only)<li>-1: unchanged (for Huawei and vivo devices only)<li>[0, 100): direct configuration (for Huawei and vivo devices only)</td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="">
Badge adaptation capabilities vary by vendor device. For details, see the badge adaptation description of each vendor below.
</dx-alert>
Sample message body:
<dx-codeblock>
:::  json
{
	"audience_type": "token",
	"expire_time": 3600,
	"message_type": "notify",
	"message":{
			"android": {
					"badge_type": -2,
					"clearable": 1,
					"ring": 1,
					"ring_raw": "xtcallmusic",
					"vibrate": 1,
					"lights": 1,
					"action": {
							"action_type": 1,
							"activity": "com.qq.xg4all.JumpActivity",
							"aty_attr": {
							"if": 0,
							"pf": 0
					}
					}
			},
			"title": "android test",
			"content": "android test 21"
	},
	"token_list": [
		"01f6ac091755a79015b4a30c9c4c7ddba1ea"
	],
	"multi_pkg": true,
	"platform": "android",
}
:::
</dx-codeblock>
:::
</dx-tabs>





## General APIs for Terminals

#### API for setting the badge number (for SDK v1.2.0.1 or later)

This API allows you to set the badge number. It applies to Huawei, OPPO, and vivo phones. For OPPO phones, you need to apply for the badge display permission from OPPO.

```java
/**
 * @param context   //Application context
 * @param setNum   //Set the badge number
 * @since v1.2.0.1
 */
XGPushConfig.setBadgeNum(Context context, int setNum);
```

Example: When an in-app message is received, call `XGPushConfig.setBadgeNum(context, 8)` to set the badge number to 8.


#### API for resetting the badge number (for SDK v1.2.0.1 or later)

This API allows you to reset the badge number. It applies to Huawei, OPPO, and vivo phones. For OPPO phones, you need to apply for the badge display permission from OPPO.

```java
	/**
	 * @param context   //Application context
	 * @since v1.2.0.1
	 */
	XGPushConfig.resetBadgeNum(Context context);
```

Example: When an in-app message is read or an application is opened, call `XGPushConfig.resetBadgeNum(context)` to reset the badge number.

>!  For notifications delivered through vendor channels, the badge number cannot be automatically decreased by 1 when the notifications are cleared. It is recommended that you call this API to clear the badge value when appropriate, for example, when re-opening the application from the desktop.
>

## Huawei Phone Badge Adaptation Guide[](id:huawei)

### Use limits

Badge display is supported by Huawei phones on EMUI 8.0 or later.
Limited by the openness of Huawei phone badge capabilities, the badge feature varies by push scenario as detailed below. Please use the Huawei phone badge feature as instructed.

|   Push Form    |                           Badge Capability                           |             Implementation Method             |
| :-----------: | :----------------------------------------------------------: | :------------------------------: |
| Notification through the Huawei channel  | The badge number can be auto increased by 1, directly configured, or unchanged; can be auto decreased by 1 for notification click; but cannot be auto decreased by 1 for notification dismissal. | Configure in the console or through the push API keyword. |
| Notification through the Tencent Push Notification Service channel | The badge number can be auto increased by 1, directly configured, or unchanged; can be auto decreased by 1 for notification click or dismissal. | Configure in the console or through the push API keyword. |
|   In-app message    |                 You can process the badge number configuration, increase, and decrease logic by yourself.                 |      Call the open API of the Tencent Push Notification Service SDK.      |

### Configuration

#### Applying for permission to set the in-app badge

To implement the correct badge modification effect, please first add the Huawei phone badge read/write permission for your application by adding the following permission configuration under the `manifest` tag in the `AndroidManifest.xml` file of the application:

```xml
<uses-permission android:name="com.huawei.android.launcher.permission.CHANGE_BADGE" />
<!-- Compatible on HONOR phones -->
<uses-permission android:name="com.hihonor.android.launcher.permission.CHANGE_BADGE" />
```

#### Setting the notification delivery badge

Be sure to enable the Huawei channel in the console and enter the `Activity` class, such as `com.test.badge.MainActivity`, of the application entry corresponding to the desktop icon in the parameter configuration area. Otherwise, the badge settings will not take effect. ![]()

#### Getting startup class name:
Drag and drop the packaged APK file into AndroidStudio. Enter the `AndroidManifest.xml` file in the package and search for the keywords "android.intent.category.LAUNCHER" in the file. The `activity.name` attribute found is the startup class name.
![](https://qcloudimg.tencent-cloud.cn/raw/5703361b634478552045b0f0f706263f.png)


#### Setting badge number auto increase/decrease for Huawei phones

For Huawei phones, the badge number can be auto increased or decreased by 1. The API is as follows:

```java
	/**
	 * Huawei phone badge modification API
	 *
	 * @param context   //Application context
	 * @param changeNum   //Changed number, which is incremental. For example, if the previous badge number is 5 and this input parameter is 1, the badge number will be set to 6. 
	 *Valid values: 1 (badge number increased by 1); -1 (badge number decreased by 1)
	 */
	XGPushConfig.changeHuaweiBadgeNum(Context context, int changeNum);
```

Example: when an in-app message is received, call `XGPushConfig.changeHuaweiBadgeNum(context, 1)` to increase the badge number by 1; when the message badge needs to be dismissed, call `XGPushConfig.changeHuaweiBadgeNum(context, -1)` to decrease the badge number by 1.



## vivo Phone Badge Adaptation Guide[](id:vivo)

### Use limits

Limited by the openness of vivo phone badge capabilities, the badge number currently can only be directly configured but cannot be auto increased or decreased. The badge feature supports only notifications delivered through the Tencent Push Notification Service channel.

|   Push Form    |                           Badge Capability                          |             Implementation Method             |
| :-----------: | :------------------------------------: | :------------------------------: |
| Notification through the vivo channel |                 Not supported                |              Not supported              |
| Notification through the Tencent Push Notification Service channel | The badge number can be directly configured or unchanged, but cannot be auto increased or decreased. | Configure in the console or through the push API keyword. |
|   In-app message    |                 You can process and configure the logic by yourself.                 |      Call the open API of the Tencent Push Notification Service SDK.      |

### Configuration

#### Applying for permission to set the in-app badge

To implement the correct badge modification effect, please first add the vivo phone badge read/write permission for your application by adding the following permission configuration under the `manifest` tag in the `AndroidManifest.xml` file of the application:

```xml
<uses-permission android:name="com.vivo.notification.permission.BADGE_ICON" />
```

#### Enabling badge in phone settings

After successful permission configuration, the **Badge** option is disabled by default and needs to be manually enabled.
Enablement path: **Settings** > **Notification & Status Bar** > **Notifications Management** > **Application Name** > **Badge**
For applications without the badge feature, the **Badge** option is not provided.

>?For different OS versions, the name **Badge** can also be **App icon badges** or **Desktop badges**.
