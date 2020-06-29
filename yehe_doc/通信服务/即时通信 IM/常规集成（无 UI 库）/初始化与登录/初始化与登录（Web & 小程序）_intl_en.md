## Creating an SDK Instance

### Web project

<pre>
import TIM from 'tim-js-sdk';
// COS SDK for sending messages such as images and files
import COS from "cos-js-sdk-v5";


let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK log level for output. For more information on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level. We recommend that you use this level during connection as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. We recommend that you use this log level in a production environment.

// Register the COS SDK plugin.
tim.registerPlugin({'cos-js-sdk': COS});
</pre>

### Mini Program project

<pre>
import TIM from 'tim-wx-sdk';
// COS SDK for sending messages such as images and files
import COS from "cos-wx-sdk-v5";


let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting.
};
// Create an SDK instance. The `TIM.create()` method returns the same instance for the same `SDKAppID`.
let tim = TIM.create(options); // The SDK instance is usually represented by tim.

// Set the SDK log level for output. For more information on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0); // Common level. We recommend that you use this level during connection as it covers more logs.
// tim.setLogLevel(1); // Release level, at which the SDK outputs important information. We recommend that you use this log level in a production environment.

// Register the COS SDK plugin.
tim.registerPlugin({'cos-wx-sdk': COS});
</pre>

## Setting the Log Level

<pre>
// Set the SDK log level for output. For more information on each level, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setLogLevel">setLogLevel API Description</a>.
tim.setLogLevel(0);
</pre>

## Binding Events

<pre>
// Monitored events, for example:
tim.on(TIM.EVENT.SDK_READY, function(event) {
  // A notification is received, indicating that the offline message and conversation lists were synchronized successfully. The access side can call APIs that require authentication, such as sendMessage.
  // event.name - TIM.EVENT.SDK_READY
});


tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // A newly pushed one-to-one message, group message, group tip, or group system notification is received. You can traverse `event.data` to obtain the message list and render it to the UI.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - An array that stores Message objects - [Message]
});

tim.on(TIM.EVENT.MESSAGE_REVOKED, function(event) {
  // The message recall notification is received.
  // event.name - TIM.EVENT.MESSAGE_REVOKED
  // event.data - An array that stores Message objects - [Message] - The isRevoked value of each Message object is true.
});

tim.on(TIM.EVENT.CONVERSATION_LIST_UPDATED, function(event) {
  // A conversation list update notification is received. You can traverse `event.data` to obtain the conversation list and render it to the UI.
  // event.name - TIM.EVENT.CONVERSATION_LIST_UPDATED
  // event.data - An array that stores Conversation objects - [Conversation]
});

tim.on(TIM.EVENT.GROUP_LIST_UPDATED, function(event) {
  // A group list update notification is received. You can traverse `event.data` to obtain the group list and render it to the UI.
  // event.name - TIM.EVENT.GROUP_LIST_UPDATED
  // event.data - An array that stores Group objects - [Group]
});

tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, function(event) {
  // A new group system notification is received.
  // event.name - TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED
  // event.data.type - Type of group system notifications. For more information, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">Description of operationType enumerated values</a> for GroupSystemNoticePayload.
  // event.data.message - Message objects, which can render event.data.message.content to the UI
});

tim.on(TIM.EVENT.PROFILE_UPDATED, function(event) {
  // A notification is received, indicating that your own profile or your friend's profile is updated.
  // event.name - TIM.EVENT.PROFILE_UPDATED
  // event.data - An array that stores Profile objects - [Profile]
});

tim.on(TIM.EVENT.BLACKLIST_UPDATED, function(event) {
  // A blacklist update notification is received.
  // event.name - TIM.EVENT.BLACKLIST_UPDATED
  // event.data - An array that stores userIDs - [userID]
});

tim.on(TIM.EVENT.ERROR, function(event) {
  // An SDK error notification is received. The error code and error message can be obtained from this notification.
  // event.name - TIM.EVENT.ERROR
  // event.data.code - Error code
  // event.data.message - Error message
});

tim.on(TIM.EVENT.SDK_NOT_READY, function(event) {
  // An SDK not-ready notification is received. At this time, the SDK cannot function normally.
  // event.name - TIM.EVENT.SDK_NOT_READY
});

