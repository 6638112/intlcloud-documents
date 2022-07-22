`TRTCVoiceRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create an audio chat room and become a speaker, or enter an audio chat room as a listener.
- The room owner can invite a listener to speak as well as remove a speaker from the seat.
- The room owner can also block a seat. Listeners cannot request to take a blocked seat.
- A listener can request to speak and become a speaker. A speaker can also become a listener.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

`TRTCVoiceRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, see [Audio Chat Room (iOS)](https://intl.cloud.tencent.com/document/product/647/37287).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: The `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the seat list, and invitation signaling is used to send requests to speak or invite others to speak.


<h2 id="TRTCVoiceRoom">TRTCVoiceRoom API Overview</h2>

### Basic SDK APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where event callbacks are. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets profile. |

### Room APIs

| API | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates a room (called by room owner). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Terminates a room (called by room owner). |
| [enterRoom](#enterroom) | Enters a room (called by listener). |
| [exitRoom](#exitroom) | Exits a room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.                                     |
| [getUserInfoList](#getuserinfolist) | Gets the user information of the specified `userId`. If the value is `nil`, the information of all users in the room is obtained. |

### Seat management APIs

| API                                             | Description                                                         |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [moveSeat](#moveseat) | Changes the seat (called by speaker).    |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker).    |
| [pickSeat](#pickseat)   | Places a user in a seat (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |
| [muteSeat](#muteseat)   | Mutes/Unmutes a seat (called by room owner). |
| [closeSeat](#closeseat) | Blocks/Unblocks a seat (called by room owner).          |

### Local audio APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Starts mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Sets whether to play sound from the device’s speaker or receiver.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | Enables/Disables in-ear monitoring.       |


### Remote audio APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | Mutes/Unmutes a specified member. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all members. |

### Background music and audio effect APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager). |

### Message sending APIs

| API                                     | Description                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text chat message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Invitation signaling APIs

| API                                             | Description                                                         |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | Sends an invitation. |
| [acceptInvitation](#acceptinvitation) | Accepts an invitation.       |
| [rejectInvitation](#rejectinvitation) | Declines an invitation.       |
| [cancelInvitation](#cancelinvitation) | Cancels an invitation.       |

<h2 id="TRTCVoiceRoomDelegate">TRTCVoiceRoomDelegate API Overview</h2>

### Common event callbacks

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Callback for error. |
| [onWarning](#onwarning) | Callback for warning. |
| [onDebugLog](#ondebuglog) | Callback of log.|

### Room event callback APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)     | The room was terminated.       |
| [onRoomInfoChange](#onroominfochange)     | The room information changed. |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Seat list change callback APIs

| API                                     | Description                                  |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   | All seat changes                |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker or was made a speaker by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was made a listener by the room owner. |
| [onSeatMute](#onseatmute) | The room owner muted a seat. |
| [onUserMicrophoneMute](#onusermicrophonemute)               | Whether a user’s mic is muted                          |
| [onSeatClose](#onseatclose)             | The room owner blocked a seat.                          |

### Callback APIs for room entry/exit by listener

| API                                             | Description                                                         |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | A text chat message was received.  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received.|

### Signaling event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | An invitation was received. |
| [onInviteeAccepted](#oninviteeaccepted)           | The invitee accepted the invitation.   |
| [onInviteeRejected](#oninviteerejected)           |  The invitee declined the invitation.   |
| [onInvitationCancelled](#oninvitationcancelled)   | The inviter canceled the invitation. |

## Basic SDK APIs

[](id:sharedInstance)

### sharedInstance

This API is used to get a [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) singleton object.

```Objective-C
/**
* Get a `TRTCVoiceRoom` singleton object
*
* - returns: `TRTCVoiceRoom` instance
* - note: to terminate a singleton object, call {@link TRTCVoiceRoom#destroySharedInstance()}.
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

This API is used to terminate a [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) singleton object.

>?After the instance is terminated, the externally cached `TRTCVoiceRoom` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```Objective-C
/**
* Terminate a `TRTCVoiceRoom` singleton object
*
* - Note: After the instance is terminated, the externally cached `TRTCVoiceRoom` instance can no longer be used. You need to call {@link TRTCVoiceRoom#sharedInstance()} again to get a new instance.
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

This API is used to set the event callback of [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287). You can use `TRTCVoiceRoomDelegate` to get different status notifications of [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286).

```Objective-C
/**
* Set the event callbacks of the component
* 
* You can use `TRTCVoiceRoomDelegate` to get different status notifications of `TRTCVoiceRoom`
*
* - parameter delegate Callback API
* - Note: Callback events in `TRTCVoiceRoom` are called back to you in the main queue by default. If you need to specify a queue for event callback, use {@link TRTCVoiceRoom#setDelegateQueue(queue)}.
*/
- (void)setDelegate:(id<TRTCVoiceRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?`setDelegate` is the delegate callback of `TRTCVoiceRoom`.   

### setDelegateQueue

This API is used to set the thread queue for event callbacks. The main thread (MainQueue) is used by default.

```Objective-C
/**
* Set the queue for event callbacks
*
* - parameter queue Queue. Various status callback notifications in `TRTCVoiceRoom` will be sent to the queue you specify.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | The status notifications of `TRTCVoiceRoom` are sent to the thread queue you specify. |

   

### login

Login

```Objective-C
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userId   | NSString            | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_) |
| userSig  | NSString       | Tencent Cloud's proprietary security signature. For how to calculate and use it, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The code is 0 if login succeeds. |

   

### logout

Log out

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | Callback for logout. The code is `0` if logout succeeds. |

   

### setSelfProfile

This API is used to set the profile.

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | ----------------------------------- |
| userName  | NSString            | Username                                |
| avatarURL | NSString                                    | Profile picture URL                          |
| callback | ActionCallback | Callback for profile setting. The code is `0` if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```Objective-C
- (void)createRoom:(int)roomID roomParam:(VoiceRoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | The room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a karaoke room list. Currently, Tencent Cloud does not provide management services for room lists. Please manage your own room lists. |
| roomParam | VoiceRoomParam | Room information, such as room name, seat list information, and cover information. To manage seats, you must enter the number of seats in the room. |
| callback | ActionCallback | Callback for room creation. The code is 0 if the operation succeeds.  |

The process of creating a karaoke room and becoming a speaker is as follows: 
1. A user calls `createRoom` to create an audio chat room, passing in room attributes (e.g. room ID, whether listeners require room owner’s consent to speak, number of seats).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
4. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room termination. The code is `0` if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| roomId   | NSInteger            | The room ID.                            |
| callback | ActionCallback | Callback for room entry. The code is `0` if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest audio chat room list from your server. The list may contain the `roomId` and room information of multiple audio chat rooms.
2. The user selects a room, and calls `enterRoom` with the room ID passed in to enter the room.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
4. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom

Leave room

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room exit. The code is `0` if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don’t need this API if both the room list and room information are managed on your server.


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(VoiceRoomInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------------------- | ------------------ |
| roomIdList | NSArray&lt;NSNumber&gt; | Room ID list       |
| callback | RoomInfoCallback | Callback of room details |


### getUserInfoList

This API is used to get the information of specific users (`userId`).

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(VoiceRoomUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

The parameters are described below:

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | NSArray&lt;NSString&gt; | IDs of the users to query. If this parameter is `null`, the information of all users in the room is queried. |
| userlistcallback | UserListCallback   | Callback of user details                                           |


## Seat Management APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger      | Number of the seat to take |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner’s consent to take a seat, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call this API.

### moveSeat
This API is used to change one’s seat (called by speaker).
>? After the seat change, all users in the room will receive the `onSeatListChange`, `onAnchorLeaveSeat`, and `onAnchorEnterSeat` notifications. This API will only change the user’s seat number, not the user role.

```Objective-C
- (NSInteger)moveSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback
NS_SWIFT_NAME(moveSeat(seatIndex:callback:))
```
The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger      | Number of the seat to change to |
| callback | ActionCallback | Callback for the operation |

Response parameters:

| Parameter | Type | Description |
| -------- | --------- | --------------------- |
| code | NSInteger | Result of seat change. `0`: operation successful; `10001`: API rate limit exceeded; other values: operation failed |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner’s consent to take a seat, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call this API.

### leaveSeat

This API is used to become a listener (called by speaker).

>? After a speaker becomes a listener, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for the operation |

### pickSeat

This API is used to place a user in a seat (called by room owner).

>? After the room owner places a user in a seat, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger      | Number of the seat to place the user in|
| userId | NSString  | User ID            |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where the room owner needs listeners’ consent to make them speakers, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `pickSeat`.


### kickSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```Objective-C
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger      | Seat number of the speaker to remove|
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list.

### muteSeat

This API is used to mute/unmute a seat (called by room owner).

>? After a seat is muted/unmuted, all members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | NSInteger      | Number of the seat to mute/unmute                          |
| isMute    | BOOL           | `YES`: mute the seat; `NO`: unmute the seat |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will call `muteAudio` to mute/unmute his or her audio.

### closeSeat

This API is used to block/unblock a seat (called by room owner).

>? After a seat is blocked/unblocked, all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | NSInteger      | Number of the seat to block/unblock                          |
| isClose   | BOOL           | `YES`: block the seat; `NO`: unblock the seat |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will leave the seat.


## Local Audio APIs

### startMicrophone

This API is used to start mic capturing.

```Objective-C
- (void)startMicrophone;
```

### stopMicrophone

This API is used to stop mic capturing.

```Objective-C
- (void)stopMicrophone;
```

### setAudioQuality

This API is used to set audio quality.

```Objective-C
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ---------- | ------------------------------------------------------------ |
| quality | NSInteger | The audio quality. For more information, see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

The parameters are described below:

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------------------------ |
| mute | BOOL | Whether to mute or unmute audio. For more information, see [muteLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to set whether to play sound from the device’s speaker or receiver.

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------- | --------------------------- |
| useSpeaker | BOOL    | `YES`: speaker; `NO`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | ----------------------------- |
| volume | NSInteger | Capturing volume. Value range: 0-100. Default value: 100 |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---------- | ----------------------------- |
| volume | NSInteger | Playback volume. Value range: 0-100. Default value: 100 |

### muteRemoteAudio

This API is used to mute/unmute a specified user.

```Objective-C
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | --------------------------------- |
| userId   | NSString  | ID of the user to mute/unmute                                             |
| mute | BOOL | `YES`: mute; `NO`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all users.

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------- | --------------------------------- |
| mute | BOOL | `YES`: mute; `NO`: unmute |

### setVoiceEarMonitorEnable

This API is used to enable/disable in-ear monitoring.

```Objective-C
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------- | --------------------------------- |
| enable | BOOL | `YES`: enable in-ear monitoring; `NO`: disable in-ear monitoring |


## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text chat message in a room, which is generally used for on-screen comments.

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| message  | NSString            | Text message     |
| callback | ActionCallback | Callback for the operation |

   

### sendRoomCustomMsg

This API is used to send a custom text message.

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | NSString            | Custom command word used to distinguish between different message types |
| message  | NSString            | Text message                                         |
| callback | ActionCallback | Callback for the operation |

   

## Invitation Signaling APIs

### sendInvitation

This API is used to send an invitation.

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ---------------- |
| cmd      | NSString         | Custom command of business |
| userId   | NSString  | ID of the user to invite                                             |
| content  | NSString         | Invitation content     |
| callback | ActionCallback | Callback for the operation |

Response parameters:

| Parameter | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | NSString | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(id:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | NSString       | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

### rejectInvitation

This API is used to decline an invitation.

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(id:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | NSString       | Invitation ID      |
| callback | ActionCallback | Callback for the operation |


### cancelInvitation

This API is used to cancel an invitation.

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(id:callback:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | NSString       | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

[](id:TRTCVoiceRoomDelegate)
## TRTCVoiceRoomDelegate Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending if necessary.

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | NSString  | Error message |


### onWarning

Callback for warning.

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | NSString | Warning message |

   

### onDebugLog

Callback for log.

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | NSString | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```Objective-C
- (void)onRoomDestroy:(NSString *)roomId
NS_SWIFT_NAME(onRoomDestroy(roomId:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | --------- |
| roomId | NSString | Room ID |


### onRoomInfoChange

Callback for change of room information. This callback is sent after successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```Objective-C
- (void)onRoomInfoChange:(VoiceRoomInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| roomInfo | VoiceRoomInfo | Room information |


### onUserMicrophoneMute

Callback of whether a user’s mic is muted. When a user calls `muteLocalAudio`, all members in the room will receive this callback.

```Objective-C
- (void)onUserMicrophoneMute:(NSString *)userId mute:(BOOL)mute
NS_SWIFT_NAME(onUserMicrophoneMute(userId:mute:));

```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------- |
| userId | NSString  | User ID            |
| mute | BOOL    | `YES`: muted;  `NO`: unmuted |


### onUserVolumeUpdate

Notification to all members of the volume after the volume reminder is enabled.

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------- |
| userVolumes | NSArray | List of user volumes                 |
| totalVolume | NSInteger    | Total volume. Value range: 0-100 |


## Seat Callback APIs

### onSeatListChange

Callback for all seat changes.

```Objective-C
- (void)onSeatInfoChange:(NSArray<VoiceRoomSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------------ | -------------------- | ---------------- |
| seatInfoList | NSArray&lt;VoiceRoomSeatInfo&gt; | Full seat list |

### onAnchorEnterSeat

Someone became a speaker or was made a speaker by the owner.

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | -------------------- |
| index | NSInteger      | Number of the seat taken     |
| user  | VoiceRoomUserInfo | Information of the user who left the seat |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | -------------------- |
| index | NSInteger      | Number of the seat the user left         |
| user  | VoiceRoomUserInfo | Information of the user who left the seat |

### onSeatMute

The room owner muted/unmuted a seat.

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | ---------------------------------- |
| index  | NSInteger     | The seat muted/unmuted                       |
| isMute | BOOL | `YES: The seat was muted; `NO`: The seat was unmuted. |

### onSeatClose

The room owner blocked/unblocked a seat.

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------- | ----------------------------------- |
| index   | NSInteger     | The seat blocked/unblocked                        |
| isClose | BOOL | `YES`: The seat was blocked; `NO`: The seat was unblocked. |

## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```Objective-C
- (void)onAudienceEnter:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | Information of the listener who entered |

### onAudienceExit

A listener exited the room.

```Objective-C
- (void)onAudienceExit:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | Information of the user who left |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

Callback for receiving a text chat message.

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------------- |
| message | NSString            | Text message       |
| userInfo | VoiceRoomUserInfo | Information of the sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)command
                    message:(NSString *)message
                   userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(command:message:userInfo:));
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------- | -------------------------------------------------- |
| command | NSString            | Custom command word used to distinguish between different message types |
| message  | NSString            | Text message                                         |
| userInfo | VoiceRoomUserInfo | Information of the sender                                   |

## Invitation Signaling Callback APIs

### onReceiveNewInvitation

An invitation was received.

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(id:inviter:cmd:content:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | -------- | ---------------------------------- |
| id      | NSString   | Invitation ID                          |
| inviter | NSString | Inviter’s user ID |
| cmd     | NSString   | Custom command word specified by business |
| content | NSString | Content specified by business |

### onInviteeAccepted

The invitee accepted the invitation

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(id:invitee:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | NSString   | Invitation ID                          |
| invitee | NSString | Invitee’s user ID |

### onInviteeRejected

The invitee declined the invitation

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(id:invitee:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | NSString   | Invitation ID                          |
| invitee | NSString | Invitee’s user ID |

### onInvitationCancelled

The inviter canceled the invitation.

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(id:invitee:));
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ----------------- |
| id      | NSString | Invitation ID         |
| inviter | NSString   | Inviter’s user ID                  |
