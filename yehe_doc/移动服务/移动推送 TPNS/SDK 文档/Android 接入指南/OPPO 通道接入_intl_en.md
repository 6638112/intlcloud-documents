

## Overview
The OPPO channel is a system-level push channel officially provided by OPPO. On an OPPO phone, push messages can be delivered through OPPO's system channel without opening the application. For more information, please visit [OPPO PUSH's official website](https://push.oppo.com/).


>?
>- The OPPO channel currently does not support in-app messages, which will be delivered through the TPNS channel.
>- The OPPO channel imposes a certain quota limit on the number of daily push messages. For more information, please see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829). When this limit is exceeded, excessive messages will be pushed through the TPNS channel.
>- The OPPO channel is supported by OPPO ColorOS v3.1 or above.



## Directions
### Applying for permission
Use an OPPO enterprise developer account to log in to the [OPPO Developer Platform](https://open.oppomobile.com/) and select **Management Center** > **Application Service Platform** > **Mobile Application List** > **Select Application** > **Development Service** > **Push Service** to apply for the OPPO PUSH permission.



### Getting key
>?You can only view the key under a developer account (root account).

1. After your application for activating OPPO PUSH is approved, you can select **[OPPO PUSH Platform](https://push.oppo.com/)** > **Configuration Management** > **Application Configuration** to view the `AppKey`, `AppSecret`, and `MasterSecret`.
![](https://main.qcloudimg.com/raw/7753e738a004854d63cf4c8e4c07d51c.png)
2. Copy and paster the `AppId`, `AppKey`, and `AppSecret` parameters of the application into **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **OPPO Official Push Channel**.

### Configuring push channel
To be compatible with channel configurations for Android 8.0 or above on OPPO phones, you need to create the default TPNS channel in the OPPO Console. For more information, please see [OPPO's official documentation](https://open.oppomobile.com/wiki/doc/#id=10198).
The configuration items are as described below:
- "Channel ID": "default_message"
- "Channel Name": "default notification"



### Configuration
#### Integrating through Android Studio

Import the dependencies related to OPPO PUSH. The sample code is as follows:
```js
implementation 'com.tencent.tpns:oppo:[VERSION]-release'// OPPO PUSH [VERSION] is the version number of the current SDK, which can be viewed in SDK for Android Updates
```
>? OPPO PUSH [VERSION] is the version number of the current SDK, which can be viewed in [SDK for Android Updates](https://console.cloud.tencent.com/tpns/sdkdownload).



#### Integrating through Eclipse
After getting the TPNS SDK package for OPPO PUSH, configure the major TPNS version and the following content in the manual integration method detailed on TPNS's official website.

1. Open the `Other-push-jar` folder and import the OPPO PUSH-related jar into the project.
2. Add a class resource file to the project with the following code:
```java
package com.heytap.mcssdk;
class R {
    public static final class string {
        public static final int system_default_channel = 
	com.tencent.android.tpns.demo.R.string.oppo_system_default_channel;// This can be changed to a custom string resource ID
    }
}
```
3. Add the following configuration to the `Androidmanifest.xml` file (two methods):
 - Use the following configuration for the TPNS SDK for Android below v1.2.0.2:
```
<!--Permissions required by OPPO PUSH-->
<uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<application>
		<!--Components required by OPPO PUSH-->
		<service
			android:name="com.heytap.mcssdk.PushService"
			android:permission="com.coloros.mcs.permission.SEND_MCS_MESSAGE">
			<intent-filter>
				<action android:name="com.coloros.mcs.action.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
		<service
			android:name="com.heytap.mcssdk.AppPushService"
			android:permission="com.heytap.mcs.permission.SEND_MCS_MESSAGE">
			<intent-filter>
				<action android:name="com.heytap.mcs.action.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
</application>
```
 - Use the following configuration for the TPNS SDK for Android v1.2.0.2 and above:
```
<!--Permissions required by OPPO PUSH-->
<uses-permission android:name="com.coloros.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<uses-permission android:name="com.heytap.mcs.permission.RECIEVE_MCS_MESSAGE"/>
<application>
		<!-- The following is the OPPO component on v1.2.0.2 -->
		<service
			android:name="com.heytap.msp.push.service.CompatibleDataMessageCallbackService"
			android:permission="com.coloros.mcs.permission.SEND_MCS_MESSAGE">
			<intent-filter>
				<action android:name="com.coloros.mcs.action.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
		<service
			android:name="com.heytap.msp.push.service.DataMessageCallbackService"
			android:permission="com.heytap.mcs.permission.SEND_PUSH_MESSAGE">
			<intent-filter>
				<action android:name="com.heytap.mcs.action.RECEIVE_MCS_MESSAGE"/>
				<action android:name="com.heytap.msp.push.RECEIVE_MCS_MESSAGE"/>
			</intent-filter>
		</service>
</application>
```

### Enabling OPPO Push
Call the following code before calling TPNS' `XGPushManager.registerPush`:
```java
// Note that OPPO's `AppKey` is entered here rather than the `AppId`
XGPushConfig.setOppoPushAppId(getApplicationContext(), "OPPO AppKey");
// Note that OPPO's `AppSecret` is entered here rather than the `AppKey`
XGPushConfig.setOppoPushAppKey(getApplicationContext(), "OPPO AppSecret");
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);

// The log of successful registration is as follows:
I/TPush: [RegisterReservedInfo] Reservert info: other push token is : CN_fc0f0b38220cba7a1bcbda20857e021b  other push type: oppo
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 007a4105425********52ac1e1360c6780f3 otherPushType = oppo otherPushToken = CN_fc0f0b3822****7a1bcbda20857e021b

```


### Code obfuscation
```xml
-keep public class * extends android.app.Service
-keep class com.heytap.mcssdk.** {*;}
-keep class com.heytap.msp.push.** { *;}
```

>?Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