tim.on(TIM.EVENT.KICKED_OUT, function(event) {
  // A forced offline notification is received.
  // event.name - TIM.EVENT.KICKED_OUT
  // event.data.type - Reason for forcible offline, for example:
  //    - TIM.TYPES.KICKED_OUT_MULT_ACCOUNT: forced offline due to multi-instance login
  //    - TIM.TYPES.KICKED_OUT_MULT_DEVICE: forced offline due to multi-device login
  //    - TIM.TYPES.KICKED_OUT_USERSIG_EXPIRED: forced offline due to UserSig expiration (supported from V2.4.0) 
});

 tim.on(TIM.EVENT.NET_STATE_CHANGE, function(event) { 
  // The network status changes (supported from V2.5.0). 
  // event.name - TIM.EVENT.NET_STATE_CHANGE 
  // event.data.state indicates the current network status. The enumerated values are described as follows: 
  //     \- TIM.TYPES.NET_STATE_CONNECTED: already connected to the network 
  //     \- TIM.TYPES.NET_STATE_CONNECTING: connecting. This often occurs when the SDK must reconnect due to network jitter. The "The current network is unstable" or "Connecting..." prompt can be displayed at the access side based on this status. 
  //    \- TIM.TYPES.NET_STATE_DISCONNECTED: disconnected. The "The current network is unavailable" prompt can be displayed at the access side based on this status. The SDK will continue to try to reconnect. If the user network restores, the SDK will automatically synchronize messages.  
});

  // Start to log in to the SDK 
   tim.login({userID: 'your userID', userSig: 'your userSig'}); </pre>

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| --------- | -------- | ----------- |
| `options` | `Object` | Application configuration |

The following table describes `options`.

| Name | Type | Description |
| ---------- | -------- | ----------------------- |
| `SDKAppID` | `Number` | `SDKAppID` of the IM application |

For more information on how to initialize the SDK and use APIs, see [SDK Initialization](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html).

## Login

You can send and receive messages in the IM console only after logging in to the IM SDK. To log in to the IM SDK, you need to provide information including the UserID and UserSig. For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). After successful login, to call APIs that require authentication such as [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage), you must wait until the SDK enters the ready state. You can obtain the status of the SDK by monitoring events. For more information, see [TIM.EVENT.SDK_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_READY).

> By default, multi-instance login is not supported. If you use an account that has been logged in to on another page to log in on the current page, the account may be forcibly logged out on the other page, which will trigger the `TIM.EVENT.KICKED_OUT` event. You can proceed accordingly after detecting the event by listening. A listening example for multi-instance login is as follows:

```javascript
let onKickedOut = function (event) {
  console.log(event.data.type); // mutipleAccount (The same account that is used to log in on multiple pages on the same device is forcibly logged out.)
};
tim.on(TIM.EVENT.KICKED_OUT, onKickedOut);
```

To support multi-instance login (allowing the use of the same account to log in concurrently on multiple pages), log in to the [IM console](https://console.cloud.tencent.com/im), find the corresponding SDKAppID, and choose **App Configuration** > **Feature Configuration** > **Login and Messages** > **Number of Concurrent Online Web Instances** to configure the number of instances. The configuration will take effect within 50 minutes.

**API name**

```javascript
tim.login(options)
```

**Request parameters**

| Name | Type | Description |
| ------- | ------ | ------------------------------------------------------------ |
| UserID | String | ID of the user |
| UserSig | String | Password for logging in to the IM console. It is essentially the ciphertext generated by encrypting the information such as the UserID.<br/>For the detailed generation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |

**Return values**

This API returns a `Promise` object.

**Example**

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Logged in successfully
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about the login failure
});
```



## Logout

 This API is used to log out of the IM console. It is usually called when you switch between accounts. This API clears the login status of the current account and all data in the memory. 

>
>
>- When calling this API, the instance triggers the [SDK_NOT_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_NOT_READY) event. In this case, the instance is automatically logged out and cannot receive or send messages.
>- Assume that the value of **Number of Concurrent Online Web Instances** configured in the [IM console](https://console.cloud.tencent.com/im) is greater than 1, and the same account has been used to log in to instances `a1` and `a2` (including a Mini Program instance). After `a1.logout()` is executed, `a1` is automatically logged out and cannot receive or send messages, whereas `a2` is not affected.
>- Assume that the **Number of Concurrent Online Web Instances** is set to 2, and your account has been used to log in to instances `a1` and `a2`. When you use this account to log in to instance `a3`, either `a1` or `a2` will be forcibly logged out. In most cases, the instance that first entered the login state is forcibly logged out. If `a1` is forcibly logged out, a logout process is executed within `a1` and the [KICKED_OUT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.KICKED_OUT) event is triggered. The access side can monitor this event and redirect to the login page when the event is triggered. In this case, `a1` is forcibly logged out, whereas instances `a2` and `a3` can continue to run properly.

**API name**

```js
tim.logout();
```

**Request parameters**

None.

**Return value**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` is a null object, which indicates that logout succeeded.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.logout();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Logged out successfully
}).catch(function(imError) {
  console.warn('logout error:', imError);
});
```

