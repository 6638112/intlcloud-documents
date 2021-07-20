`TRTCCalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one audio/video calls. For detailed instructions how to implement it, see [Real-Time Audio Call (Flutter)](https://intl.cloud.tencent.com/zh/document/product/647).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047) is used to send and process signaling messages.


<h2 id="TRTCCalling">`TRTCCalling` API Overview</h2>

### Basic SDK APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | Gets a singleton.                                       |
| [destroySharedInstance](#destroysharedinstance) | Destroys a singleton. |
| [registerListener](#registerlistener)                     | Registers an event listener.                                   |
| [unRegisterListener](#unregisterlistener)               | Unregisters an event listener.                                   |
| [destroy](#destroy)                             | Destroys an instance that is no longer needed.    |
| [login](#login)                                 | Logs in. All features can be used only after login. |
| [logout](#logout)                               | Logs out. No calls can be made after logout.         |


### Call operation APIs

| API                                             | Description                                                         |
| ----------------------- | -------------- |
| [call](#call)           | Makes a one-to-one call. |
| [accept](#accept) | Accepts the current call. |
| [reject](#reject) | Declines the current call. |
| [hangup](#hangup) | Ends the current call. |


### Audio control APIs

| API                                             | Description                                                         |
| ----------------------------- | ------------------------------------------------ |
| [setMicMute](#setmicmute)     | Mutes the local mic.                                   |
| [setHandsFree](#sethandsfree) | Enables the hands-free mode.                                       |

<h2 id="TRTCCallingDelegate">`TRTCCallingDelegate` API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------- | ---------- |
| [onError](#onerror) | Error |

### Inviter callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------------- |
| [onReject](#onreject) | The call was declined. |
| [onNoResp](#onnoresp) | The invitee did not answer. |
| [onLineBusy](#onlinebusy) | The line is busy. |

### Invitee callback APIs

| API | Description |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | An invitation was received.     |
| [onCallingCancel](#oncallingcancel) | The call was canceled. |
| [onCallingTimeOut](#oncallingtimeout) | The call timed out. |

### General callback APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| 
| [onUserEnter](#onuserenter)                                  | A user joined the call.         |
| [onUserLeave](#onuserleave)                                  | A user left the call.         |
| [onUserAudioAvailable](#onuseraudioavailable) | Whether a user is sending audio |
| [onUserVoiceVolume](#onuservoicevolume)                      | Call volume of a user         |
| [onCallEnd](#oncallend)                                      | The call ended.             |

## Basic SDK APIs

### sharedInstance

This API is used to get a singleton of the `TRTCCalling` component.

```java
static Future<TRTCCalling> sharedInstance();
```

### destroySharedInstance

This API is used to destroy a singleton of the `TRTCCalling` component.

```java
static void destroySharedInstance();
```

### destroy

This API is used to destroy an instance that is no longer needed.

```java
void destroy();
```

### registerListener

This API is used to register callbacks for [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) events. You can receive status notifications of [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) via `TRTCCallingDelegate`.

```java
void registerListener(VoiceListenerFunc func);
```


### unRegisterListener

This API is used to unregister event callbacks.

```java
void unRegisterListener(VoiceListenerFunc func);
```

### login

This API is used to log in to the component.

```java
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | UInt32 | You can view the `SDKAppID` on **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For more information on how to obtain it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

### logout

This API is used to log out of the component.

```java
Future<ActionCallback> logout();
```

## Call Operation APIs

### call

This API is used to make a one-to-one call. It can be called during a call to invite more users.

```java
Future<ActionCallback> call(String userId, int type);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | -------------------------------- |
| userId | String | User ID of the callee |
| type | int | `1`: audio call; `2`: video call |

### accept

This API is used to accept the current call. After receiving the `onInvited()` callback, the invitee can call this API to accept the call.

```java
Future<ActionCallback> accept();
```

### reject

This API is used to decline the current call. After receiving the `onInvited()` callback, the invitee can call this API to decline the call.

```java
Future<ActionCallback> reject();
```

### hangup

This API is used to end the current call.

```java
void hangup();
```


## Audio Control APIs

### setMicMute

This API is used to mute the local mic.

```java
void setMicMute(bool isMute);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | ------------------------------------------- |
| isMute | bool | `true`: mutes the mic; `false`: unmutes the mic. |

### setHandsFree

This API is used to enable the hands-free mode.

```java
void setHandsFree(bool isHandsFree);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ------- | --------------------------------------- |
| isHandsFree | bool | `true`: enables the hands-free mode; `false`: disables the hands-free mode. |

## `TRTCCallingDelegate` Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>?This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------ | ---------- |
| code    | int    | Error code   |
| msg  | String | Error message |


## Inviter Callback APIs

### onReject

The call was declined.

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | --------------- |
| userId | String | User ID of the invitee who declined the call |

### onNoResp

The invitee did not answer.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | User ID of the invitee who did not answer |

### onLineBusy

The line is busy.


The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | --------------- |
| userId | String | User ID of the invitee whose line is busy |

## Invitee Callback APIs

### onInvited

A call invitation was received.

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | User ID of the inviter                    |
| userIds     | List&lt;String&gt; | IDs of other users invited         |
| isFromGroup | bool          | Whether it is a group call               |
| type        | int                | `1`: audio call; `2`: video call |

### onCallingCancel

The call was canceled. The invitee will receive this callback if the inviter cancels the invitation before he or she handles it.


### onCallingTimeOut

The call timed out.


## General Callback APIs

### onUserEnter

A user joined the call.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | ID of the user who joined the call |

### onUserLeave

A user left the call.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | ID of the user who left the call |

### onUserAudioAvailable

Whether a user is sending audio.

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | ------- | ------------------ |
| userId | String | User ID |
| available | boolean | Whether the user has available audio |


### onUserVoiceVolume

Call volume of a user.

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------------------- | ------------------------------------------------------------ |
| userVolumes | List | Volume of every speaking user in the room. Value range: 0-100. |
| totalVolume | int | Total volume of all remote users. Value range: 0-100. |

### onCallEnd

The call ended.
