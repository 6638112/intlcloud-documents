### Why is a development environment token considered as a production environment token in iOS? How do I deal with the issue?

If an application is installed in the Xcode development environment, and development environment messages are pushed through TPNS, the following error messages are reported:
- Error message reported when you query the token using the push troubleshooting tool in the TPNS console

- Error log recorded when you debug the TPNS SDK in Xcode
```xml
Missing Provisioning Profile - iOS Apps must contain a provisioning profile  named embedded.mobileprovision.
 
```

Error cause: the application package does not contain the `embedded.mobileprovision` configuration file, making the token environment unknown.
Solution:
1. In the Xcode menu bar, choose **File** > **Project Settings**.
![](https://main.qcloudimg.com/raw/c470889681e34e87cc7f661ffb677e7d.png)
2. Set **Build System** to **Legacy Build System** and click **Done**.
![](https://main.qcloudimg.com/raw/812b625ddfe5c2e7c40c0ad52cae9aec.png)
3. Build the application again, and uninstall and reinstall it.
4. After successful registration, push messages to test the token.

### Why can't pushes be received in an iOS build production environment?
1. Check whether the production environment meets the following testing conditions: the application is the ad-hoc/App Store build (with the release certificate "Production"), and the release certificate is uploaded and successfully verified.
2. Check whether the `bundle id` configured in the Xcode project matches the configured `Provision Profile` file and whether the `Provision Profile` file corresponding to the application has been configured with the message push capability.
3. Check whether the environment specified by the `aps-environment` field in the `embedded.mobileprovision` file is correct.

### What should I do if the error `building for iOS Simulator, but linking in object file built for iOS` is reported when the Xcode 12 simulator integrates with the notification extension plugin during the build?

You need to find the extension plugin target, click **Build Settings** > **Excluded Architectures**, and add the ARM64 instruction set, as shown in the following figure:
![](https://main.qcloudimg.com/raw/1b62d4bc884c1870c70209b99200d6a6.png)

### What should I do if push certificate upload failed in the TPNS console?

Convert the .p12 file of the push certificate into a .pem file and troubleshoot as follows:

1. Open the Terminal and go to the .p12 file directory.
2. Run the following command to generate a certificate (`apns-dev-cert` is the name of the sample push certificate, which should be replaced with the name of your certificate).
<dx-codeblock>
:::  plaintext
openssl pkcs12 -clcerts -nokeys -out apns-dev-cert.pem -in apns-dev-cert.p12
:::
</dx-codeblock>
3. Enter the password of the .p12 file.
4. Run the following command to convert the .pem certificate into text:
<dx-codeblock>
:::  plaintext
openssl x509 -in apns-dev-cert.pem -inform pem -noout -text
:::
</dx-codeblock>
5. Check whether the certificate environment and corresponding Bundle ID match the application as shown below:
![](https://main.qcloudimg.com/raw/ba0e35a8bbd0e77022f26ad1dcca83ca.png)

### Why doesn't clicking a notification trigger a callback for the notification clicking event when the application is cold started?

1. Check the version of the TPNS SDK. If it is v1.2.5.3 or earlier, you are recommended to upgrade it to v1.2.5.4 or later.
2. Check the timing for calling the TPNS SDK initialization method. Currently, the TPNS SDK initialization method needs to be called as soon as possible in the main thread of the application startup method to ensure that the TPNS SDK is set as the proxy of the notification center in the first time.

### What should I do if an empty notification cannot pop up on devices on iOS 10 or below?

The `content` field cannot be empty if the RESTful API is called for push; otherwise, the notification will not pop up on devices on **iOS 10 or below**.


### Does TPNS support .p8 certificates?

A .p8 certificate has security risks. Although it is valid longer than a .p12 certificate, it has a wider push permission and scope. If leaked, it may cause more severe consequences. TPNS recommends you use .p12 certificates to manage the push services of your applications separately.



### Why can't push messages be received?
Message push involves various associated modules, and exception in any steps can lead to message delivery failure. If message delivery failures occur, you are recommended to use the [Toolbox](https://console.cloud.tencent.com/tpns/user-tools) for troubleshooting. Below are the most common issues:

**Client troubleshooting**
- Check the notification settings of the device
Please go to **Notifications** > **App name** to check whether your app has enabled message push.
- Check the network settings of the device
If there is a network issue, the client may fail to obtain the message-receiving token when registering for APNs. As a result, TPNS cannot be used to push messages to specified devices.

If the device is not connected to the Internet, it cannot receive the message, even if the client has correctly obtained the token, registered it with the TPNS backend, and the TPNS server has successfully delivered the message. The message might be received if the device reconnects to the Internet within a short time, as APNs will retain the message for some time and deliver it again.

Check the SDK integration. After the SDK is integrated, please make sure that it can get the device token used to receive messages. For more information, please see [iOS SDK Integration Guide](https://intl.cloud.tencent.com/document/product/1024/30726).


**Server troubleshooting**
- APNs server problem
The TPNS server sends a message to an iOS device via APNs. If APNs fails, the TPNS server will fail to request APNs to deliver the message to the device.
- TPNS push server problem
The TPNS server achieves message delivery through the collaboration of multiple feature modules. If an exception occurs in any of these modules, message push will fail.


**Push certificate troubleshooting**
When the TPNS server requests APNs to deliver the message, it needs to use two required parameters: the message push certificate and the device token. When pushing the message, please make sure that the message push certificate is valid. For more information on how to configure the message push certificate, please see [Acquisition of Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).




### What do I do if the error `no valid 'aps-environment' entitlement string found for application` is reported in terminal?
Check whether the bundle ID configured in the Xcode project matches the configured provisioning profile, and whether the provisioning profile corresponding to the app has been configured with the message push capability.



### How does the client play the custom push message audio?

First, on the device development side, put the audio file in the `bundle` directory.
- If you use the TPNS console to create a push, enter the audio file name in **Advanced Settings** (the full path of the audio file is not required).
- If you use RESTful APIs, set the `sound` parameter to the name of the audio file (the full path of the audio file is not required).


### Does iOS support offline retention of push messages? 
No. When the TPNS server sends a message to APNs, if APNs finds that the device is not online, it will retain the message for a while. However, the duration of the retention is not clear.



### Why is arrival data unavailable for iOS?
- iOS 9.x and earlier versions do not provide an API to listen to the arrival of messages at the device. Therefore, arrival data can be collected.  
- iOS 10.0 and later versions provide the Service Extension API, which can be called by the client to listen to the arrival of messages. For more information, please see [Notification Service Extension](https://intl.cloud.tencent.com/document/product/1024/30730).


### How do I create silent push with the TPNS server SDK?
Set `content-available` to `1` and do not use `alert`, `badge`, or `sound`.



### What should I do if `DeviceToken` is not returned occasionally for registration or APNs' request for token fails in the development environment of iOS?
This problem is caused by instability of APNs. You can fix it in the following ways:
1. Insert a SIM card into the phone and use the 4G network.
2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.
3. Use a package for the production environment.
4. Use another iPhone.


### How do I expand the testing scope on iOS if the number of testing devices is limited?
1. Enterprise signature certificate
Apply for enterprise signature and push certificates and release your application as follows:
Use the enterprise signature certificate to build and release your application. Testers can download and install the application through the dedicated enterprise channel.
2. App Store signature certificate
Use the current push certificate released on App Store as follows:
Release the preview version in TestFlight: upload the IPA package to [App Store Connect](https://appstoreconnect.apple.com), use TestFlight to create a beta version, and set the list of testers (Apple IDs) for the specified version in TestFlight. Testers can download and install your application through the official TestFlight application on App Store.


### For iOS, how do I configure to change the badge number only without displaying the message?
When creating a push, you can use the API to specify the notification bar message type, leave the title empty, and only set `badge_type`. For more information, please see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
Example:
<dx-codeblock>
:::  json
{
    "platform": "ios",
    "audience_type": "token",
    "environment":"dev",
    "token_list": [
    "05a8ea6924590dd3a94480fa1c9fc8448b4e"],
    "message_type":"notify",
    "message":{
    "ios":{
        "aps": {
            "badge_type":-2
        }
    }
 }
}
:::
</dx-codeblock>



### What should I do if my application reports the error `Crash: you can't call -sendResponse: twice nor after encoding it`?
If your application integrates TPNS SDK for iOS (1.2.7.2–1.2.5.4), uses the **Recall** feature of TPNS, and implements the following system callback:
```
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo  fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
```
Then you may encounter this error. You can use the **override** feature to process sent messages.


### What should I do if `Error Domain=NSCocoaErrorDomain Code=1001. APNs' request for a token failed` is reported during Xcode debugging?
**Problem description:**
The following error is reported during Xcode debugging: "Error Domain=NSCocoaErrorDomain Code=1001. APNs' request for a token failed during Xcode debugging. -> Please resolve the problem as follows: use 4G network and restart the phone. If the problem persists after the phone is restarted for multiple times, you are recommended to use another phone for testing." However, the problem persists after I fixed the problem as instructed.

**Troubleshooting process:**
1. Use a relevant method in the TPNS SDK to avoid running at the same time as other methods for registering remote notifications.
2. Change Xcode's build system to the legacy build system to see if there is any repeated class definition caused by repeated import of the static library. The procedure is as follows:
	1. In the Xcode menu bar, choose **File** > **Project Settings**.
	![](https://main.qcloudimg.com/raw/bec61fe573cfe656b426f2e76a6e7310.png)
	2. Set **Build System** to **Legacy Build System** and click **Done**.
	![](https://main.qcloudimg.com/raw/e3ac972a5e6c6c7f8ebdab886c7f2342.png)
	3. Compile again. If a compilation error occurs, make modifications accordingly.







