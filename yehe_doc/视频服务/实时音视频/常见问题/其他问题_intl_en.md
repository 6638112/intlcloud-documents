[](id:que1)
### How do live streaming, interactive live streaming, TRTC, and relayed live streaming differ from and relate to each other?
- **Live streaming** (keywords: one-to-many, RTMP/HLS/HTTP-FLV, CDN)
 Live streaming consists of the push end, the playback end, and the cloud live streaming service. Streams are pushed over the universal protocol RTMP, distributed through CDNs, and can be watched over protocols including RTMP, HTTP-FLV, or HLS (for HTML5).
- **Interactive live streaming** (keywords: co-anchoring, cross-room communication)
 In interactive live streaming, audience can co-anchor with anchors and anchors from different rooms can compete with each other.
- **Tencent real-time communication** (keywords: multi-person interaction, UDP-based proprietary protocol, low latency)
 The main capabilities of TRTC are audio/video interaction and low-latency live streaming. It uses a UDP-based proprietary protocol and can keep the latency as low as 100 ms. Typical applications include QQ calls, VooV Meeting, and online group classes. TRTC offers solutions for mainstream platforms including iOS, Android, and Windows, allows communication with WebRTC, and supports mixing streams in the cloud and relaying them to CDNs.
- **Relayed live streaming** (keywords: on-cloud stream mixing, RTC relayed live streaming, CDN)
 The relayed live streaming technology replicates multiple streams in a low-latency co-anchoring room and mixes them into one stream in the cloud before pushing it to a live streaming CDN for distribution and playback. 

[](id:que2)

### The demo is running on two devices, but why can't they display the images of each other?
Make sure that the two devices use different `UserID`. With TRTC, unless under different applications (`SDKAppID`), you cannot use the same `UserID` on two devices simultaneously.

[](id:que3)
### When there is only one user in a room, why is CDN playback stuttering and blurry?
Please set the `TRTCAppScene` parameter in `enterRoom` to **TRTCAppSceneLIVE**.
The `VideoCall` mode is optimized for video calls, so when there is only one user in a room, TRTC tends to maintain a low bitrate and frame rate to reduce traffic usage, which makes the video choppy and blurry.

[](id:que4)
### Why can't I enter any online room?

