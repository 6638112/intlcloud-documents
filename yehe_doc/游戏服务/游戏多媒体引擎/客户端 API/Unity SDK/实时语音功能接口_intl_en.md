This document describes how to access and debug the GME APIs for Unity Voice Chat.

<dx-alert infotype="explain" title="">
This document applies to GME SDK version 2.9.
</dx-alert>

## Considerations

GME provides two services: Voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
You **only need to call `Init` API once** no matter how many GME services you want to use.
Calling `Init` does not trigger billing. The billing starts when the <dx-tag-link link="#EnterRoom" tag="EnterRoom">EnterRoom</dx-tag-link> API is called and users enter the room successfully.
</dx-alert>

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Directions

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initialize GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Periodically trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Enter a voice chat room</dx-tag-link>
-<dx-tag-link  tag="Callback: QAVEnterRoomComplete">Callback of Room Entry</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Turn on the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Turn on the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exit a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitialize GME SDK</dx-tag-link>
</dx-steps>


### Important

- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

### C# classes

| Class | Description |
| ------------------- | :----------------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**Call the `Init` API before calling any APIs of GME.**

If you have any questions when using the service, please see [General Issues](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

<dx-alert infotype="notice" title="">
If you need to switch the account, please call `UnInit` to uninitialize the SDK. No fee is incurred for calling Init API.
</dx-alert>

### Imported header files

```
using TencentMobileGaming;
```

### Getting an instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

### [Initializing SDK](id:Init)

- This API is used to initialize the GME service. You need to call it before using GME. No fee is incurred for calling this API.
- **For more information on how to get the `sdkAppID`, see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.

<dx-alert infotype="notice" title="">
 - The SDK must be initialized before a user can enter a voice chat room.
 - The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.
</dx-alert>

#### Function prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme) |
| openId | string | The `openId` must be an Int64 string. |


#### Response

| Response | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | The SDK file is not complete. Please delete it and import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.


<dx-alert infotype="notice" title="Notes on 7015 error code">
- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
</dx-alert>

#### Sample code 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// Determine whether the initialization is successful by the returned value
if (ret != QAVError.OK)
    {
        Debug.Log("SDK initialization failed:"+ret);
        return;
    }
```

### [Event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. `Poll` is the message pump of GME, and the `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### Function prototype

```
ITMGContext public abstract int Poll();
```

#### Sample code

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext  public abstract int Resume()
```

### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### Function prototype

```
ITMGContext public abstract int Uninit()
```

## Voice Chat

Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/28a13d4beccdfecb0ad7530008ec8da0.png)

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/39524).

| API | Description |
| -------------- | :------------------: |
| GenAuthBuffer | Initializes authentication |
| EnterRoom | Enters room |
| IsRoomEntered | Indicates whether room entry is successful |
| ExitRoom | Exits room |
| ChangeRoomType | Modifies user's room audio type |
| GetRoomType | Gets user's room audio type |

### Voice chat room call flowchart

![](https://main.qcloudimg.com/raw/2b5d8f7f7f4b4b3fbce8c9ebf01f78d8.png)

<dx-alert infotype="alarm" title="Enter the room successfully">
If the room entry callback result is 0, the room entry is successful. The returned value of 0 from the `EnterRoom` API does not necessarily mean that the room entry is successful.
</dx-alert>

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppID` from the GME console.|
| roomId | string | Room ID, which can contain up to 127 characters. |
| openId | string | User ID, which is the same as `openID` during initialization. |
| key | string | Permission key from the [GME console](https://console.cloud.tencent.com/gamegme). |

#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}
```

###  [Entering a room](id:EnterRoom)

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates successful API call but not successful room entry.

#### Function prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----------: | ----------------------- |
| roomId | string | Room ID, which can contain up to 127 characters |
| roomType   | ITMGRoomType | Just enter `ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY` |
| authBuffer | Byte[] | Authentication code |

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```


<dx-alert infotype="notice" title="Please use smooth quality">
Use `ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY` as the room type parameter to enter the room. If you enter the room with non-LD sound quality, an error will be reported and you cannot enter the room.
</dx-alert>



### Callback for room entry

After the user enters the room, the room entry result will be called back, which can be listened on for processing. A successful callback means that the room entry is successful, and the billing **starts**.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/36276)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when the client goes offline?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### Function prototype

```
// Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
// Event-triggered function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

// Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("error code:" + err + " error message:" + errInfo);
            return;
	}else{
		// Entered room successfully
    }
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |


If the network is disconnected, there will be a callback message `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. Upon receiving of this message, the SDK tries to reconnect with the callback message `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.


#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | The user is already in another room. |
| 1001 | The user entering a room. It is recommended not to call `EnterRoom` repeatedly until the EnterRoom callback is returned. |
| 1003 | The user is already in the room. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### [Exiting the room](id:ExitRoom)

This API is called to exit the current room. It is an async API. The reponse `AV_OK` indicates that the task is triggered.

If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype  

```
ITMGContext ExitRoom()
```

#### Sample code  

```
ITMGContext.GetInstance().ExitRoom();
```

### Callback for room exit

A callback will be executed through a delegate function to pass a message after room exit.

#### Function prototype  

```
Delegate function:
public delegate void QAVExitRoomComplete();
Event-triggered function:
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
Process the event listened on:
void OnExitRoomComplete(){
    // Send a callback after room exit
}
```

### Determining whether the user has entered the room

This API is used to determine whether the user has entered a room. A bool-type value will be returned. The call is invalid during the process of room entry.

#### Function prototype  

```
ITMGContext abstract bool IsRoomEntered()
```

#### Sample code  

```
ITMGContext.GetInstance().IsRoomEntered();
```

### Switching room

This API to used to switch the user to another voice chat room. It’s called after the user enters the room. After the switching, the device is not reset, that is, if the microphone is already enabled in the previous room, the microphone is stilled enabled in the new room.
The callback for quickly switching rooms is `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM`, and the fields are `error_info` and `result`.

#### API prototype

```
public abstract int SwitchRoom(string roomID, byte[] authBuffer);
```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | ID of the room to enter |
| authBuffer | byte[] | Generates a new authentication with the ID of the room to enter |

### Cross-room mic connection

Call this API to connect the microphones across rooms after the room entry. After the calling, the local user can communicate with the target OpenID user in the target room.

#### Example
Assume that User A in Room 1 is talking with User B is in Room 2 using this API. When User C in Room 1 speaks, User B and User D in Room 2 cannot hear. User C in Room 1 can hear only the voice in Room 1 and the voice of User B in Room 2 but not other users in Room 2.

#### API prototype

```
/// <summary> Enable the room sharing, and connect the mic of the OpenID in another room.</summary>
public abstract int StartRoomSharing(string targetRoomID, string targetOpenID, byte[] authBuffer);
/// <summary> Stop the enabled room sharing.</summary>
public abstract int StopRoomSharing();
```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ------ | ----------------------- |
| targetRoomID | String | ID of the room to connect mic |
| targetOpenID | String | The target OpenID to connect mic |
| authBuffer | byte[] | Reserved flag. You just need to enter NULL. |

### Notifications of member room entry and speaking status

This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone enters or exits the room.
A notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at the upper layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds. This event only returns the member speaking event but not the specific volume level. If you need the specific volume levels of members in the room, use the `GetVolumeById` API.

| event_id | Description | Maintenance |
| --------------------------- | :------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER | Return all the openid when a member enters the room. | Member list |
| EVENT_ID_ENDPOINT_EXIT | Return all the openid when a member exits the room | Member list |
| EVENT_ID_ENDPOINT_HAS_AUDIO | Return all the chatting openid when a member sends audio packets | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO | Return all the openid that stop chatting when a member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### Sample code

```
// Delegate function:
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
// Event-triggered function:
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

// Listen on an event:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
// Process the event listened on:
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
				// Process
		    switch (eventID)
 		    {
 		    case EVENT_ID_ENDPOINT_ENTER:
  			    // A member enters the room
  			    break;
 		    case EVENT_ID_ENDPOINT_EXIT:
  			    // A member exits the room
			    break;
		    case EVENT_ID_ENDPOINT_HAS_AUDIO:
			    // A member sends audio packets
			    break;
		    case EVENT_ID_ENDPOINT_NO_AUDIO:
			    // A member stops sending audio packets
			    break;
		  
		    default:
			    break;
 		    }
		break;
}
```

### Muting in a room


This API is used to add an ID to the audio data blocked list. This operation blocks audio from someone and only applies to the local device. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is used to mute a user in a room.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | String | ID to be blocked openid |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (openId);
```

