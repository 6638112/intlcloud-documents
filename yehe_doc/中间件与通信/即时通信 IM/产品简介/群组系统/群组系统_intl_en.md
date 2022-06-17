## Group System Overview
The group system is an instant messaging system that allows multiple users to communicate in one chat. It has the following basic capabilities:
- Comprehensive [group management](https://intl.cloud.tencent.com/document/product/1047/33530) capabilities: group creation and disbanding, member management, group profile management, member profile management, and more.
- Stable and reliable messaging and a sophisticated [group message](https://intl.cloud.tencent.com/document/product/1047/33526) management mechanism: permission control, muting, message callback, message roaming, and more.
- Based on common use cases, IM provides the following default group types: **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **audio-video group (AVChatRoom)**, and **Community group (Community)**.
- Maximum number of group members:
  - The number of members in a Work, Public, or Meeting group can be increased to a maximum of 6,000 if fees are paid. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
  - A community group (Community) supports up to 100,000 members per group.
  - There is no upper limit on the number of members in an audio-video group (AVChatRoom).
- On the web or mini program end, audio-video groups allow users to receive messages as guests without logging in.

>!
>- Although audio-video groups (AVChatRoom) support unlimited group members, if a spike in group members is expected within a short time (in scenarios such as large online events where the number of members in a single group reaches 50,000 or above), contact sales representatives in advance and report service resource usage by providing the SDKAppID and the scheduled event time.
>- Currently, historical message storage is available only for non-audio-video groups, with messages stored for 7 days for billing plans of the Free Edition and Pro Edition and 30 days for the Ultimate Edition by default. If you require a longer storage period, change the storage period of historical messages in the [console](https://console.cloud.tencent.com/im). Increasing the storage period of historical messages is a value-added service. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
>- The community group (Community) feature is supported only in SDK 5.8.1668 enhanced edition or higher. To use the feature, you need to purchase the Ultimate Edition package and [apply for activation](https://intl.cloud.tencent.com/document/product/1047/37275).

IM's group system is highly customizable, allowing you to use:

- [Custom message formats](https://intl.cloud.tencent.com/document/product/1047/33527)
- [Custom group IDs](https://intl.cloud.tencent.com/document/product/1047/33529#custom-group-ids)
- [Custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#custom-fields)
- [Custom callbacks](https://intl.cloud.tencent.com/document/product/1047/33529#custom-callbacks)

## Group Member Roles

The following table lists various group member roles and their permissions:

| Group Member Role | Description       | Management Permission         |
| ------------ | -------------- | ------------ |
| Ordinary member     |  An ordinary member has no management permissions.      |   In a work group (Work), an ordinary member has the permission to modify the group profile.    |
| Group admin       | A group admin is specified by the group owner to assist in managing group members and holds certain management permissions. |<ul style="margin:0;"><li>Modify the group profile</li><li>Remove an ordinary member from the group</li><li>Mute an ordinary member, that is, prevent the ordinary member from speaking for a certain period of time</li><li>Approve or reject a group joining request</li></ul>Work groups do not support specifying group admins by default. |
| Group owner         | A group owner is the creator of a group and has the highest level of management permissions in the group.    | The group owner has the following permissions in addition to all permissions held by an admin: <ul style="margin:0;"><li>Appoint or cancel an admin</li><li>Remove an admin from the group</li><li>Mute an admin</li><li>Disband the group</li><li>Transfer the group ownership</li></ul> |
| App admin | This special role has the permission to manage all groups in the app and has higer permission than the group owner. | The app admin can manage any group as the group owner does, whether the app admin joins the group or not. |

[](id:GroupType)
## Group Types

Based on common use cases, IM provides the following default group types:

| Group Type | Applicable Scenario |
|--------|---------|
| Work group (Work) | A work group is like a WeChat group. After a work group is created, users can join the group only after being invited by group members. The invitation does not need to be accepted by the invitee or approved by the group owner. This group type is the same as private group (Private) in earlier versions. |
| Public group (Public) | A public group is like a QQ group. After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group. |
| Meeting group (Meeting) | A meeting group allows users to join and leave freely and view historical messages sent before they join the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio/video conferencing and online education. This group type is the same as chat room (ChatRoom) in earlier versions. |
| Audio-video group (AVChatRoom) | An audio-video group allows users to join and leave freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios. |
| Community group (Community) | A community group allows users to join and leave freely, supports up to 100,000 members, and stores message history. To join the group, a user needs to search for the group ID and send a request, and the request does not need to be approved by an admin before the user can join the group. |


### Differences in basic group capabilities

| Item | Work Group | Public Group | Meeting Group | Audio-Video Group | Community Group |
|--- |-- |-- |-- |-- |-- |
| Available member roles | Group owner<br>Ordinary member<br>App admin | Group owner<br>Admin<br>Ordinary member<br>App admin | Group owner<br>Admin<br>Ordinary member<br>App admin | Group owner | Group owner<br>Admin<br>Ordinary member<br>App admin |
| Who can modify the group profile | Ordinary member | Group admin<br>Group owner<br>App admin | Group owner<br>App admin | App admin | Group owner<br>App admin |
| Number of group members whose information can be obtained | All group members | All group members | All group members | None (no group member information stored) | All group members |
| Who can disband a group | App admin | Group owner and app admin | Group owner and app admin | Group owner and app admin | Group owner and app admin |

>?
>- Group types are upgraded in the new SDK version and they are **work group (Work)**, **public group (Public)**, **meeting group (Meeting)**, **audio-video group (AVChatRoom)**, and **Community group (Community)**. Private group (Private) and chat room (ChatRoom) in earlier versions (which have Public, Private, ChatRoom, and AVChatRoom groups) correspond to work group (Work) and meeting group (Meeting) in the new version respectively.
>- Ordinary members of a work group (Work) can modify only the group name, introduction, announcement, and group profile photo URL, but not other group profile information.
>- If the roles of a group type cannot meet your business needs, you can add roles by setting member-level [custom fields](https://intl.cloud.tencent.com/document/product/1047/33529#custom-fields).
>- It is necessary to obtain the information about some members in scenarios where an audio-video group displays a list of some of its members.

### Differences in joining a group

| Item | Work Group | Public Group | Meeting Group | Audio-Video Group | Community Group |
|--- |-- |-- |-- |-- |-- |
| Perform an exact search for a group ID to join a group | Not supported | Supported | Supported | Supported | Supported |
| Perform a fuzzy search for group information to join a group | Not supported | Not supported | Not supported | Not supported | Not supported |
| Request to join a group | Not supported | Supported. Approval from the group owner or admin is needed. | Supported. No approval is needed. | Supported. No approval is needed. | Supported. No approval is needed. |
| Join a group after receiving an invitation from a group member | Supported | Not supported | Not supported | Not supported | Supported |

>?
>- Exact search is to search for a group by group ID. Fuzzy search is to search for a group by fields such as the group name.
>- Approval for joining a group: the group owner and admin can approve or reject requests made by non-members to join the group. Only approved users can join the group.
>- For a group type that does not support the invitation of non-members to a group, group members can share the group ID with non-members in the app so that the non-members can join the group.

### Differences in member management capabilities

| Item | Work Group | Public Group | Meeting Group | Audio-Video Group | Community Group |
|--- |--- |--- |--- |--- |--- |
| Setting admins | Not supported | Supported | Supported | Not supported | Supported |
| A group owner leaves the group | Supported. After the group owner leaves, the group has no group owner. | Not supported | Not supported | Not supported | Not supported |
| Remove a group member | Supported. The group owner can remove group members. | Supported. The group owner and admin can remove group members, but the admin can remove only ordinary group members. | Supported. The group owner and admin can remove group members, but the admin can remove only ordinary group members. | Not supported. The muting feature can be used to achieve a similar effect. | Supported. The group owner and admin can remove group members, but the admin can remove only ordinary group members. |
| Mute a group member | Not supported | Supported. The group owner and admin can mute group members, but the admin can mute only ordinary group members. | Supported. The group owner and admin can mute group members, but the admin can mute only ordinary group members. | Supported. The group owner can mute group members. | Supported. The group owner and admin can mute group members, but the admin can mute only ordinary group members. |
| Periodically remove offline group members | Supported, but disabled by default | Supported, but disabled by default | Supported, but disabled by default | Not supported | Not supported |

>!Muted group members cannot send group chat messages within the muting period.


### Differences in group limits
| Item | Work Group/Public Group/Meeting Group | Audio-Video Group | Community Group |
|--- |--- |--- |--- |
| Maximum number of members | <ul style="margin:0;"><li>Free Edition: 20 per group</li><li>Pro Edition: 200 members/group by default, which can be extended to 2,000 members/group through a [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#zz)</li><li>Ultimate Edition: 2,000 members/group by default, which can be extended to 6,000 members/group through a [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#zz).</li></ul> | Unlimited | <li>Free Edition: not supported</li><li>Pro Edition: not supported</li><li>Ultimate Edition: 100,000 members/group by default</li>|
| Maximum number of groups | <ul style="margin:0;"><li>Free Edition: up to 100 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition or Ultimate Edition: unlimited</li></ul> | <ul style="margin:0;"><li>Free Edition: up to 10 existing groups, and disbanded groups do not count against the quota</li><li>Pro Edition: up to 50 existing groups, and disbanded groups do not count against the quota. You can upgrade to an unlimited number of audio-video groups by purchasing the [value-added service](https://intl.cloud.tencent.com/document/product/1047/34350#zz).</li><li>Ultimate Edition: unlimited</li></ul> | <li>Free Edition: not supported</li><li>Pro Edition: not supported</li><li>Ultimate Edition: 100,000 groups can be created by default </li>|

>!
>- In the Pro Edition or Ultimate Edition SDKAppID, the maximum net increase in group count per day (the number of created groups minus the number of disbanded groups) is 10,000 for all group types.
>- In the Pro Edition or Ultimate Edition SDKAppID, the free peak group count is 100,000 per month, and [excessive part will be billed](https://intl.cloud.tencent.com/document/product/1047/34350#jc). We recommend that you disband the groups that are no longer needed.


### Differences in message capabilities

| Item | Work Group | Public Group | Meeting Group | Audio-Video Group | Community Group |
|--- |--- |--- |--- |--- |--- |
| Unread message count | Supported | Supported | Not supported | Not supported | Supported |
| Group members can view messages sent before they join the group | Not supported | Not supported | Supported | Not supported | Supported |
| Historical message storage | Supported | Supported | Supported | Not supported | Supported |
| Member change notifications | Supported | Supported | Not supported | Supported | Supported |
| A message must be sent to activate a new group | Required | Not required | Not required | Not required | Not required |
| Default message receiving option | Receive online and offline push messages | Receive online and offline push messages | Receive only online push messages | Receive only online push messages | Receive online and offline push messages |
| Users can receive group messages as guests without logging in | No | No | No | Yes | No |

>!
>- For a group that requires activation, before the group owner sends a message, the group is inactive and invisible to all group members except the group owner. A group that does not require activation is visible to all group members once it is created.
>- Currently, offline push is available only on Android (Android offline push) and iOS (APNs push) platforms.
>- The work group, public group, meeting group, and community group have the historical message storage capability, which allows historical messages to be stored for 7 days (30 days for the Ultimate Edition) free of charge by default. If you need a longer storage period, change the storage period of historical messages in the [console](https://console.cloud.tencent.com/im). Increasing the storage period of historical messages is a value-added service. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


### Differences in batch import and automatic repossession

| Item | Work Group/Public Group/Meeting Group/Community Group | Audio-Video Group |
|--- |--- |--- |
| Importing groups, group members, and group messages is allowed | Supported. It is allowed when historical groups are migrated from a third-party platform to IM. | Not supported. Only existing groups, group members, and group messages can be used. |
| Time before a group is automatically repossessed (in seconds) | The backend does not repossess groups, unless the group owner disbands the group or all members leave the group. (About group disbanding: the backend does not proactively disband a group unless the group owner disbands the group, or the group is automatically repossessed. If automatic repossession is configured for a group, the backend irregularly traverses the group and disbands it if no one sends a message in the group for n seconds or the group profile is modified.) | The backend does not repossess groups, unless the group owner disbands the group, or all members leave the group. |

>!To enable group repossession, submit a ticket based on [ticket templates](https://intl.cloud.tencent.com/document/product/1047/37275#.E8.87.AA.E5.8A.A8.E5.9B.9E.E6.94.B6.E7.BE.A4.E7.BB.84). After configuration, inactive groups will be removed. An inactive group is one in which no message has been sent and no member change has occurred.

## Group Data Structure
### Group basic information[](id:GroupBaseInfoFilter)

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| GroupId | String | Unique identifier of the group | Read-only.<br>Each group ID must be unique in the app. The prefix is @TGS#, and custom group IDs can also be used in the app. |
|Type | String | Group type | Read-only.<br>The following group types are supported by default: work group, public group, meeting group, audio-video group, and community group. For more information, see [Group Types](#GroupType).<br>In the SDK of an earlier version, group types also include the private group, ChatRoom, and BChatRoom, which are not recommended. |
| Name | String | Name of the group | Readable and writable. The maximum length is 30 bytes and cannot be adjusted. |
| Introduction | String | Introduction of the group | Readable and writable. The maximum length is 240 bytes and cannot be adjusted. |
| Notification | String | Group announcement | Readable and writable. The maximum length is 300 bytes and cannot be adjusted. |
| FaceUrl | String | URL of the group's profile photo | Readable and writable. The maximum length is 100 bytes and cannot be adjusted. |
| Owner_Account | String | ID of the group owner | Read-only. |
| CreateTime | Integer | Creation time of the group | Read-only. |
| InfoSeq | Integer | This value increases every time the group information changes. | Read-only. |
| LastInfoTime | Integer | Time of the last change to group information | Read-only. |
| LastMsgTime | Integer | Time of the last message in the group chat | Read-only. |
| NextMsgSeq | Integer | Sequence number of the next message in the group chat | Read-only.<br>Every message in the group chat has a unique sequence number. Sequence numbers are consecutive numbers based on the sequence of sent messages. With every message sent in the group chat, `NextMsgSeq` (starting from 1) increases by 1. |
| MemberNum | Integer | Number of current members | Read-only. |
| MaxMemberNum | Integer | Maximum number of members | Default value: the upper limit of the paid plan; for example, it is 20 on Free Edition. If you upgrade the plan, you need to modify this field to the corresponding value according to the basic information of the modified group|
| ApplyJoinOption | String | Group joining option | The following options are available:<ul style="margin:0;"><li>DisableApply: Disallow any request.</li><li>NeedPermission: Require group owner or admin's approval </li><li>FreeAccess: users can join the group freely without prior approval.</li></ul> |


>!The permissions to modify the group name, introduction, announcement, and profile photo URL are described as follows:
>- In a work group, any member can modify them.
>- For other group types, only **non-ordinary members** can modify them.

### Group member profile[](id:SelfInfoFilter)

| Field Name | Type | Description | Notes |
|--- |--- |--- |--- |
| Member_Account | String | Group member ID | Read-only. |
| Role | String | Role in the group | A group has the following roles: Owner (group owner), Admin (group admin), and Member (group member). |
| JoinTime | Integer | Time of joining the group | Read-only. |
| MsgSeq | Integer | Sequence number of the current read message of the member | Read-only. |
| MsgFlag | String | Message receiving option | The following options are available:<ul style="margin:0;"><li>AcceptAndNotify: Receive and notify.</li><li>AcceptNotNotify: Receive without notifying (remote APNs push is not triggered)</li><li>Discard: Block group messages (messages are not pushed to clients)</li></ul>|
| LastSendMsgTime | Integer | Time of sending the last message | Supported by work groups, public groups, and meeting groups, but not audio-video groups. |
| NameCard | String | Group name card | Readable and writable. |

## Custom Group IDs

When a group is created in the app, IM assigns a default group ID to the new group by default. This default group ID starts with @TGS# and is unique in the app.
IM also allows you to customize group IDs that are simple and easy to remember and communicate. A custom group ID must be a string of ASCII characters (0x20-0x7e) with a length less than 48 bytes. Do not use @TGS# as the prefix to avoid confusion with assigned group IDs.
>!The prefix of the IDs of community groups (Community) must be @TGS#_.
## Custom Fields

IM allows you to configure up to 10 group-level custom fields and 5 member-level custom fields based on your business needs. With custom fields, apps can attach additional data to groups, and the data can be read and written through existing APIs. **Custom fields cannot be deleted once created and applied.**

### Description

Custom fields have the following characteristics:

- Their values are in key-value format.
- Key is a string with a length less than 16 bytes. Its name can contain only uppercase and lowercase letters, numbers, and underscores (_).
- Value is a buffer customized by the user, which can be binary data. Group-level values have a maximum length of 512 bytes, while member-level values have a maximum length of 64 bytes.
- You can configure the least read permission and the least write permission for each key.

The read and write permissions of a custom field are listed as follows, from high to low:

1. Readable and writable by the app admin.
2. Readable and writable by the group owner.
3. Readable and writable by the group admin.
4. Readable and writable by group members.
5. Readable and writable by anyone, including non-members.

For example, an app needs to extend the `GroupLevel` field for groups and the value of this field is a number representing the level of a group. If this level information is calculated by the app backend, then the least write permission should be **writable by the app admin**. If the field is part of the public profile of the group, its least read permission should be **readable by anyone, including non-members**.

If the value to be stored is a number, we recommend that C and C++ developers store it as a string instead of binary data. For example, when the number to be stored is 1, store it as string `1` instead of binary data `0x01`. In the future, IM will offer more operations for custom fields, such as specific mathematical operations on values, which will be performed on the basis of string-type numbers.

### Configuration method

Custom fields at these two levels can be configured in the IM console.
To configure member-level custom fields, you need to specify the group type first. Audio-video group and custom group types that are configured based on it do not support custom fields at the group member level, because these types of groups do not store member profiles.
The **self read and write permissions** indicate whether members can read and write their own member-level custom fields. For example, a member-level customer field named `MemberLevel` represents the level of a member in a group. Group members can read but not modify their own levels, and therefore their **self read and write permissions** are set to **read-only** for this field.

## Custom Callbacks

Third-party callback is an important method to meet the special requirements of apps. It provides users with the capability to customize actions.
IM's group system supports different callbacks. For more information, see [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354) and [Callback Command List](https://intl.cloud.tencent.com/document/product/1047/34355).
