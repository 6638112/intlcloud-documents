>!**Do not use APIs of new and old versions at the same time**.

## Initialization and Login APIs
To use Tencent Cloud IM services, you need to perform initialization and log in.

| API | Description |
|---------|---------|
| [initSDK](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ac905c315726b517ba62421471bbecf56) | Initializes the SDK. |
| [unInitSDK](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd) | Uninitializes the SDK. |
| [login](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416) | Logs in. |
| [logout](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48) | Logs out. |
| [getLoginStatus](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a1836146275265b2a120412f18961db95) | Gets the login status. |
| [getLoginUser](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad4b2e5a7df5e786ba369054ac582007f) | Gets the UserID of the current login user. |

## Simple Message APIs
Use the following message APIs if you only need to use text and signaling (a piece of custom buffer) messages.

| API | Description |
|---------|---------|
| [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) | Sets an event listener for simple messages (text messages and custom messages). <br>Do not use it and [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) at the same time. |
| [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) | Removes the event listener for simple messages (text messages and custom messages). |
| [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981) | Sends a one-to-one (C2C) text message. |
| [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f) | Sends a one-to-one (C2C) custom (signaling) message. |
| [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52) | Sends a group text message. |
| [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2) | Sends a group custom (signaling) message. |

## Signaling APIs
| API | Description |
|---------|---------|
| [addSignalingListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a862073ac16de7f02e5f97b8cbe7eb028) | Adds a signaling listener. |
| [removeSignalingListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a72f6c032de1b0dbaabb227be54d0bcfc) | Removes a signaling listener. |
| [invite](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a61e283c64f1a303b0a9f0e13a48de0a9) | Invites a user. |
| [inviteInGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ad51059e9f430650da09bcae01f0bb3b8) | Invites certain users in the group. |
| [cancel](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a9d69707620f038d6e47356cdaa3ab9bd) | The inviter cancels the invitation. |
| [accept](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a4cd3629a0952db7c59186e0c222e17a0) | The invitee accepts the invitation. |
| [reject](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ad9510bf8a333189fd1a0c1eafbde2266) | The invitee rejects the invitation. |
| [getSignalingInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ab303f20f53de134e6f6ebe5f9f9bcad0) | Gets the signaling information. |
| [addInvitedSignaling](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ac50301e05e1672b771dc2c92fadff8de) | Adds invitation signaling (can be used for invitation signaling triggered by group offline push messages). |

## Advanced Message APIs
If you need to send/receive rich media messages (images, videos, files, etc.) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple messages APIs and advanced message APIs at the same time.

