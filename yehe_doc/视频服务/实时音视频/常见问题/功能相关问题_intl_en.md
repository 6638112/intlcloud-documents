<span id="que1"></span>
### What is a `RoomID` in TRTC? What is its value range?
A `RoomID` (room ID) is used to uniquely identify a room. It can range from 1 to 4294967295 and is maintained and assigned on your own.

<span id="que2"></span>
### What is the room entry UserID in TRTC? What is its value range? 
A `UserID` (user ID) is used to uniquely identify a user in a TRTC application. Its recommended length is below 32 bytes. It can be a combination of letters, digits, and underscores. It is case insensitive.


<span id="que3"></span>
### How long is the lifecycle of a TRTC room?
- The first user who enters a room will be the room owner, but this user cannot dismiss the room actively.
- After all users actively exit the current room, it will be immediately dismissed on the backend.
- If a user in the room is disconnected exceptionally, the server will remove this user from the room after 30 seconds. If all users in the room are disconnected exceptionally, the server will automatically dismiss the room after 30 seconds.
- When a user attempts to enter a room that does not exist, the backend will create the room first.

<span id="que4"></span>
### Does TRTC support manually configuring the subscription to audio/video streams? 
To implement the "instant streaming" effect, the stream will be automatically subscribed to during room entry by default. You can call the `setDefaultStreamRecvMode` API to switch to the manual subscription mode.

<span id="que5"></span>
### Can I set a custom ID for a relayed stream in TRTC?  
Yes. You can specify the `streamId` in the `TRTCParams` parameter of `enterRoom` or call the `startPublishing` API to pass in the `streamId` parameter.