This may be because advanced permission control is enabled. If you enable advanced permission control for an application (`SDKAppID`), users must pass `PrivateMapKey` in TRTCParams` to enter the rooms under the application. Therefore, if your business is online, and you haven’t integrated into it the `privateMapKey` logic, please do not enable the feature. For more information, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157).

[](id:que5)
### How do I view TRTC logs?
TRTC logs are compressed and encrypted by default with the XLOG extension. You can use `setLogCompressEnabled` to specify whether to encrypt logs. If a log filename contains `C` (compressed), the log is compressed and encrypted; if it contains `R` (raw), the log is in plaintext.

- iOS/macOS: `Documents/log` of the application sandbox
- Android:
	- v6.7 or earlier: `/sdcard/log/tencent/liteav`
	- v6.8-8.5: `/sdcard/Android/data/package name/files/log/tencent/liteav/`
	- Later than v8.5: `/sdcard/Android/data/package name/files/log/liteav/`
- Windows:
	- Earlier than v8.8: `%appdata%/tencent/liteav/log`
	- v8.8 and later: `%appdata%/liteav/log`
- Web: Open the browser console or use vConsole to log printed SDK information.

  

>?
>- You need to download a decryption tool to view an XLOG file. Place the tool in the same directory as the XLOG file in Python 2.7 and run `python decode_mars_log_file.py`.
>- You can download the log decryption tool at `dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`.


[](id:que6)
### What should I do if a 10006 error occurs?
If the "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether your TRTC application service is available.
Log in to the TRTC console, click **[Application Management](https://console.cloud.tencent.com/trtc/app)**, find the application you created, and click **Application Info** to view the service status.
![](https://qcloudimg.tencent-cloud.cn/raw/5004e787b0f76d62f899234cf974b645.png)

[](id:que7)
### Why is the error code “-100018” returned during room entry?
This error is a result of `UserSig` verification failure, which may be caused by the following reasons:
- The `SDKAppID` parameter passed in is incorrect. You can log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)** to view the `SDKAppID`.
- The `UserSig` passed in, which should match the `UserID`, is incorrect. To verify your `UserSig`, log in to the TRTC console and click **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.


[](id:que8)
### How do I make a cross-room call?
You can make a cross-room call by using the `connectOtherRoom` API. Anchor A calls `connectOtherRoom()` to connect to anchor B and gets the result via the `onConnectOtherRoom` callback. All users in anchor A’s room will be notified via the `onUserEnter` callback that anchor B has entered the room, and all users in anchor B’s room will be notified via the `onUserEnter` callback that anchor A has entered the room.

[](id:que10)
### Do I have to call the `exitRoom()` API?
After you call `enterRoom`, regardless of whether room entry succeeds, you must call `exitRoom` before calling `enterRoom` again; otherwise, an unexpected error will occur.


[](id:que16)
### What are the formats of the recording files generated in different relayed recording scenarios?  
Recording files are generated in the formats you specify in the [TRTC console](https://console.cloud.tencent.com/trtc).


[](id:que20)
### How do I know whether a stream is published successfully in a video call?
You know when you receive the `onSendFirstLocalVideoFrame` callback. After `enterRoom` and `startLocalPreview` are called successfully, the SDK will capture video from the camera and encode the video captured. It will return this callback after sending the first video frame to the cloud.

[](id:que21)
### How do I know whether a stream is published successfully in an audio call?
You know when you receive the `onSendFirstLocalAudioFrame` callback. After `enterRoom` and `startLocalAudio` are called successfully, the SDK will capture audio from the mic and encode the audio captured. It will return this callback after sending the first audio frame to the cloud.

[](id:que22)
### Can I query all `UserID` values?
Currently, you cannot view the statistics of all user IDs, but you can write user data into the SQL database whenever accounts are created on the client for future management and query.


[](id:que23)
### Can users with the same `UserID` be in the same room at the same time?
In TRTC, users with the same `UserID` cannot be in the same room at the same time because it will cause a conflict.

[](id:que24)
### Why doesn't the audio route (receiver/speaker) configured via the `setAudioRoute` API take effect? 
You can switch between the receiver and speaker only in the call volume mode. That is to say, the API works only if two or more users are co-anchoring.


[](id:que25)
### Can I manually enable recording for a call?
You can manually enable recording for a call in the following steps:
1. In the TRTC console, click **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Function Configuration**, enable **Relay to CDN**, and disable On-Cloud Recording**.
2. After a user (`userid`) enters the room, splice the user’s `streamid` according to the stream ID generation rule.
3. Use the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API of CSS to start a recording task for the `streamid`.
 - Set `DomainName` to `[bizid].livepush.myqcloud.com`.
 - Set `AppName` to `trtc_[sdkappid]`.
 - Set `StreamName` to `streamid`.
4. After the recording task is completed, CSS will save the file in VOD and notify you via the [recording callback](https://intl.cloud.tencent.com/document/product/267/38080).

[](id:que26)
### How does TRTC verify `UserSig`? How do I troubleshoot the “-3319” or “-3320” error during room entry? 
Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)** to verify your `UserSig`.

[](id:que27)
### How do I view my call duration and usage? 
You can find the information on the **[Usage Statistics](https://console.cloud.tencent.com/trtc/statistics)** page of the TRTC console.

[](id:que28)
### How do I maintain the user list and count the number of users in a TRTC room?  
If you have integrated [IM](https://intl.cloud.tencent.com/document/product/1047) into your project, you can use the IM group user counting API to calculate the number of users in a room. However, such calculation is not always accurate. You may use this method if you don’t have a high requirement on accuracy.
If you do have a high requirement on the accuracy of the calculation, we recommend you implement the following calculation logic:

1. Increase the user count (client -> server): Whenever a user enters the room, increase the user count by 1. To achieve this, you can make the user’s client send a count increasing request to the server upon room entry.
2. Decrease the user count (client -> server): When a user leaves a room, decrease the user count by 1. To achieve this, you can make the user’s client send a count decreasing request to the server during room exit.

[](id:que29)
### A “-100013” error is reported during room entry, with the error message “ERR_SERVER_INFO_SERVICE_SUSPENDED”. What should I do?  
This error indicates that the service is unavailable. Please check the following:
- Whether you have used up your package
- Whether your Tencent Cloud account has overdue payment

[](id:que33)
### What should I do if I have enabled on-cloud recording but no recording files are generated?
1. Make sure you have enabled **Relay to CDN** and **On-Cloud Recording** in the [TRTC console](https://console.cloud.tencent.com/trtc).
2. TRTC starts recording only if there is a user publishing audio/video data in a room.
3. A recording file will be generated only if CDN pull is successful.
4. If there is only audio in a room at first before video is published, depending on the recording template configured, the recording file generated may contain only the video segment or the audio-only segment.

[](id:que36)
### How do I give the room ID to the co-anchor I invite?
You can insert the room ID in a custom message. The invitee can get the room ID after parsing the message. For details, see [Message Sending and Receiving](https://intl.cloud.tencent.com/document/product/1047/34322) and [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391).

[](id:que37)
### Is it possible to start audio recording only when there are two or more users in a room?
Yes, it is. If you want to record mixed audio data, call On-Cloud MixTranscoding first, specifying the output stream ID, and call the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API of CSS.

 [](id:que38)
### How do I capture the audio of a shared application on Windows?
You can call [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) to enable system audio capturing.

[](id:que39)
### How to implement the feature that allows anchors to invite audience members to co-anchor in conference scenarios on Windows?
You need to use another Tencent Cloud product, [IM](https://intl.cloud.tencent.com/document/product/1047/33996), to implement the feature.

This is how it works: A sends a custom message X (you can determine how the message is displayed) to B, and the calling page is shown; B receives X and the called page is shown; B uses [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) to enter the room and sends a custom message X1 to A; A receives X1 (you can determine whether to display the message) and uses `enterRoom` to enter the room. The messages are sent via IM.

[](id:que40)
### How do audience members watch the videos of co-anchors in a room?
In live streaming scenarios, audience get the `userid` of anchors in a room via the [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) callback in `TRTCCloudDelegate` (co-anchoring users enter the room by calling [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) and are also anchors for the audience). They then call [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) to play the videos of the anchors.
For more information, see [Live Streaming Mode > Windows](https://intl.cloud.tencent.com/document/product/647/35109).

[](id:que41)
### Is there a TRTC SDK for Linux?
The TRTC Linux SDK is not commercially available yet. If you have questions about the SDK or want to use it, please contact us at colleenyu@tencent.com.

[](id:que42)
### Does TRTC support screen sharing during video calls or interactive live streaming?
Yes, it does. During video calls or interactive live streaming, the video captured by the camera is published as the primary stream. You can also publish the screen as the substream. The shared screen will contain the video call or interactive live streaming window.
