### How do I use the `AccessID`, `AccessKey`, and `SecretKey` of a TPNS application?
- AccessID: unique identifier of the TPNS application. Use cases: 1. SDK integration; 2. Authentication signature generation during RESTful API call.
- AccessKey: client authentication key of the TPNS application. Use cases: SDK integration.
- SecretKey: server authentication key of the TPNS application. Use cases: authentication signature generation during RESTful API call.




### Why is my application rejected after the review when I publish it on Huawei AppGallery?
Please download the official Huawei HMS SDK and copy all files and subdirectories in the `assets` directory to that in your application project. If the `assets` directory does not exist in the application project, create one.


### Why can't pushes be received on a Nubia phone?
TPNS does not support Nubia phones released after 2015, as the new version of Nubia operating system has a super power-saving feature, which will kill background processes very quickly and prevent TPNS Service from being started, resulting in failures of registration with Nubia phones.


### Why can't pushes be received in an iOS build production environment?
1. Check whether the production environment meets the following testing conditions: the application is the ad-hoc/App Store build (with the release certificate "Production"), and the release certificate is uploaded and successfully verified.
2. Check whether the `bundle id` configured in the Xcode project matches the configured `Provision Profile` file and whether the `Provision Profile` file corresponding to the application has been configured with the message push capability.
3. Check whether the environment specified by the `aps-environment` field in the `embedded.mobileprovision` file is correct.



### Why can't pushes be received in the production environment?
Check whether the production environment meets the following testing conditions: the application is a build packaged with the ad-hoc certificate or the release certificate ("Production") and uploaded to App Store.

### Why is the iOS token invalid?
- The system was logged out or the application was uninstalled.
- The user installed the application on a new device.
- The user restored the device from a backup.
- The user reinstalled the operating system.
- Other system-defined events. (After calling the `unregisterNotification` API, register the notification again and clear device data and settings.)

### Why can only one push message be displayed on a device that has integrated the Mi channel?
According to the documentation at Xiaomi official website, the notification bar only displays one push message by default. If you want multiple messages to be displayed in the notification bar, you need to set a unique `notify_id` for different messages (a new notification bar message with the same `notify_id` will override the previous one). The parameter at TPNS official website is `n_id`.


### Is there a limit on the number of messages displayed in the notification bar?
There is no limit on the number of notification bar messages that a phone can receive and display. The reasons for not displaying may include:
- The notification bar on a Mi phone displays the latest message by default. If you want multiple messages to be displayed, you need to set a unique `n_id` for different messages.
- The message broadcast is blocked by a phone manager application.
- A Meizu phone has a message box, and uncommon messages will go directly to it. Please view the messages there.


### How do I set a custom ringtone?

1. In the console: select **Push Notification** > **Advanced Settings** > **Reminder Mode** > **Sound** > **Customize** (for Android, select the ringtone file in the `raw` directory, which does not need the extension, such as `xg_ring`. For iOS, select the ringtone file in the `bundle` directory, which requires the extension, such as `xg_ring.wav`).
2. In RESTful API v3: for Android, set `ring=1` in the push message body, and set `ring_raw` to the name of the specified ringtone file without the extension in the `raw` directory of the Android project. For iOS, set the sound in the push message body to the name of the specified ringtone file with the extension in the `bundle` directory of the project.

>!If the client has integrated with a vendor channel, due to the limitations of Huawei and Meizu, a custom ringtone file is not allowed on their phones, and the system sound will be used by default. Currently, a custom ringtone can be used on Mi phones.


### How do I adapt to small icons?

- ROMs running native Android 5.0 or above will process the small icon of an application and add a layer of color if `target sdk` is greater than or equal to 21, causing the icon to be gray.
- If you want to display it as colored, you can set `target sdk` to below 21. If you don't want `target sdk` to be below 21, you can rename a small transparent background .png image to `notification_icon.png` (the filename must be unique) and place it in the `drawable` directory; in this way, the small icon will be displayed as gray (but shaped).
- Starting from TPNS SDK for Android v1.2.2.0, the `notification_icon.png` small icon resource will only take effect directly on Google Pixel phones by default. To achieve such small icon effect for custom notifications on other phones, you need to specify the resource filename (without the extension) as the `message.android.small_icon` field in the push API. In addition, the custom notification small icon supports solid colors by specifying a decimal value of an RGB color as the `message.android.icon_color` field in the push API.

Below is an example of push API fields, where `icon_color: 123456` indicates the RGB color 01e240:
```
{
    "message": {
        "android": {
            "small_icon": "notification_icon",
            "icon_color": 123456
        }
    }
}
```



>?
>- The small icon must be a PNG image with an alpha channel.
>- The background must be transparent.
>- Do not leave too much padding around the icon.
>- We recommend you use an image with dimensions of 46x46, as smaller images will be blurry, while larger images will be automatically scaled down.




### Can an application still receive push messages after it is closed or its process is ended?
- The TPNS channel mainly uses TPNS Service to push and receive messages. When the process is ended, TPNS Service will also be ended. Messages be received and pushed only after TPNS Service is restarted. If another application connected to TPNS is opened on the phone, messages can be received and pushed by using TPNS Service of that application. However, TPNS Service channel sharing is also subject to the phone's ROM, and 100% success rate cannot be guaranteed.
- Vendor channels can receive push messages even after the application process is ended.


### What should I do if Android v4.4.4 reports a compiling error?
If the number of loaded methods in the project exceeds 65,000, please create subpackages for the project.



### Why can't callback information be received for device registration?
- A vendor channel's callbacks are returned by the vendor server.
- You can check whether broadcast is blocked by any security application.

### Why can't I find the records of pushes created through API?
Log in to the [TPNS console](https://console.cloud.tencent.com/tpns) and select **Created via API** on the **Push Management** > **Task List** page to view the records of pushes created through API.
![](https://main.qcloudimg.com/raw/0319075f0a90f18592e33b0da9698e9c.png)


### If an account changes its bound device, what will happen when a message is sent to this account?
The currently bound device (B) can receive the push, but the original bound device (A) cannot, as only the last device bound to the account can receive pushes.


### What should I do if I specified to open an `Activity` page but it often cannot be redirected to normally?
On some phones, redirection upon click on the notification bar may experience permission issues.
Solution: in `androidManifest.xml`, add `android:exported="true"` to the `Activity` to be opened.


### What is the order in which multiple push messages are received after a user goes back online?
The messages are in ascending order by message ID. The client will also receive messages in this rule; therefore, the order in which the messages are received is the same as that in which they are sent.

### If a past time is selected for a scheduled push, will the push be sent?
Yes. If a past time is selected, the system will send the push immediately.


### Can the registration method be created in a thread?
The registration method can be called anywhere, but `ApplicationContext` needs to be passed.