<span id="que6"></span>
### Which roles are supported by TRTC live streaming? What are the differences between them?
In live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`), two roles are supported: `TRTCRoleAnchor` (anchor) and `TRTCRoleAudience` (viewer). The difference is that an anchor can upstream and downstream audio/video data at the same time, while a viewer can only downstream and play back others' data. You can call `switchRole()` to switch between roles.

<span id="que7"></span>
### What is the "role" concept in TRTC? 
Anchors and viewers can be set only in live streaming scenarios. The anchor role `TRTCRoleAnchor` has audio/video upstreaming/downstreaming permissions, and there can be up to 30 concurrent anchors. The viewer role `TRTCRoleAudience` has only the audio/video downstreaming permissions, and there can be up to 100,000 concurrent viewers.
>? Up to 20 users can simultaneously enable the camera or mic on web.


<span id="que8"></span>
### What scenarios are supported by TRTC rooms?  
The following scenarios are supported:
- TRTCAppSceneVideoCall: video call scenarios such as one-to-one video call, video conferencing with up to 300 participants, online medical diagnosis, video chat, and video interview.
- TRTCAppSceneLIVE: interactive video live streaming scenarios such as low-latency video live streaming, interactive classroom for up to 100,000 participants, live video competition, video dating room, remote training, and mega-scale conferencing.
- TRTCAppSceneAudioCall: audio call scenarios such as one-to-one audio call, audio conferencing with up to 300 participants, voice chat, and online Werewolf.
- TRTCAppSceneVoiceChatRoom: interactive audio live streaming scenarios such as low-latency live audio streaming, live audio co-anchoring, voice chat room, karaoke room, and FM radio.


<span id="que9"></span>
### What platforms does TRTC support?
Supported platforms include iOS, Android, Windows (C++), Windows (C#), macOS, desktop browser, Electron, and Linux. For more information, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35078).

<span id="que10"></span>
### What are the differences between TRTC Lite (TRTC), Professional, and Enterprise Editions? 
For more information, please see [Differences Between Editions](https://intl.cloud.tencent.com/document/product/647/34615).


<span id="que11"></span>
### Does TRTC support live streaming co-anchoring?
Yes. For detailed directions, please see:
- [Live Streaming Mode (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35107)
- [Live Streaming Mode (Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [Live Streaming (Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [Live Streaming (Web)](https://intl.cloud.tencent.com/document/product/647/35110)


<span id="que12"></span>
### How many rooms can be created in TRTC at the same time?
There can be up to 4,294,967,294 concurrent rooms, and there is no limit on the cumulative number of rooms.

<span id="que13"></span>
### How do I create a room?
A room will be automatically created on the Tencent Cloud backend when a user enters the room on the client, so you can "enter a room" simply by calling the relevant client API, with no need to manually create a room:
- [iOS and macOS > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows (C++) > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)
- [Windows (C#) > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b)
- [Electron > enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?_ga=1.212321108.1562552652.1542703643#enterRoom)
- [Desktop Browser > join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html?_ga=1.256770123.1562552652.1542703643#join)

<span id="que14"></span>
### What is the maximum bandwidth supported by the video server of TRTC?
Unlimited.


<span id="que15"></span>
### Does TRTC support deployment in a private cloud?
No.

<span id="que16"></span>
### To enable relayed live streaming in TRTC, do I need to get an ICP filing for my domain name?
To enable relayed live streaming, according to the requirements of applicable Chinese authorities, the playback domain name in Mainland China needs an ICP filing before it can be used. For more information, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

<span id="que17"></span>
### How long is the average delay in TRTC?
The average end-to-end delay around the globe is less than 300 ms.

<span id="que18"></span>
### Does TRTC support active calls?
This feature can be implemented together with the signaling channel. For example, you can use the custom message feature of [Instant Messaging](https://intl.cloud.tencent.com/product/im) to make calls. For more information, please see the scenario-specific demos in the [SDK](https://intl.cloud.tencent.com/document/product/647/34615) source code.

<span id="que19"></span>
### Does TRTC support Bluetooth earphones during one-to-one video call?
Yes.


<span id="que20"></span>
### Can TRTC be used outside Mainland China?
Yes.

<span id="que21"></span>
### Does TRTC support screen sharing on PC?
Yes. For more information, please see the following documents:
- [Screen Sharing (Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [Screen Sharing (macOS)](https://intl.cloud.tencent.com/document/product/647/37336)
- [Screen Sharing (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/35163)

For more information on screen sharing APIs, please see [APIs for Windows (C++)](https://intl.cloud.tencent.com/document/product/647/35131) or [APIs for Windows (C#)](https://intl.cloud.tencent.com/document/product/647/35136). In addition, you can also use [APIs for Electron](https://intl.cloud.tencent.com/document/product/647/35141).

<span id="que23"></span>
### Can I share local video files in TRTC?

Yes. This can be implemented through the [custom capturing](https://intl.cloud.tencent.com/document/product/647/35158) feature.

<span id="que24"></span>
### Can TRTC record live streaming videos and store the recording files locally on the phone?
Recording files cannot be stored locally on the phone. Video recording files will be stored on the VOD platform by default. You can download and save them to the phone by yourself. For more information, please see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).


<span id="que25"></span>
### Does TRTC support pure real-time audio?
Yes.


<span id="que26"></span>
### Can there be more than one channel of screen sharing in the same room at the same time?
Currently, there can only be one substream of screen sharing in a room.

<span id="que27"></span>
### When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change as the window size changes?
By default, the SDK will automatically adjust the encoding parameters according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameter for screen sharing or specify the corresponding encoding parameter when calling the `startScreenCapture` API.


<span id="que28"></span>
### Does TRTC support 1080p?
Yes. You can set the resolution through the video encoding parameter `setVideoEncoderParam` of the SDK.

<span id="que29"></span>
### Does TRTC support custom data capturing?
This feature is supported on certain platforms. For more information, please see [Custom Capturing and Rendering](https://intl.cloud.tencent.com/document/product/647/35158).

<span id="que30"></span>
### Can TRTC communicate with the ILVB SDK?
No.

<span id="que31"></span>
### Can TRTC communicate with MLVB? 
TRTC and MLVB have different backend architectures and therefore cannot directly communicate with each other. The TRTC backend can relay pushes only to CDN.



<span id="que32"></span>
### What are the differences between the TRTC room entry modes indicated by `AppScene`?
TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as call mode, while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as live streaming mode.
- In call mode, there can be a maximum of 300 members in a single TRTC room, and up to 30 of them can speak at the same time. This service is suitable for various scenarios such as one-to-one video call, video conferencing with up to 300 participants, online medical diagnosis, video interview, video customer service, and online werewolf.
- TRTC in live streaming mode supports a maximum of 100,000 online users in one single room with a co-anchoring latency of below 300 ms and a watch latency of below 1,000 ms and enables users to mic on/off smoothly. This mode is suitable for such application scenarios as low-latency interactive live streaming, interactive classroom for up to 100,000 participants, video dating, online education, remote training, and large-scale conferencing.

>? Up to 20 users can simultaneously enable the camera or mic on web.

<span id="que33"></span>
### Does TRTC support hands-free mode during audio/video call?
Yes. You can implement the hands-free mode by setting audio routing. In the native SDK, switch the routing in the `setAudioRoute` API.

<span id="que34"></span>
###  Does TRTC support volume level reminder?
Yes. You can call the `enableAudioVolumeEvaluation` API to enable it.

<span id="que35"></span>
### Can I set image mirroring in TRTC? 
Yes. You can call the `setLocalViewMirror` API to set the mirroring mode for the preview image of the local camera or call the `setVideoEncoderMirror` API to set the mirroring mode for the output image of the encoder.

<span id="que36"></span>
### Can I record call audio in TRTC to a local file? 
Yes. You can call `startAudioRecording` API to record all audios (such as local audio, remote audio, and background music) in the current call to a file. Currently, PCM, WAV, and AAC audio formats are supported.

<span id="que37"></span>
### Can I record the video in audio/video communication in TRTC to a file?
(Audio/Video) recording on a local server is supported. To try this feature out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to get the SDKs and relevant guides.
You can also use the [on-cloud recording and playback](https://intl.cloud.tencent.com/document/product/647/35426) feature to record video.

<span id="que38"></span>
### Does TRTC support features such as floating window like that in WeChat video call and big/small image switch?
These features belong to the UI layout logic, and the SDK does not restrict the display and processing of UI. The official demo provides sample code for image cascading and 9-grid layout modes and supports floating window, big/small image switch, and image drag. For more information, please see the [official demo](https://github.com/tencentyun/TRTCSDK).

<span id="que39"></span>
### How does TRTC implement pure audio call?
TRTC does not distinguish between audio and video channels. If only `startLocalAudio` is called but `startLocalPreview` is not, the call will be in pure audio mode.

<span id="que40"></span>
### How are relayed push and recording implemented during audio call in TRTC?
- Version below TRTC SDK 6.9: construct `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}` during room entry and pass it into `TRTCParams.businessInfo`. `1` indicates relayed push, and `2` indicates relayed push and recording.
- TRTC SDK 6.9 or above: select `TRTCAppSceneAudioCall` or `TRTCAppSceneVoiceChatRoom` as the scenario parameter during room entry.

<span id="que41"></span>
### Can I kick out a user, forbid a user to speak, or mute a user in a TRTC room?  
Yes.
- To perform a simple signaling operation, you can use the custom signaling API `sendCustomCmdMsg` of TRTC to define the corresponding control signaling, and the user in the call will perform the corresponding operation after receiving the control signaling. For example, to kick out a user is to define a kick-out signaling, and the user receiving it will exit the room automatically.
- If you want to implement a more comprehensive operation logic, we recommend you use [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047) to map the TRTC room to an IM group and receive/send custom messages in the group, so as to perform the corresponding operation.

<span id="que42"></span>
### Does TRTC support playback of pulled RTMP/FLV streams?  
Yes. Currently, TXLivePlayer has been embedded in the TRTC SDK. If you need more player features, you can directly use the LiteAVSDK_Professional Edition, which provides all player features.

<span id="que43"></span>
### How many people can be in the same call in TRTC?
- In call mode, a single room can sustain up to 300 concurrent online users, and up to 30 of them can simultaneously enable the camera or mic.
- In live streaming mode, a single room can sustain up to 100,000 concurrent online viewers, and up to 30 of them can simultaneously enable the camera or mic as anchors.

>? Up to 20 users can simultaneously enable the camera or mic on web.

<span id="que44"></span>
###  How does TRTC implement live streaming applications?
Specially for live streaming scenarios, TRTC provides the low-latency interactive live streaming solution. It can sustain up to 100,000 concurrent users and ensure a latency between co-anchoring anchors of as short as 200 milliseconds and a latency between anchor and viewer of less than 1 second. In addition, it delivers a high performance even in weak network environments to adapt to the complex network environments of mobile devices.
For detailed directions, please see [Live Streaming Mode](https://intl.cloud.tencent.com/document/product/647/35107).

<span id="que45"></span>
### Can I use the custom message sending API of TRTC to implement features such as chat room and on-screen commenting?
No. Custom message sending in TRTC is only applicable to simple and low-frequency signaling transfer scenarios. For specific limits, please see [Use Limits](https://intl.cloud.tencent.com/document/product/647/35159).

<span id="que46"></span>
### Does the TRTC SDK support looped playback of the background music? Can I adjust the playback progress of the background music?  
Yes. You can call the playback API again in the completion callback to implement looped playback and call `setBGMPosition()` to set the playback progress.

<span id="que47"></span>
### Does TRTC provide listening callbacks for room entry/exit of members? Are `onUserEnter` and `onUserExit` available?
Yes. TRTC uses `onRemoteUserEnterRoom`/`onRemoteUserLeaveRoom` to listen on room entry/exit of members (they will be triggered only for users with audio/video upstreaming permissions).
>?`onUserEnter` and `onUserExit` have been disused on v6.8 and replaced with `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom`, respectively.

<span id="que48"></span>
### How does TRTC monitor network disconnection and reconnection?
It can listen on such events through the following listening callbacks:
- onConnectionLost: the connection between SDK and server is closed.
- onTryToReconnect: the SDK tries to reconnect to the server.
- onConnectionRecovery: the connection between SDK and server is restored.

<span id="que49"></span>
### Does TRTC provide a callback for first frame rendering? Can the start of image rendering and start of audio playback be listened on?
Yes. `onFirstVideoFrame` and `onFirstAudioFrame` are used for listening on such events.

<span id="que50"></span>
### Does TRTC support screencapturing of video images?
Currently, you can call `snapshotVideo()` on iOS or Android to screencapture the local and remote video images.

<span id="que51"></span>
### An exception occurred in TRTC when a peripheral device such as Bluetooth earphone was connected. What should I do?
Currently, TRTC is compatible with mainstream Bluetooth earphones and other peripheral devices; however, it is still incompatible with certain devices. We recommend you use the official demo, WeChat, and QQ audio/video call to test the compatibility.

<span id="que52"></span>
### How do I get information such as upstream/downstream bitrate, resolution, packet loss rate, and audio sample rate of a TRTC audio/video call?
You can call the `onStatistics()` API of the SDK to get these statistics.

<span id="que53"></span>
### Does the background music API `playBGM()` of TRTC support online music?
No. Currently, only local music is supported. You can download the music file and then call the `playBGM()` API for playback.

<span id="que54"></span>
### Does TRTC support setting the local capturing volume level? Can I set the playback volume level of each remote user?
Yes. You can call the `setAudioCaptureVolume()` API to set the SDK capturing volume level and the `setRemoteAudioVolume()` API to set the playback volume level of a remote user.

<span id="que55"></span>
### What are the differences between `stopLocalPreview` and `muteLocalVideo`?
- `stopLocalPreview` is used to stop local video capturing. After this API is called, both the local and remote video images will turn black.
- `muteLocalVideo` is used to set whether to send the local video image to the backend. After this API is called, the image viewed by other users will turn black, but the caller can still view the local preview image.

<span id="que56"></span>
### What are the differences between `stopLocalAudio` and `muteLocalAudio`? 
- `stopLocalAudio` is used to disable local audio capturing and upstreaming.
- `muteLocalAudio` does not stop sending audio/video data; instead, it continues to send mute packets with extremely low bitrate.

<span id="que57"></span>
### Which resolutions are supported by the TRTC SDK?
We recommend you configure the resolution as instructed in [Setting Image Quality](https://intl.cloud.tencent.com/document/product/647/35153) to achieve a more appropriate image quality.

<span id="que58"></span>
### How do I set the upstream video bitrate, resolution, and frame rate in the TRTC SDK? 
You can call the `setVideoEncoderParam()` API in `TRTCCloud` to set the `videoResolution` (resolution), `videoFps` (frame rate), and `videoBitrate` (bitrate) in the `TRTCVideoEncParam` parameter.

<span id="que59"></span>
### How do I use the SDK to control the image angle and direction?  
For more information, please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).

<span id="que60"></span>
### How do I make a video call in landscape mode? 
For more information, please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).

<span id="que61"></span>
### How do I adjust the directions of local and remote images in TRTC if they are different?  
For more information, please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).


<span id="que62"></span>
### Are there any recommended parameter settings for TRTC image quality (bitrate, resolution, and frame rate)?
For more information, please see [Recommended Configuration](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE).

<span id="que63"></span>
### Does TRTC support network speed test? How do I use this feature?  
For more information, please see [Testing Network Speed Before Chat](https://intl.cloud.tencent.com/document/product/647/35156).

<span id="que64"></span>
### Does TRTC support room entry authentication in scenarios such as allowing entry for only authorized members? 
Yes. For more information, please see [Room Entry Permission Protection](https://intl.cloud.tencent.com/document/product/647/35157).

<span id="que65"></span>
### Can TRTC audio/video streams be pulled through CDN for playback? 
Yes. For more information, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

<span id="que66"></span>
### What formats are supported by TRTC custom rendering? 
- For iOS, I420, NV12, and BGRA are supported.
- For Android, I420 and Texture2D are supported.