| API | Description |
|---------|---------|
| [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) | Sets an event listener for advanced messages. <br>Do not use it and [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) at the same time. |
| [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) | Removes the event listener for advanced messages. |
| [createTextMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a3ea254cd12aa0bcfd004f26f759b76a0) | Creates a text message. |
| [createCustomMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) | Creates a custom message. |
| [createImageMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1) | Creates an image message. |
| [createSoundMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7e661ce2b4eba1535bd04f3b6539b9dc) | Creates a voice message. |
| [createVideoMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ada17dbc78e9876a8f3a9fd24a73752b5) | Creates a video message. |
| [createFileMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a39e4b6609321fd188a2e156a00bb3135) | Creates a file message. |
| [createLocationMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a67cebe27192392080fc80a86c80a4321) | Creates a location message. |
| [createFaceMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7ad0f3b7eff3978c12d8c912ca164a5d) | Creates an emoji message. |
| [createMergerMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#acebe275789ab49cc8abe6af5e07aa3b0) | Creates a combined forward message. |
| [createForwardMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af8f609bfbfe99a0c65611b14159b6b4d) | Creates a single forward message. |
| [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) | Sends a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [revokeMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) | Recalls a message. The message object can be created by the `createXXXMessage` API, where `XXX` is a variable. |
| [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df) | Gets the one-to-one (C2C) message history. |
| [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) | Gets the group message history. |
| [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b) | Marks one-to-one (C2C) messages as read. |
| [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69) | Marks group messages as read. |
| [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534) | Deletes a message from the local storage. |
| [insertGroupMessageToLocalStorage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a04a3f6c250f9d6c0053fd71be74f047f) | Adds a message to the group message list. |


## Group APIs
Tencent Cloud IM SDK supports four preset group types, each of which pertains to different scenarios.
- Work group (Work): similar to a regular WeChat group. Users can only join the group by being invited by existing group members.
- Public group (Public): similar to a QQ group. Users can join the group through requests, which need to be approved by the group owner or group admin.
- Meeting group (Meeting): when used with [TRTC](https://intl.cloud.tencent.com/product/trtc), ideal for scenarios such as video conferencing and online education. Users can join and exit the group freely and view the existing message history before they join the group.
- Audio-video group (AVChatRoom): suitable for scenarios such as live streaming and chat rooms with on-screen comments. Users can join and exit the group freely. There is no limit on the number of group members.

| API | Description |
|---------|---------|
| [setGroupListener](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a092fc428f35eb18c41a80b3655948d40) | Sets an event listener for groups. |
| [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) | Creates a (simple) group. |
| [createGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) | Creates an (advanced) group. The group information and the initial group members can be set during group creation. |
| [joinGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) | Joins a group. |
| [quitGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) | Quits a group. |
| [dismissGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) | Deletes a group. Only the group owner and group admin can delete the group. |
| [getJoinedGroupList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a05bfd8f7df6bfba718abc96fdad49791) | Gets the list of groups the current user has joined, excluding audio-video groups. |
| [getGroupsInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) | Pulls the profiles of groups. |
| [setGroupInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad87ce42b4dc4d97334fe857e4caa36c4) | Modifies the profile of a group. |
| [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6bf8f3eafb5ffcb1d13bd69231de8bd4) | Sets the group message receiving option. |
| [getGroupMemberList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) | Gets the group member list. |
| [getGroupMembersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) | Gets the profiles of specified group members. |
| [setGroupMemberInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) | Modifies the profile of a specified group member. |
| [muteGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) | Mutes a group member. |
| [kickGroupMember](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333) | Removes a member from a group. |
| [setGroupMemberRole](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) | Sets the role for a group member. |
| [transferGroupOwner](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) | Transfers the ownership of a group. |
| [inviteUserToGroup](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) | Invites users to a group. |
| [getGroupApplicationList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) | Gets the list of requests to join a group. |
| [acceptGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) | Accepts a request to join a group. |
| [refuseGroupApplication](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd) | Rejects a request to join a group. |
| [setGroupApplicationRead](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a498d9d76217cbae0aa235ac928ad02d8) | Marks the request list as read. |

## Conversation List APIs
The conversation list is the list a user sees on the first screen after logging in to WeChat or QQ. It includes elements such as conversation node, conversation name, group name, last message, and unread count.

| API | Description |
|---------|---------|
| [setConversationListener](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a39228ebb1c5d6855643aa8c1efcc429c) | Sets a conversation listener. |
| [getConversationList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) | Gets the conversation list. |
| [deleteConversation](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) | Deletes a conversation. |
| [setConversationDraft](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab) | Sets a draft for a conversation. |

## User Profile APIs
APIs for querying user profiles, modifying one's own user profile, and blocking messages from a specified user (or adding a specified user to the blocklist).

| API | Description |
|---------|---------|
| [getUsersInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) | Gets user profiles. |
| [setSelfInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) | Modifies one's own user profile. |
| [addToBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456) | Blocks the messages from a specified user, which means adding the user to the blocklist. |
| [deleteFromBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa) | Unblocks the messages from a specified user, which means removing the user from the blocklist. |
| [getBlackList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6) | Gets the blocklist. |

## Offline Push APIs
Use the offline push service if you want your app to receive IM messages in real time when it is in the background. As there is currently no unified push service in the Chinese mainland, to implement Android offline push, the mobile phones of different vendors need to be [specifically adapted](https://intl.cloud.tencent.com/document/product/1047/39156).

| API | Description |
|---------|---------|
| [setOfflinePushConfig](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) | Sets the offline push configuration. |

## Friend Management APIs
By default, Tencent Cloud IM does not check your relationship with a user when receiving and sending messages. You can enable the "Check Relationship for One-to-One Messages" on **Feature Configuration** > **Login and Message** > **Relationship Check** in the [IM console](https://console.cloud.tencent.com/im) and use the following APIs to delete/add friends and manage your friend list.

| API | Description |
|---------|---------|
| [setFriendListener](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a17e92c5ca9abad7afe25b654f1fcd75c) | Sets a relationship chain listener to receive friend list and blocklist change events. |
| [getFriendList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) | Gets the friend list. |
| [getFriendsInfo](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a88732b0f7a5e77a9dd34403fe7bbdd21) | Gets the profiles of specified friends. |
| [setFriendInfo](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe) | Sets the profile of a specified friend. |
| [addFriend](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) | Adds a friend. |
| [deleteFromFriendList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61) | Deletes a friend. |
| [checkFriend](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#accac9a69c8e4332b0b83755ec54ecfed) | Checks your relationship with a specified user. |
| [getFriendApplicationList](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a2dbf4da19f3b9b170089b8e8cb210166) | Gets the list of friend requests. |
| [acceptFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa) | Accepts a friend request. |
| [refuseFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89) | Rejects a friend request. |
| [deleteFriendApplication](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5c869e3358ca74f9cd2eaebfc7298490) | Deletes a friend request. |
| [setFriendApplicationRead](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a022b4817a31dd25707f14b8184c42675) | Sets a friend request as read. |
| [createFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) | Creates a friend list. |
| [getFriendGroups](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) | Gets the information of friend lists. |
| [deleteFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) | Deletes friend lists. |
| [renameFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) | Modifies the name of a friend list. |
| [addFriendsToFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) | Adds friends to a friend list. |
| [deleteFriendsFromFriendGroup](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) | Deletes friends from a friend list. |


