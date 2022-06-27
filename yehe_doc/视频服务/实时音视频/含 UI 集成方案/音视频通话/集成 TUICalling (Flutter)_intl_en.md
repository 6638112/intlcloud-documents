You can use the demo we provide to quickly implement the video call feature. You can also use the `TUICalling` component to customize your own UI.

>? The `TUICalling` component uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports only 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

## Using the Demo UI

### Step 1. Create an application

1. In the TRTC console, click **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVideoCall` and click **Create**.

>! The component uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

[](id:ui.step2)

### Step 2. Download the SDK and demo source code
1. Download the SDK and [demo source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, select your platform.
2. Find and open `/example/lib/debug/GenerateTestUserSig.dart`.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul><li/>SDKAPPID: A placeholder by default. Set it to the actual `SDKAppID`.
	<li>`SECRETKEY`: A placeholder by default. Set it to the actual secret key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.
>!
>- In this document, the method to obtain `UserSig` is to configure the secret key in the client code. In this method, the secret key is vulnerable to decompilation and reverse engineering. Once your secret key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and debugging**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)

### Step 4. Run the demo

>! An Android project must be run on a real device rather than a simulator.

1. Run `flutter pub get`.
2. Compile, run, and test the project.
<dx-tabs>
:::  Android\s
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or later), and click **Run**.
:::
::: iOS\s
1. Open `\ios project` in the source code directory with Xcode (11.0 or later).
2. Compile and run the demo project.
:::
</dx-tabs>

[](id:ui.step5)
### Step 5. Modify the demo source code
The `TRTCCallingDemo` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code.

| File or Folder | Description |
| ----------------------- | ------------------------------------------------------------ |
| TRTCCallingVideo.dart   | The main view for audio/video calls, where calls are answered/declined |
| TRTCCallingContact.dart | The view for contacts, where one can search for registered users to call |

[](id:model)
## Customizing UI
The `TRTCCallingDemo` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TUICalling`. You can find the component's APIs in `TRTCCalling.dart`.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

You can use the open-source component `TUICalling` to customize your own UI. This means you will use the model of the demo but design the UI by yourself.

[](id:model.step1)
### Step 1. Integrate the SDK
The audio/video call component `TUICalling` depends on the [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud) and [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin). You can configure `pubspec.yaml` to download their updates automatically.

Add the following dependencies to `pubspec.yaml` of your project.
```
dependencies:
  tencent_trtc_cloud: Latest version number
  tencent_im_sdk_plugin: Latest version number
```

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules

<dx-tabs>
::: iOS\s
Add request for mic permission in `Info.plist`:
```
<key>NSMicrophoneUsageDescription</key>
<string>You can make audio calls only if you grant the app mic permission.</string>
```
:::
::: Android\s
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.
>? Without the above steps, the [Android Manifest merge failed](https://intl.cloud.tencent.com/document/product/647/39242) error will occur and the compilation will fail.

![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>

[](id:model.step3)
### Step 3. Import the `TUICalling` component
Copy all the files in the directory below to your project:
```
/lib/TRTCCallingDemo/model
```

[](id:model.step4)
### Step 4. Initialize the component and log in
1. Call `TRTCCalling.sharedInstance()` to get an instance of the component.
2. Call `login(SDKAppID, userId, userSig)` to log in to the component. For the parameters passed in, see the table below.
 <table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
<tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it in line with your user account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. For how to calculate and use a signature, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>
<dx-codeblock>
::: java 
// Initialize the component
sCall = await TRTCCalling.sharedInstance();
sCall.login(1400000123, "userA", "xxxx");
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Make a one-to-one video call
1. The caller calls `call()` of `TRTCCalling`, passing in the user ID of the callee (`userid`) and call type (`type`). For a video call, the call type should be `TRTCCalling.typeVideoCall`.
2. The callee, if logged in, will receive the `onInvited()` callback. You can display the corresponding view based on the call type set by the inviter, which is represented by `callType` in the callback.
3. The callee can call `accept()` to answer the call and `openCamera()` to turn the local camera on. He or she can also call `reject()` to reject the call.
4. After audio/video communication is established between the caller and callee, they will both receive the `onUserVideoAvailable()` callback, which indicates that they have received each other's video. They can then call `startRemoteView()` to display each other’s video. Remote audio will be played back automatically by default.


[](id:api)
## Component APIs
The table below lists the APIs of the `TUICalling` component.

| API | Description |
| ------------------ | --------------------------------------------------------- |
| registerListener   | Registers a listener of the component to listen for events. |
| unRegisterListener | Unregisters a listener.                                                 |
| destroy | Terminates an instance. |
| login | Logs in to IM. All features can be used only after login. |
| logout | Logs out of IM. Calls cannot be made after logout. |
| call | Makes a C2C call. The invitee will receive the `onInvited` notification. |
| accept | Answers a call. |
| reject | Declines a call. |
| hangup | Ends a call. |
| startRemoteView | Renders the camera data of a remote user in the specified `TXCloudVideoView`. |
| stopRemoteView | Stops rendering the camera data of a remote user. |
| openCamera | Turns the camera on and renders the camera data in the specified `TXCloudVideoView`. |
| closeCamera | Turns the camera off. |
| switchCamera | Switches between the front and rear cameras. |
| setMicMute | Mutes/Unmutes the mic. |
| setHandsFree | Enables/Disables the hands-free mode. |