### Unmuting

This API is used to remove a user from the audio blocklist. A returned value of 0 indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)

```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | String | openId of the user to unmute|

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (openId);

```

## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/c85fe68b4b26555adf8ad01c82711f5b.png)

### Notes on voice chat audio connection

The voice chat APIs can only be called when the SDK is initialized and the user has entered the room.
When Enable/Disable Mic/Speaker is clicked on the UI, the following practices are recommended:

- Games: Call `EnableMic` and `EnableSpeaker`, which is equivalent to call both `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv`.
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback will not be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked**.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

### Voice chat audio APIs

| API                        |            Description            |
| --------------------------- | :----------------------------: |
| EnableMic | Enables/disables mic |
| GetMicState | Gets mic status |
| EnableAudioCaptureDevice | Enables/disables capturing device |
| IsAudioCaptureDeviceEnabled | Gets capturing device status |
| EnableAudioSend | Enables/disables audio upstreaming |
| IsAudioSendEnabled | Gets audio upstreaming status |
| GetMicLevel | Gets real-time mic volume |
| GetSendStreamLevel | Gets real-time audio upstreaming volume |
| SetMicVolume | Sets mic volume |
| GetMicVolume | Gets mic volume |
| EnableSpeaker | Enables/disables speaker |
| GetSpeakerState | Gets speaker status |
| EnableAudioPlayDevice | Enables/disables playback device |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv | Enables/disables audio downstreaming |
| IsAudioRecvEnabled | Gets audio downstreaming status |
| GetSpeakerLevel | Gets real-time speaker volume |
| GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
| SetSpeakerVolume | Sets speaker volume |
| GetSpeakerVolume | Gets speaker volume |
| EnableLoopBack | Enables/disables in-ear monitoring |

