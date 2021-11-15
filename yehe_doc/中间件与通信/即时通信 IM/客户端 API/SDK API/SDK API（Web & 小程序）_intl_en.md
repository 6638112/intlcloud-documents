
## TIM

TIM is the namespace of the IM Web SDK and provides the static method [create()](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) for creating SDK instances, the event constant [EVENT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html), and the type constant [TYPES](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html).

**Initialization**

| API     | Description |
| --- | --- |
| [create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) | Creates an SDK instance. |

## SDK Instance

| Term| Description |
| :--- | :---- |
| Message | [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) indicates the content to be sent and carries multiple attributes which specify whether you are the sender, the sender account, the message generation time, and so on. |
| Conversation | Two types of [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) are available: <li>Client to Client (C2C): a one-to-one chat, involving only 2 participants.</li><li>GROUP: a group chat, involving more than 2 participants. |
| Profile | [Profile](https://web.sdk.qcloud.com/im/doc/en/Profile.html) describes the basic information of a user, including the nickname, gender, personal signature, and profile photo address. |
| Friend | [Friend](https://web.sdk.qcloud.com/im/doc/en/Friend.html) describes the basic information of a friend, including the remarks and friend list. |
| FriendApplication | [FriendApplication](https://web.sdk.qcloud.com/im/doc/en/FriendApplication.html) describes the basic information of a friend request, including the friend source and remarks. |
| FriendGroup | [FriendGroup](https://web.sdk.qcloud.com/im/doc/en/FriendGroup.html) describes the basic information of a friend list, including the friend list name and members.
| Group | [Group](https://web.sdk.qcloud.com/im/doc/en/Group.html) indicates a communication system for group chatting, including Work, Public, Meeting, and AVChatRoom. |
| GroupMember (group member) | [GroupMember](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html) indicates the basic information of each group member, such as the ID, nickname, role, and the time of joining the group. |
| Group notification | A group notification is generated when an event such as adding or deleting group member occurs. The access side can configure whether to display group notifications to group members. <br/>For more information about group notification types, see [Message.GroupTipPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload).|
| Group system message | For example, when a user requests to join a group, the group admin receives a system message. After the admin accepts or rejects the request, the IM SDK returns the result to the access side, which then displays the result to the user. <br/>For more information about group system message types, see [Message.GroupSystemNoticePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload). |
| Message display on screen | The sent messages, including text segments and images, are displayed on the computer or phone screen. |

### Login
| API     | Description |
| --- | --- |
| [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) | Logs in. |
| [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) | Logs out. |


### Message
| API     | Description |
| --- | --- |
| [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) | Creates a text message. |
| [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextAtMessage) | Creates a text message with the @ notification feature. |
| [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) | Creates an image message. |
| [createAudioMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage) | Creates a voice message. |
| [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) | Creates a video message. |
| [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) | Creates a custom message. |
| [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) | Creates an emoji message. |
| [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) | Creates a file message. |
| [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) | Creates a combined message. |
| [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage) | Downloads a combined message. |
| [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) | Creates a forward message. |
| [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) | Sends a message. |
| [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) | Recalls a message. |
| [resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage) | Sends a message again. |
| [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) | Deletes a message. |

### Conversation
| API     | Description |
| --- | --- |
| [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) | Gets the message list.  |
| [setMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRead) | Sets a message as read.  |
| [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) | Gets the conversation list. |
| [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile) | Gets the conversation information. |
| [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) | Deletes a conversation. |
| [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation) | Pins/Unpins a conversation to/from top. |

### Profile
| API     | Description |
| --- | --- |
| [getMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMyProfile) | Gets your personal profile. |
| [getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) | Gets other user’s profile. |
| [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) | Updates your personal profile. |
| [getBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getBlacklist) | Gets your blocklist. |
| [addToBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToBlacklist) | Adds a user to the blocklist. |
| [removeFromBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromBlacklist) | Removes a user from the blocklist. |

### Relationship Chain
| API     | Description |
| --- | --- |
| [getFriendList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendList) | Gets the friend list in the SDK cache. |
| [addFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addFriend) | Adds friends. |
| [deleteFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriend) | Deletes friends. |
| [checkFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#checkFriend) | Verifies friends. |
| [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) | Gets the friend data and profile data of a specified user. |
| [updateFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateFriend) | Updates the relationship chain data of friends.  |
| [getFriendApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendApplicationList) | Gets the friend request list in the SDK cache. |
| [acceptFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#acceptFriendApplication) | Accepts a friend request. |
| [refuseFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#refuseFriendApplication) | Rejects a friend request. |
| [deleteFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendApplication) | Deletes a friend request. |
| [setFriendApplicationRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setFriendApplicationRead) | Set a friend request as reads. |
| [getFriendGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendGroupList) | Gets friend lists in the SDK cache.  |
| [createFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFriendGroup) | Creates a friend list. |
| [deleteFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendGroup) | Deletes a friend list. |
| [addToFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToFriendGroup) | Adds friends to a friend list. |
| [removeFromFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromFriendGroup) | Removes friends from a friend list. |
| [renameFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameFriendGroup) | Modifies the name of a friend list. |

### Group
| API     | Description |
| --- | --- |
| [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) | Gets the group list. |
| [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile) | Gets the group profile. |
| [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) | Creates a group. |
| [dismissGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#dismissGroup) | Deletes a group. |
| [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) | Modifies the group profile. |
| [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) | Requests to join a group. |
| [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup) | Quits a group. |
| [searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID) | Searches for a group. |
| [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount) | Gets the number of online users in an audio-video group. |
| [changeGroupOwner](https://web.sdk.qcloud.com/im/doc/en/SDK.html#changeGroupOwner) | Transfers the group ownership. |
| [handleGroupApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#handleGroupApplication) | Processes requests to join the group. |
| [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) | Initializes group attributes.  |
| [setGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupAttributes) | Sets group attributes. |
| [deleteGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupAttributes) | Deletes group attributes. |
| [getGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupAttributes) | Gets group attributes. |

### Group member
| API     | Description |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) | Gets the group member list. |
| [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) | Gets a group member’s profile. |
| [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember) | Adds a group member. |
| [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember) | Deletes a group member. |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberMuteTime) |Configures the muting period.|
| [setGroupMemberRole](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberRole) | Modifies the group member’s role. |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) | Sets the name card for a group member. |
| [setGroupMemberCustomField](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberCustomField) | Sets a custom field for a group member. |
| [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) | Specifies the notification type of group messages. |

### Others
| API     | Description |
| --- | --- |
| [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) | Enables event listening. |
| [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) | Disables event listening. |
| [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin) | Registers a plugin. |
| [setLogLevel](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel) | Sets the log level. |
| [destroy](https://web.sdk.qcloud.com/im/doc/en/SDK.html#destroy)  | Terminates an SDK instance. |


