### 2.9.3 @2021.2.3

**Changed**

If a user haven’t joined a group (not an audio-video group), calling [quitGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#quitGroup) will return error code 2623, indicating that the user is not in the group.

**Fixed**

`avatar` (profile photo) or `nick` (nickname) was inconsistent in the C2C conversation message list.

### 2.9.2 @2021.1.26

**Added**

- Support for sending and receiving C2C messages with `avatar` (profile photo) and `nick` (nickname) displayed.
- Support for the Tencent Cloud IM upload plugin [tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin). This plugin enables more secure file upload, supports web, WeChat, QQ, Baidu, Toutiao, and Alipay Mini Program platforms, and is merely 26 KB. For more information, see [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin).

**Fixed**

- When a user joined an audio-video group anonymously after logging out, the error code 70402 was returned in the response packet during a long polling.
- The browser environment was misjudged during Taro 3.0+ integration.
- When the image type and size verification failed, there were errors in the returned data structure.



### 2.9.1 @2020.12.23
**Fixed**

A compilation error occurred when [tim-wx-sdk.js](https://www.npmjs.com/package/tim-wx-sdk) was imported into the basic library 2.14.1 of WeChat Developer Tools.


### 2.9.0 @2020.12.15
**Added**

- The [createTextAtMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage) API allows users to specify @ a specific member or @ all members during a group chat.
- [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) added the `namecard` attribute to display group members’ group name cards (i.e., their nicknames in a group).


### 2.8.5 @2020.11.23
**Changed**

The [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) API can be called when the SDK is not ready.

**Fixed**

- Errors occurred in SDK operations when read receipts and read notifications existed at the same time.
- Attempts to anonymously re-join an audio-video group after logout failed.
- The group list was cleared abnormally.

### 2.8.4 @2020.11.4
**Added**

- The WeChat, QQ, Baidu, Toutiao, and Alipay Mini Program platforms are supported (currently on the Baidu, Toutiao, and Alipay Mini Program platforms, image, video, or file messages, or other messages that need to be uploaded to COS, cannot be sent).
- The third-party frameworks of MPX and uni-app are supported.

### 2.8.1 @2020.10.29

**Added**

Images in BMP format can be sent.

**Changed**

`unreadCount` and `lastMessage` of the [conversation object](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html) are not updated when the sender sends an online message and the recipient receives the online message.

**Fixed**

The SDK could not enter the ready state due to problems synchronizing the list of recent contacts.


### 2.8.0 @2020.10.20

**Added**

- [getGroupOnlineMemberCount](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupOnlineMemberCount) was added to query of the number of online users in an audio-video group.
- Image compression was integrated in the sending of image messages. The access side can choose to display the original image or thumbnail image based on business requirements. For more information, see [ImagePayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.ImagePayload).

**Fixed**

Compatibility issues when Taro 3.x integrates WebIM

**Changed**

Reduced the SDK size. The size of [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk) was reduced by 8.5%, and that of [tim-wx-sdk](https://www.npmjs.com/package/tim-wx-sdk) was reduced by 15%.


### 2.7.8 @2020.9.24

**Added**

The [TIM.create](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html#.create) API added the `oversea` parameter. When this parameter is set to `true`, the SDK uses a domain name outside the Chinese mainland to avoid interference.

**Fixed**

- The return value for calling relevant APIs was `undefined` when the SDK was in the `not ready` state.
- Issues related to statistics


### 2.7.7 @2020.8.12

**Added**

Added the [TIM.EVENT.SDK_RELOAD](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_RELOAD) event.

**Fixed**

- Audio-video groups occasionally failed to pull messages in cases where the network was reconnected after a long disconnection or the Mini Program switched to the foreground after running in the background for a long time.
- The type and value of imageFormat of an image message were inconsistent with those of the actual image.
- The nicknames displayed in work groups and public groups were incorrect.


### 2.7.6 @2020.7.9

**Fixed**

Messages occasionally failed to be pulled if an audio-video group (AVChatRoom) was used for a long time.

### 2.7.5 @2020.7.2

**Fixed**

After the RESTful API for [creating a work group](https://intl.cloud.tencent.com/document/product/1047/34895) was called to create a work group successfully and the group members were specified, messages from group members would fail to be sent.


### 2.7.2 @2020.6.30

**Fixed**

- Occasionally, when [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) was called, the SDK prompted "Already in the group" but in fact the user was not in the group. Consequently, the user could not send or receive messages.
- The count of messages sent in a temporary meeting group was incorrect.

### 2.7.0 @2020.6.8

**Added**

Provided support for C2C message read receipts (indicating whether the peer has read your messages). For more information, see the event [TIM.EVENT.MESSAGE_READ_BY_PEER](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_READ_BY_PEER). In a [message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) that has already been read by the peer, the value of `isPeerRead` is `true`.

**Fixed**

- After a user joined a chat room (ChatRoom), the newly created conversation did not display the last message.
- After login, a user who had not joined an audio-video group (AVChatRoom) could still send a message to the audio-video group (AVChatRoom).


### 2.6.6 @2020.5.27

**Fixed**

- In audio-video groups (AVChatRoom), messages were occasionally repeatedly displayed on the screen.
- An error was reported when [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) received an empty message.
- If [login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login) was called again after [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout), error 70001 occasionally occurred when [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) was called.

### 2.6.4 @2020.5.8

**Added**

The [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) API added the sending option to support the sending of online messages (no offline or roaming messages; cannot be used for AVChatRoom or BChatRoom) and the configuration of [offline push](https://intl.cloud.tencent.com/document/product/1047/33525).

### 2.6.3 @2020.4.26

**Fixed**

- Message content was lost because the input `payload.data payload.extension` type of [createCustomMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createCustomMessage) is incorrect.
- Multiple messages contained in a response to a single request were disordered.
- The unread count could not be cleared occasionally after the read count is reported because the number of unread C2C conversions overflows.
- [TIM.EVENT.ERROR](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.ERROR) `event.data.code` and `event.data.undefined` were undefined occasionally.

### 2.6.2 @2020.4.16

**Added**

- [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) supports muting and unmuting all.
- [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) can get the group member muting deadline timestamp [muteUntil](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**Fixed**

The unread count could not be cleared when the latest group message was a group prompt.

### 2.6.1 @2020.4.8

**Fixed**

Files could not be uploaded occasionally when the uploaded COS signature was invalid and not updated in a timely manner.


### 2.6.0 @2020.3.30

**Added**
- The web client can create and send video messages [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage) of up to 100 MB in size.
- The `nick` and `avatar` properties are added in [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) to display the nickname and profile photo address of the message sender in an audio-video group. The nickname and profile photo address need to be set in advance by calling [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile).
- When an account logs in on multiple instances, namely, multiple webpages or web browsers, the C2C message cancellation notification can be synchronized between these webpages or web browsers.
- After [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) is called to successfully modify custom group fields, group members can receive group prompts and obtain related content [Message.payload.newGroupProfile.groupCustomField](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).

**Changed**

[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) is deprecated and replaced by [MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED).

**Fixed**

Errors occurred occasionally when the [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) API was called.

### 2.5.2 @2020.3.13

**Changed**

When [searchGroupByID](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#searchGroupByID) fails, the log level is degraded to warning and the prompt text is modified.

**Fixed**

- Anonymous users or visitors failed to join [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups and had statistical problems.
- Other known issues

### 2.5.1 @2020.3.5

**Changed**

When [login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#login) is successful, key value pair `repeatLogin: true` is added for the `imResponse.data` callback object to identify repeated login of a login account.

**Fixed**

The priority of messages received at the receiver side of an audio-video group is different from that set on the sender side.

### 2.5.0 @2020.2.28
**Added**
- The network status change event [TIM.EVENT.NET_STATE_CHANGE](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.NET_STATE_CHANGE) is added, and the access side can make related prompts and guidance based on this event.
- Running in WeChat Mini Program plug-in environments is supported.

**Changed**
[Error codes](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html) are reduced and optimized.

**Fixed**
- After an audio-video group was created in the [console](https://console.cloud.tencent.com/im) and a group owner was specified, messages sent by other group members will be repeated on the group owner side after the group owner joins the group.
- When groups were created and terminated in the [console](https://console.cloud.tencent.com/im) or using a RESTful API frequently, the SDK did not deliver the [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) event.
- [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) failed to get the group message list occasionally.


### 2.4.2 @2020.2.7

**Added**
[Message priorities](https://intl.cloud.tencent.com/document/product/1047/33526), [enumerated values](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_PRIORITY_HIGH), and [use cases](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createTextMessage) can be set for group messages.


### 2.4.1 @2020.1.14

**Changed**
- Anonymous users or visitors can only join [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups.

**Fixed**
- Some online messages cannot be pulled occasionally.
- After a system notification from an audio-video group is received, the [TIM.EVENT.MESSAGE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED) event is not delivered.
- In some scenarios, the group message recall result is inaccurate.
- Other known issues

### 2.4.0 @2020.1.3
**Added**
- The [revokeMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage) API is added.
- The `isRevoked` property is added for [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html). The property value `true` identifies recalled messages.
- The message recall event notification [TIM.EVENT.MESSAGE_REVOKED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_REVOKED) is added.
- [Force offline due to multi-client login](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT) and [force offline due to UserSig expiration](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED) are added to [TIM.EVENT.KICKED_OUT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.KICKED_OUT).

**Changed**
- The maximum size of files uploaded through [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) is increased from 20 MB to 100 MB.
- `msgMemberInfo` and `shutupTime` of [Group Prompts](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload) will be deprecated. Use `memberList` and `muteTime` instead.


**Fixed**
- Listening events could not be canceled by calling the [off](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#off) API.
- The value and type of the `isRead` property in [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) were incorrect.
- The error code and error message were incorrect when the video file in a sent video message exceeded the maximum size.
- The content of updated custom fields were incorrect occasionally.
- The [JOIN_STATUS_ALREADY_IN_GROUP](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP) event occurred occasionally when a user logged in and joined an audio-video group.
- core-js caused potential performance issues.


### 2.3.2 @2019.12.18
**Changed**
[getUserProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getUserProfile) and [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) support [custom profile fields](https://intl.cloud.tencent.com/document/product/1047/33520).

**Fixed**
Messages were lost in combined messages obtained using [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList).

### 2.3.1 @2019.12.13
**Added**
- [createImageMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createImageMessage) and [createFileMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFileMessage) support passing in [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File) objects.
- The [createFaceMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createFaceMessage) API is added.
- The message notification efficiency for [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups is optimized to improve the user experience.

**Changed**
- When messages fail to be sent, the SDK returns the actual error codes and error messages.
- When [logout](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#logout) is called, only the message channel of the current instance logs out.
- When a callback function passed in by the access side is encapsulated for security purposes and the logic of the callback function is incorrect, errors can be captured and located quickly.
- The SDK provides Chinese error information when [IM server-side error codes](https://intl.cloud.tencent.com/document/product/1047/34348) are received.

**Fixed**
- Messages were lost occasionally when the WeChat Mini Program went to foreground after staying in background for a long time.
- [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.CONVERSATION_LIST_UPDATED) was triggered several times when a message was sent.
- The SDK reported errors when files, such as images were uploaded if [registerPlugin](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#registerPlugin) was not called or incorrect parameters were entered.
- Long polling did not stop after a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group was deleted.
- When "multi-instance" or "multi-client" login was enabled, other instances or clients failed to receive messages after a web instance was logged out.
- The SDK reported errors occasionally due to the structure of session lists that were pulled.

### 2.2.1 @2019.11.28
**Changed**
The logic for getting group roaming messages is optimized.

**Fixed**
- The SDK reported the [2901 error code](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html) after the group owner of an audio-video group modified the group profile.
- After the group admin processed applications for joining a group, processed applications can be received after refresh.

### 2.2.0 @2019.11.21
**Added**
- Mini Programs support creating and sending video messages [createVideoMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createVideoMessage). Video messages can be synced across platforms. Update to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).
- The [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) API is added.
- Audio and file messages sent by Native IM v3.x are compatible.
- Location messages [GeoPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GeoPayload) can be received.

**Changed**
Up to 100 groups can be written to local storage. The SDK does not write the full group list when there are more than 100 groups.

**Fixed**
- Long polling of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups continues after logout.
- The group contact cards in message instances of [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) groups did not have values.
- Errors were reported when Internet Explorer 10 was used.
- Users could not join groups anonymously.

### 2.1.4 @2019.11.7
**Changed**
- When the `Promise` status returned by an SDK API is `rejected`, the SDK no longer delivers a [TIM.EVENT.ERROR](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.ERROR) event.
- Updates to a user's profile are immediately written to the local cache.

**Fixed**
- Code running failed after SDK integration when Angular zone.js modified prototype chains.
- After a group owner created and joined a [TIM.TYPES.GRP_AVCHATROOM](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.GRP_AVCHATROOM) group, the group owner could not receive messages.
- Initialization failed when a group list is large.

### 2.1.3 @2019.10.31

**Changed**
Combined messages (multiple message elements in one message) sent by RESTful APIs or the legacy IM are compatible. For more information, see [Compatibility Guide](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/tutorial-01-faq.html).

**Fixed**
- The unread count was inaccurate.
- Messages were disordered because read messages were not reported.
- Empty image messages were sent successfully but could not be rendered. The SDK did not support sending empty image messages.
- Empty file messages were sent with incorrect message status. The SDK did not support sending empty file messages.
- SDK code errors were reported occasionally when [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) was called.

### 2.1.2 @2019.10.25
**Added**
 [getGroupList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupList) supports pulling group profile information, including the group owner ID and group member count.

**Fixed**
- SDK code errors were reported when a RESTful API is used to send custom group notifications in an audio–video chat room.
- The SDK did not send a request to pull historical messages when a user re-joined a left group and called the getMessageList API.
- SDK code errors were reported when upload failed.

### 2.1.1 @2019.10.18
**Added**
Mini Programs support [sending audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#createAudioMessage). Audio messages can be synced across platforms. Update to the latest versions of the [TUIKit and SDK](https://intl.cloud.tencent.com/document/product/1047/33996).

**Fixed**
[getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) could still pull historical messages in a left group after rejoining.

### 2.1.0 @2019.10.16

**Added**
- Web and Mini Programs support receiving [audio messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.AudioPayload).
- Web and Mini Programs support receiving [video messages](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.VideoPayload).

**Changed**
- The [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) API can pull up to 15 messages at a time.
- [TIM.TYPES.MSG_SOUND](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_SOUND) is deprecated and replaced by [TIM.TYPES.MSG_AUDIO](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html#.MSG_AUDIO).

**Fixed**
- [getMessageList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMessageList) could not pull messages in deleted group chats.
- Group system notifications did not contain group names.
- When a conversation is created after receiving a new message, the conversion did not have profile of the message sender.

### 2.0.11 @2019.10.12

**Fixed**
Image messages failed to be sent under the React framework.

### 2.0.9 @2019.9.19

**Added**
The actual width and height of an image are detected before the image message is sent.

**Changed**
- The HTTPS protocol is used by default.
- [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) events are sent when new group system notifications are received.

**Fixed**
- Screen splash occurred when Mini Programs sent image messages.
- JPG or other images failed to be sent.
