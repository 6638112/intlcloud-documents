## Feature Description
When a message is inserted, the message will only be inserted into the local database but not be sent to the server.
> ! Inserted messages will be lost if the account is logged in on another mobile device or the application is uninstalled and reinstalled.

This API is used to insert tips into a conversation, such as "You have left the group" and "Keep your information secure. Do not send private information such as account, password, and verification code to the group chat". Such messages need to be displayed in the chat area, but do not need to be sent to others.

### Inserting a local message between one-to-one messages

Call `insertC2CMessageToLocalStorage` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/insertC2CMessageToLocalStorage.html)) to insert a local message between one-to-one messages. Currently, the SDK for Flutter only supports inserting custom messages.

Sample code:


```dart
TencentImSDKPlugin.v2TIMManager.getMessageManager().insertC2CMessageToLocalStorage(data: "", userID: "", sender: "");
```



### Inserting a local message between group messages

Call `insertGroupMessageToLocalStorage` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/insertGroupMessageToLocalStorage.html)) to insert a local message between group messages.

Sample code:

```dart
TencentImSDKPlugin.v2TIMManager.getMessageManager().insertGroupMessageToLocalStorage(data: "", groupID: "", sender: "");
```

