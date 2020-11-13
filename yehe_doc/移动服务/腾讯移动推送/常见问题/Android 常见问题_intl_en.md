### How do I disable the keep-alive feature of TPNS?

TPNS enables the keep-alive feature by default. Please call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in a `false` value:
```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```
If you use the automatic gradle integration method, please configure the following node under the <application> tag of the `AndroidManifest.xml` file of your application, where ```xxx``` is a custom name. If you use manual integration, please modify the node attributes as follows:

```xml
<!-- Add the following node to the AndroidManifest.xml file of your application, where xxx is a custom name: -->     
<!-- To disable the feature of keep-alive with TPNS application, please configure -->
<provider
	 android:name="com.tencent.android.tpush.XGPushProvider"
	 tools:replace="android:authorities"
	 android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
	 android:exported="false" />    
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPush: [ServiceUtil] disable pull up other app`.

### Why can't push messages be received?
Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and use the obtained token for message push. If pushes cannot be received, please troubleshoot as follows:
- Please make sure that the SDK is on the latest version. Problems in legacy versions may have already been fixed in the latest version.
- If an error occurs during message push through web, please refresh the page and try again.


### Why can't pushes be received after registration succeeded?
- Please check whether the current application package name is the same as that entered when TPNS is registered, and if not, you are recommended to enable multi-package name push.
- Check whether the network is exceptional on the phone and switch to 4G network for testing.
- TPNS push includes **notification bar message** and **in-app message** (passthrough message). A notification bar message can be displayed on the notification bar, while an in-app message cannot.
- Confirm that the phone is in normal mode. Some phones may have restrictions on network and activity of the backend TPNS process when in Low Power or Do Not Disturb mode.
- Check whether the notification bar permission is granted on the phone. On some OPPO and Vivo phones, the notification bar permission has to be granted manually.


