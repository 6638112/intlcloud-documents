## Feature Description
After initializing the IM SDK, you need to call the SDK login API to authenticate your account to get the permissions to use message, conversation, and other features.

<dx-alert infotype="notice" title="">
Only the conversation acquisition API can be called immediately after you call the login API, and other APIs can be called only after you have successfully logged in to the SDK. Therefore, **make sure that you have logged in successfully** before using other features; otherwise, such features may become abnormal or unavailable.
</dx-alert>


## Login
You don't need to sign up on your first login, as you will automatically sign up if the login is successful.
Call the `login` API ([Dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/method_channel_im_flutter/MethodChannelIm/login.html)) to log in.

Key parameters of the `login` API are as follows:

| Parameter | Definition | Description |
| --- | --- | --- |
| UserID | Unique user ID | It can contain up to 32 bytes of letters (a-z and A-Z), digits (0-9), underscores (_), and hyphens (-). |
| UserSig | Login ticket | It is calculated by your business server to ensure security. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |

You can call the `login` API in the following scenarios:
* You use the features of the IM SDK for the first time after your application is started.
* Your ticket expires on login: The callback of the `login` API returns the `ERR_USER_SIG_EXPIRED (6206)` or `ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)` error code. In this case, you need to generate a new `userSig` to log in again.
* Your ticket expires when the user is online: You may receive the `onUserSigExpired` callback ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener/onUserSigExpired.html)) when users are online. In this case, you need to generate a new `userSig` to log in again.
* A user is kicked offline: When a user is kicked offline, the IM SDK will notify you through the `onKickedOffline` callback ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener/onKickedOffline.html)). In this case, you can prompt the user and call `login` to log in again.

You don't need to call the `login` API in the following scenarios:
* After the user's network is disconnected and then reconnected, you don't need to call the `login` function, as the IM SDK will automatically go online.
* The login process is running.

>?1. After you call the IM SDK API and log in successfully, DAU calculation will start; therefore, call the login API as needed to avoid a high DAU.
>
>2. You cannot log in to multiple IM SDK accounts of the same application at the same time; otherwise, only the last logged in account will be online. 

Sample code:


```dart
String userID = "your user id";
String userSig = "userSig from your server";
V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login(userID: userID, userSig: userSig);
if(res.code == 0){
	// Logic for successful login    
}else{
 	// Logic for failed login
}
```


### Getting the UserID

After logging in successfully, call `getLoginUser` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getLoginUser.html)) to get the `UserID`.
If the login fails, the `UserID` will be empty.

Sample code:


```dart
// Get the `UserID` of the logged-in user
V2TimValueCallback<String> getLoginUserRes = await TencentImSDKPlugin.v2TIMManager.getLoginUser();
if(getLoginUserRes.code == 0){
  userID = getLoginUserRes.data;
}
```



### Getting the login status

Call `getLoginStatus` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getLoginStatus.html)) to get the login status. If a user is logged in or logging in, don't call the login API frequently. The IM SDK supports the following login statuses:

| Login Status | Description |
|---------|---------|
| V2TIM_STATUS_LOGINED (0)  | Logged in |
| V2TIM_STATUS_LOGINING (1) | Logging in |
| V2TIM_STATUS_LOGOUT (2) | Not logged in |

Sample code:


```dart
 V2TimValueCallback<int> getLoginStatusRes = await TencentImSDKPlugin.v2TIMManager.getLoginStatus();
if(getLoginStatusRes.code == 0){
  int status = getLoginStatusRes.data;
  if(status == 0){
		// Logged in
  } else if(status == 1){
		// Logging in
  } else if(status == 2){
		// Not logged in
  }
}
```



## Multi-Client Login and Kickout
You can configure multi-client login policies for the IM SDK in the Tencent Cloud console.
There are multiple multi-client login policies, such as **A user can be concurrently online on a mobile or desktop platform and the web platform** or **A user can be concurrently online on all platforms**.
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

You can configure the **Max Login Instances per User per Platform** for the IM SDK in the Tencent Cloud console, that is, the maximum number of instances on the same platform that can be concurrently online.
This feature is available only for the Ultimate edition. A user can be concurrently online on up to ten clients on the web platform or on up to three clients on the Android, iPhone, iPad, Windows, or macOS platform (the maximum number of clients that can be concurrently online on Flutter is subject to the actual compilation result).
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

When you call the `login` API ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/login.html)) to log in, if the limit specified by the multi-client login policy for your account is exceeded, a newly logged in instance will kick out an earlier one.
The one kicked out will receive `onKickedOffline`([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener/onKickedOffline.html)).


## Logout
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, there is no need to log out before exiting the application.
In special cases, for example, if you use the IM SDK only after entering a specific UI and no longer use it after exiting the UI, you can call the `logout` API ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/logout.html)) to log out of the SDK, after which you will no longer receive new messages. Note that in this case, you also need to call `unInitSDK` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/unInitSDK.html)) after the logout to uninitialize the SDK.

Sample code:


```dart
V2TimCallback logoutRes = await TencentImSDKPlugin.v2TIMManager.logout();
if(logoutRes.code == 0){

}
```


## Account Switch
Call `login` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/login.html)) to switch between accounts in the application.

For example, to switch the logged-in user from `alice` to `bob`, just log bob in. You don't need to explicitly call `logout alice`, as this operation will be handled automatically inside the IM SDK.