## Voice Chat Capturing APIs

### [Enabling or disabling the microphone](id:EnableMic)

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**


#### Function prototype  

```
ITMGAudioCtrl EnableMic(bool isEnabled)

```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | `true`: Enable the mic; `false`: Disable the mic. |

#### Sample code  

```
// Enable mic
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);

```

### Getting the mic status

This API is used to query the mic status. `0`: The mic is off. `1·: The mic is on.

#### Function prototype  

```
ITMGAudioCtrl GetMicState()

```

#### Sample code  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();

```

### Enabling or disabling capturing device

This API is used to enable/disable an audio capturing device. By default, the audio capturing device is not enabled when the user enters the room.

- This API can only be called after `EnterRoom`. The device is disabled automatically after the user exits the room.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool |`true`: Enable the capturing device; `false`: Disable the capcuring device. |

#### Sample code

```
// Enable capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);

```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()

```

#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();

```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);

```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioSendEnabled()

```

#### Sample code  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();

```

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl int GetMicLevel

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();

```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl int GetSendStreamLevel()

```

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();

```

### Setting the mic software volume

This API is used to set the mic volume. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl SetMicVolume(int volume)

```

| Parameter | Type | Description |
| ------ | :--: | --------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);

```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
ITMGAudioCtrl GetMicVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();