### Why does device registration fail?
- Data sync for newly created applications will take about one minute. During this period, the registration may return the error code 20. You can try again later.
- **Incorrect parameter:** check whether the `Access ID` and `Access Key` are correctly configured. Common errors are that the `Secret key` is misused or the `Access Key` contains spaces.
- **Registration error:** if the console returns an error code such as 10004, 10002, or 20, please see [SDK for Android Error Codes](https://intl.cloud.tencent.com/document/product/1024/30722).
- **No callback after registration:** check the current network condition. You are recommended to use 4G network for testing. Wi-Fi used by many users may have insufficient network bandwidth.
- **Nubia phones:** models released in the second half of 2015 and 2016 cannot be registered, including Nubia Z11 series, Nubia Z11S series, and Nubia Z9S series.

### Why pushes can't be received after the application is closed?
- At present, third-party push services cannot guarantee that the pushes can be received after the application is closed. This problem is due to the limitation of the mobile phone's custom ROM on the TPNS service. All activities of TPNS are on the basis that the TPNS service can connect to the internet and run properly. After the service is terminated, whether it can be restarted depends on the system settings, security programs, and user operations.
- QQ and WeChat are in the system-level application allowlist, and the relevant service will not be terminated after the application is closed, so the user can still receive messages after closing the application, and in fact, the relevant service survives on the backend.
- After the Android application exits from TPNS Service and the TPNS server is disconnected, messages delivered to the device will become offline messages. Each device only retains the latest three offline messages for up to 72 hours. If messages pushed during the application shutdown is not received after you start the application again, please check whether the `XGPushManager.unregisterPush\(this\)` API has been called.

### After I install the Huawei push service on a non-Huawei mobile phone, and integrate the application with TPNS SDK, the Huawei push and other features will be deactivated. How do I fix this?

Starting from TPNS SDK 1.1.6.3, only the push service of the same brand is supported, **so the push service cannot be started in the backend or transfer user data in the mobile phone of other brands**.
Different Huawei features including the account, game and push share components, therefore, the push deactivation may lead to the unavailability of other features on a non-Huawei mobile phone. To disable this deactivation feature, please configure as follows:
Add the node configuration to the `application` tag in the `AndroidManifest.xml `. Uninstall and reinstall the application.
```xml
<meta-data
		android:name="tpns-disable-component-huawei-v2"
		android:value="false" />
<meta-data
		android:name="tpns-disable-component-huawei-v4"
		android:value="false" />
```

### How do I set the message click event?
TPNS recommends using Intent for redirection (note: the SDK supports click events by default upon message click, and the corresponding homepage will be opened. If the redirection operation is set in `onNotifactionClickedResult`, it will conflict with the custom redirection specified in the console/API, resulting in failure of the custom redirection).
**Guide for redirection through Intent:**
You need to configure the page to redirect to in the client app's manifest:
 - For example, if you want to redirect to the page specified by `AboutActivity`, use the following sample code:
```
<activity
            android:name="com.qq.xg.AboutActivity"
            android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
            <intent-filter >
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT"/>
                <!-- The custom data block specifies your complete scheme, which will generate a URL in the format of "scheme name://hostname/pathname" based on your configuration-->
                <!-- You may use app name, app package name, or another field that uniquely identifies the application to avoid conflicting redirection with other applications.-->
                <data
                    android:scheme="Scheme name"
                    android:host="Hostname"
                    android:path="/Pathname" />
            </intent-filter>
</activity>
```
 - If you use the TPNS Console to set the intent for redirect, enter in the following way:
![](https://main.qcloudimg.com/raw/5c7339b703864377ed2bc6463faddce1.png)
 - If you use a server SDK, you can set the intent for redirect as follows (with the SDK for Java as an example):
```
action.setIntent("xgscheme://com.tpns.push/notify_detail");
```
 - If you want to bring parameters such as `param1` and `param2`, you can set as follows:
```
action.setIntent("xgscheme://com.tpns.push/notify_detail?param1=aa&param2=bb");
```

**Get the parameters on the device**:
1. In the `onCreate` method of the page you specify for redirect to, add the following code:
```
Uri uri = getIntent().getData();
    if (uri != null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
 }
```
2. If the parameters passed in contain special characters such as # and &, they can be parsed by using the following method:
```
Uri uri = getIntent().getData();
    if (uri != null) {                
 String url = uri.toString();
 UrlQuerySanitizer sanitizer = new UrlQuerySanitizer();
 sanitizer.setUnregisteredParameterValueSanitizer(UrlQuerySanitizer.getAllButNulLegal());
   sanitizer.parseUrl(url);
   String value1 = sanitizer.getValue("key1");
   String value2 = sanitizer.getValue("key2");
      Log.i("TPNS" , "value1 = " + value1 + " value2 = " + value2);
}
```


### What callbacks are supported by vendor channels?
- The Mi channel supports arrival callback and passthrough but not click callback.
- The Huawei channel supports click callback (custom parameters required) and passthrough (custom parameters ignored) but not arrival callback.
- The Meizu channel supports arrival callback and click callback but not passthrough.
- The Vivo channel supports click callback but not arrival callback or passthrough.
- The OPPO channel does not support click callback, arrival callback, or passthrough.

>?Note: if you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so.



### How do I fix the problem of `otherpushToken = null` that may be encountered during debugging?
#### Troubleshooting for Mi channel
- Check whether the application package name is the same as that registered on Mi Open Push Platform.
- Check whether message push has been enabled on Mi Open Push Platform.
- For manual connection, check the manifest file configuration against the development documentation, especially the places where the package name needs to be modified:
```
<permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" android:protectionLevel="signature" />
<!-- Here, change `com.example.mipushtest` to the application package name -->
<uses-permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" />
<!-- Here, change `com.example.mipushtest` to the application package name -->
```
- Check whether you have set the `APPID` and `APPKEY` of Mi before the TPNS registration and whether third-party push has been enabled:
```
// Enable the third-party push
XGPushConfig.enableOtherPush(this,true);
// Set the `APPID` and `APPKEY` of Mi
XGPushConfig.setMiPushAppId(this,MIPUSH_APPID);
XGPushConfig.setMiPushAppKey(this,MIPUSH_APPKEY);
```
- Listen on the registration result of Mi by implementing the custom broadcast that inherits `PushMessageReceiver` and check the registration return code.
- Start Logcat and check the log with the tag of `PushService` to see what error message exists.

#### Troubleshooting for Huawei channel
- Check whether the version in **Settings** > **App Management** > **Huawei Mobile Service** on the Huawei phone is above 2.5.3.
- Check whether the application package has been signed.
- Check whether an SHA256 certificate fingerprint has been configured at Huawei's official website.
- Check the manifest file configuration against the Huawei channel connection guide in the development documentation.
- Check whether the third-party push has been enabled before the TPNS registration and whether the Huawei `AppID` is configured correctly.
- Check whether the application package name is the same as that registered at Huawei Push's official website and in the TPNS Console.
- Call `XGPushConfig.setHuaweiDebug\(true\)` before registering the code, manually confirm that the storage permission is granted to the application, check the cause of Huawei registration failure output in the `huawei.txt` file in the SD card directory, and then find the cause corresponding to the [error code](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_errorcode) in Huawei development documentation.
- In CMD, run ```adb shell setprop log.tag.hwpush VERBOSE``` and
  ```adb shell logcat -v time &gt; D:/log.txt``` to start capturing logs, conduct the test, and close the CMD window. Then, send the log to technical support.


#### Troubleshooting for Meizu channel
- It is similar to the troubleshooting method for the Mi channel. For more information, please see troubleshooting for the Mi channel.

### Why can't messages be displayed on the notification bar after arriving at phones on Meizu Flyme 6.0 or below?
1. Manual integration is used on Meizu phones on Flyme 6.0 and below.
2. Automatic integration is used on Meizu phones on Flyme 6.0 and below, and the version of the used TPNS SDK for Android is below 1.1.4.0.

In the above two cases, you need to place an image exactly named `stat_sys_third_app_notify` in the drawable folders with different resolutions. For more information, please see the `flyme-notification-res` folder in the [TPNS SDK for Android](https://console.cloud.tencent.com/tpns/sdkdownload).




### How do I fix the exception that occurs when I use quick integration in the console?
1. If an exception occurs during integration, set the `"debug"` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `"TpnsPlugin"` keyword for analysis.
2. Click "sync projects".
![](https://main.qcloudimg.com/raw/5fecbe6b63374e7e0e58c4b2cd215acb.png)

3. Check whether there are relevant dependencies in the external libraries of the project.
![](https://main.qcloudimg.com/raw/485c7595f1b478a6fad725d38deb87b4.png)


### How do I convert Android extension library v4 to AndroidX?

Add the following property to the `gradle.properties` file of the AndroidX project:
```
android.useAndroidX=trueandroid.enableJetifier=true
```
>? 
>- `android.useAndroidX=true` indicates to enable `AndroidX` for the current project.
>- `android.enableJetifier=true` indicates to migrate the dependency package to `AndroidX`. 