```

## Voice Chat Playback APIs

### [Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in** [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).

**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### Function prototype  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool |`true`: Enable the speaker; `false`: Disable the speaker. |

#### Sample code  

```
// Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);

```

### Getting the speaker status

This API is used to get the speaker status. `0`: Speaker off; `1`: Speaker on.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerState()

```

#### Sample code  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();

```



### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### Function prototype  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | `false`: Disable the device; `true`: Enable the device. |

#### Sample code  

```
// Enable the playback device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);

```

### Getting the playback device status

This API is used to get the status of a playback device.

#### Function prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()

```

#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();

```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | `true`: Enable downstreaming; `false`: Disable downstreaming. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);

```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()

```

#### Sample code  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();

```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerLevel()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();

```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)

```

| Parameter | Type | Description |
| ------ | :----: | -------------------- |
| openId | string | `openId` of another member in the room |

#### Sample code  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);

```

### Setting the speaker volume

This API is used to set the speaker volume.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

#### Function prototype  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)

```

| Parameter | Type | Description |
| ------ | :--: | -------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);

```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume, and `Volume` the speaker volume. The final volume = Level * Volume%. For example, if `Level` is 100 and `Volume` is 60, the final volume is `60`.

#### Function prototype  

```
ITMGAudioCtrl GetSpeakerVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();

```



## Advanced APIs


### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)

```

| Parameter | Type | Description |
| ------ | :--: | ------------ |
| enable | bool | Specifies whether to enable |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);

```

### Callback for device use and release

After a device is used or released in a room, a callback will be executed through a delegate function to pass a message of the event.

```
Delegate function:
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
Event-triggered function:
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;

```

| Parameter | Type | Description |
| ----------- | :----: | ----------------------------------------------------- |
| deviceType | int | <li>`1`: Capturing device, <li>`2`: Playback device |
| deviceId | string | Device GUID, which is used to identify a device and only applies to Windows and macOS. |
| openOrClose | bool | Occupies or releases a capturing/playback device |

#### Sample code  

```
Listen on an event:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
Process the event listened on:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    // Callback for device occupancy and release
}

```

### Getting user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype  

```
ITMGContext ITMGRoom public int GetRoomType()

```


#### Sample code  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();

```

### Callback for modifying the room type

#### Function prototype  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)

```


| Parameter | Type | Description |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype | ITMGRoomType | Room type to be switched to. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);


```

### Callback for modifying room audio type

Set the room type. After the room type is set, a callback will be executed through a delegate function to pass a message indicating that the modification has been completed.

| Returned Parameter | Description |
| ---------- | :------------------------: |
| roomtype | The new room type|


```
// Delegate function:
public abstract event QAVCallback OnChangeRoomtypeCallback;

// Event-triggered function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;

```

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance ().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent (OnRoomTypeChangedEvent);
// Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}


```

### Notification of room type change

Once the room type is modified by you or another user in the room, this callback function will be called to notify the business layer of the room type change. The returned value will be the room type. For more information, please see the `EnterRoom` API.

```
// Delegate function:
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

// Event-triggered function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	

```

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
// Process the event listened on:
void OnRoomTypeChangedEvent(int roomtype){
    // Send a callback after the room type is changed
}

```



### The monitoring event of room call quality

The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

This API is used to monitor the network quality. 

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1 (Worst) - 50 (Best).. `0` is the initial value and is meaningless. It’s recommended to send users alerts about poor network condition when the value is below 30. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |


### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
ITMGContext  abstract string GetSDKVersion()

```

#### Sample code  

```
ITMGContext.GetInstance().GetSDKVersion();

```





### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)

```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL | Description |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);

```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### Function prototype

```
ITMGContext  SetLogPath(string logDir)

```

| Parameter   |  Type  | Description              |
| ------ | :----: | ---- |
| logDir | String | Path |

#### Sample code  

```
ITMGContext.GetInstance().SetLogPath(path);

```

### Getting the diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### Function prototype  

```
ITMGRoom GetQualityTips()

```

#### Sample code  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```
