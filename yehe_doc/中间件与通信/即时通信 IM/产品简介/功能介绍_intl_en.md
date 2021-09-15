### Supported platforms

The following platforms can communicate with each other and provide services across devices and platforms.

| Platform | SDK and Compatibility | Demo | Source Code | UI Component |
| ------- | --------------| -------- | -------- | -------- |
| Android | Compatible with JDK 1.6 and Android SDK version 14 and later | Supported | Supported | Supported |
| iOS | Compatible with iOS 8.0 and later | Supported | Supported | Supported |
| Mac | Compatible with OS X 10.10 and later | Supported | Supported | - |
| Windows | C and C++ are included. Compatible with Windows 7, Windows 8 and 8.1, and Windows 10. Both 32-bit and 64-bit programs can be connected. | - | - | - |
| Web | Supports Internet Explorer 11+, Chrome 7+, Firefox 3.6+, Opera 12+ and Safari 6+ | Supported | - | - |
| Mini Program | Supported | Supported | - | - |
| Unity | Supports 2020.2.7f1c1 or later | Supported | Supported | - |
| Flutter |Supports Flutter 2.0.12 | Supported | Supported | - |


### Global access

| Feature Type | Description |
| -------------- | -------------- |
| Global access overview | IM provides highly reliable and secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling across the entire network. When terminals log in from outside the Chinese mainland, IM SDK connects to the nearest access nodes or cache nodes. |
| China | South China, North China, East China, Hong Kong, Taiwan, etc. |
| Global | Asia: Japan, South Korea, Singapore, India, Thailand, Malaysia, Vietnam, Philippines, UAE, Indonesia<br>Europe: Germany, United Kingdom, France, Russia, Italy, Norway, Spain, Netherlands<br>North America: United States, Canada, Mexico<br>South America: Brazil<br><br>Oceania: Australia<br>Africa: South Africa, Nigeria, etc. |


### Account features

| Feature Type | Description |
| ------------ | -------------------------------------- |
| Import accounts | Import accounts in batches |
| Deactivate accounts | Invalidate UserSig |
| Delete accounts | Delete accounts in batches |
| User online status | Manage the online and offline statuses after users log in |
| Query accounts | Check whether accounts are imported |

### Multi-client login

| Feature Type | Description |
| --------- | --------------------------------------------------------- |
| Single-platform     | A user can be online on only one of the Android, iPhone, iPad, Windows, Mac, and web platforms at one time.              |
| Dual-platform (default) | A user can be concurrently online on the Android, iPhone, iPad, Windows, or Mac platform and the web platform.            |
| Triple-platform     | A user can be concurrently online on the Android, iPhone, or iPad platform, the Windows or Mac platform, and the web platform. |
| Multi-platform     | A user can be concurrently online on the Android, iPhone, iPad, Windows, Mac, and web platforms.              |

>? You can configure multi-device login by logging in to the [IM console](https://console.cloud.tencent.com/im) and clicking **App Configuration** for the target app to open the **Feature Configuration** page.

### Message types

| Feature Type | Description |
| ------------ | ----------------- |
| Text | The message content is plain text. |
| Image | The message content includes the URL, dimensions, and size of the image. |
| Emoji | Emoji messages are customized by developers. |
| Audio | Audio data must include the duration in seconds. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| File | The message content includes the URL, size, and format of the file. There are no file format restrictions, and the maximum supported file size is 100 MB. |
| Short video | The message content includes the URL, duration, size, and format of the video file. The maximum supported file size is 100 MB. |
| Custom | Message types that are customized by developers, such as red packet and rock-paper-scissor. |
| System notification | This type of messages include built-in system notification messages and system notification messages customized by developers. |
| Group tips | System messages pushed when a member joins or leaves a group, group description is modified, group member profile changes, etc. |
| Combined messages | Up to 300 messages can be combined. |



### Message features

| Feature Type | Description |
| -------- | -------- |
| Download messages | The app admin can obtain all one-to-one or group messages for a specified hour of a specified day in the past 7 days through this API. |
| Offline messages | IM supports offline push when a user logs in, the app switches to work in the background, and other users send messages. |
| Roaming messages | When a user logs in on a new device, the historical message storage recorded (on the cloud) by the server is synchronized to the new device. Roaming messages are stored for 7 days by default. You can pay to increase the roaming message storage period. |
| Multi-device synchronization | Messages are synchronized and received across multiple devices. |
| Historical messages | Both local and cloud historical messages are supported. |
| Recall messages | Recall a message that has been delivered successfully. By default, messages that were delivered more than 2 minutes ago cannot be recalled. Only one-to-one and group chat messages can be recalled. Messages sent in audio-video chat rooms (AVChatRooms) cannot be recalled. |
| Read receipts | Users can check if messages have been read in a one-to-one chat. |
| Forward messages | Users can forward messages to other users or groups. |
| @ feature | There is no essential difference between an in-group @ message and an ordinary message, although the user specified by @ will see a special UI effect. |
| Typing status indicator | This feature can be implemented in online messaging scenarios. |
| Offline push | Apple APNs, Xiaomi push, Huawei push, Meizu push, OPPO push, vivo push, and Google FCM push are supported. |
| Delete messages | Use the remove method for messages to delete messages locally. |
| Red packets | Red packet messages are similar to @ messages and can be implemented through TIMCustomElem. |
| Push to all users | A set of RESTful APIs based on the IM communication architecture to enable push to all users, push by tag, and push by attribute in an app. You can integrate the client with the SDK for capabilities such as online push, offline push (Android background notification and APNs), and message receiving. |
| Local message search | Support search for friends, search for groups/group members, search for messages, and grouping by conversation. |


### Profile features

| Feature Type | Description |
| ------------------ | ---------------- |
| Set user profiles | Users can set information including the nickname, verification method, profile photo, gender, age, signature, and location. |
| Obtain user profiles | Users can view their own profiles and the profiles of friends and strangers. |
| Obtain user information by fields | This feature can obtain user information based on specific fields. |
| Custom user information | Up to 20 custom user profile fields are supported. |



### Relationship chain features

| Feature Type | Description |
| -------------------- | ---------------------- |
| Search for friends | Search for a friend by account ID. |
| Apply for friend requests | Specify whether a request reason is required. The default is no. |
| Add friends | Send friend requests. |
| Import friends |Support importing multiple one-way friends at a time. |
| Update friends | Support updating the relationship chain data of multiple friends of a user at a time. |
| Delete friends | Friends can be deleted after they are added to the contact list. |
| Obtain all friends | This feature can obtain all friends. Only basic information of friends is pulled by default. |
| Accept/Reject friend requests | Accept or reject a friend request after receiving a friend request system notification. |
| Add to the blocklist | Blocklist any user. If you blocklist friends, you also unfriend them. |
| Remove from the blocklist | Remove a user from the blocklist. |
| Obtain the blocklist | Pull the blocklist of users. |
| Remarks | Add remarks for a friend. |
| Set custom friend profile fields | Up to 20 custom fields are allowed. |
| Create a friend list | When creating a list, you can choose who goes to the list. A user can be added to multiple lists. |
| Delete a friend list | Delete a friend list. |
| Verify friends | Support verifying multiple friends at a time.|
| Verify users on a blocklist | Support verifying multiple users at a time.|
| Add a friend to a list | Add a friend to a list. |
| Delete a friend from a list | Remove a friend from a list. |
| Rename a friend list | Rename a friend list. |
| Obtain friend list information | Obtain a specific friend list. |
| Obtain all friend lists | Obtain the information of all friend lists. This can also be achieved by obtaining all friends. |
| Relationship chain storage | The SDK can store relationship chain information. |
| System notifications on friend profile changes | When a friend’s profile changes, you will receive a system notification. |
| System notification on relationship chain changes | When a relationship chain change occurs, you will receive a system notification. |



### Group features
Based on common use cases, IM has set the following default group types:
- A work group (Work) allows users to join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner.
- A public group (Public) allows the group owner to designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- A meeting group (Meeting) allows users to join and exit freely and supports viewing message history from before the user joined the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio and video conferences and online education.
- An audio-video group (AVChatRoom) allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.

The following table compares the default features of each group type:

<table>
   <tr>
      <th width="0px" style="text-align:center">Feature</td>
      <th width="0px" style="text-align:center">Work</td>
			 <th width="0px" style="text-align:center">Public</td>
       <th width="0px" style="text-align:center">Meeting</td>
			 <th width="0px" style="text-align:center">AVChatRoom</td>
   </tr>
   <tr>
      <td style="text-align:center">Maximum number of members</td>
      <td ><li>Trial Edition: 20 per group</li><br><li>Pro Edition: 200 per group by default; can be increased to 2,000 per group</li><br><li>Flagship Edition: 2,000 per group by default; can be increased to 6,000</li></td>
			      <td><li>Trial Edition: 20 per group</li><br><li>Pro Edition: 200 per group by default; can be increased to 2,000 per group</li><br><li>Flagship Edition: 2,000 by default; can be increased to 6,000 per group</li></td>
						      <td ><li>Trial Edition: 20 per group</li><br><li>Pro Edition: 200 per group by default; can be increased to 2,000 per group</li><br><li>Flagship Edition: 2,000 per group by default; can be increased to 6,000 per group</li></td>
									      <td>Unlimited</td>
   </tr>
   <tr>
     <td>Permission to modify a group profile</td>
     <td>Group members</td>
    <td><li>Group admins</li><br><li>Group owner</li><br><li>App admins</li></td>
    <td><li>Group owner</li><br><li>App admins</li></td>
    <td>App admins</td>
   </tr>
	   <tr>
     <td>Member lists</td>
     <td>Show all</td>
    <td>Show all</td>
    <td>Show all</td>
    <td>Show 300 members</td>
   </tr>
	   <tr>
     <td>Permission to delete a group</td>
     <td>App admins</td>
    <td><li>Group owner</li><br><li>App admins</li></td>
    <td><li>Group owner</li><br><li>App admins</li></td>
    <td><li>Group owner</li><br><li>App admins</li></td>
   </tr>
	   <tr>
     <td>Request to join a group</td>
     <td>Not supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
   </tr>
	   <tr>
     <td>Membership request approval</td>
     <td>Not supported</td>
    <td>Required</td>
    <td>Not required</td>
    <td>Not required</td>
   </tr>
	   <tr>
     <td>Inviting others to a group</td>
     <td>Confirmation from the invitee is not required.</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
   </tr>
	 	   <tr>
     <td>Group owner leaving the group</td>
     <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
   </tr>
	 	   <tr>
     <td>Setting admins</td>
     <td>Not supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
   </tr>
		 	   <tr>
     <td>Removing members from a group</td>
    <td><li>Group owner</li><br><li>App admins</li></td>
    <td><li>Group admins</li><br><li>Group owner</li><br><li>App admins</li></td>
    <td><li>Group admins</li><br><li>Group owner</li><br><li>App admins</li></td>
    <td>Not supported</td>
   </tr>
		 	   <tr>
     <td>Viewing message history from before the user joined the group</td>
     <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>Not supported</td>
   </tr>
		 	   <tr>
     <td>Member change notifications</td>
     <td>All members</td>
    <td>All members</td>
    <td>None</td>
    <td>All members</td>
   </tr>
		 	   <tr>
     <td>Group activation</td>
     <td>Activate via messages.</td>
    <td>Not required</td>
    <td>Not required</td>
    <td>Not required</td>
   </tr>
	 	   <tr>
     <td>Muting members</td>
     <td>Not supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
   </tr>
		 	   <tr>
     <td>Unread message count</td>
     <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
   </tr>
		 	   <tr>
     <td>Receiving messages as a guest</td>
     <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
   </tr>
		 	   <tr>
     <td>Historical message storage</td>
     <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
   </tr>
		 	   <tr>
     <td>Default message receiving option</td>
     <td>Receive online and offline pushed messages.</td>
    <td>Receive online and offline pushed messages.</td>
    <td>Receive only online pushed messages.</td>
    <td>Receive only online pushed messages.</td>
   </tr>
		 	   <tr>
     <td>Importing groups</td>
     <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
   </tr>
</table>




### IM console

You can log in to Tencent Cloud [IM console](https://console.cloud.tencent.com/im) to configure the app based on your needs.

| Feature Type | Description |
| ------- | --------------------- |
| App creation | Create an app. |
| App upgrade    | Upgrade the plan.              |
| SDK Download | Download the client SDK. |
| App configuration | Configure the app. |
| Statistics | View operations data. |
| Callback configuration | Perform third-party callbacks. |
| Feature configuration | Add custom fields and online instances. |
| Group management    | Add, modify, and delete groups; manage group members; send messages. |
| Developer tool | Generate UserSig on the webpage. |
| Content filtering    | Identify and screen out messages containing restricted words.  |



### Statistics

The [statistics and analytics](https://console.cloud.tencent.com/im) feature in the IM console allows you to view operational data in various dimensions.

| Statistic Type | Description |
| -------- | ----------------- |
| Active users | View the number of users (deduplicated) that have connected to and interacted with the server. |
| New registered users | View the number of newly registered users. |
| Total registered users | View the total number of registered users. |
| Upstream messages | Specify a time period and view the number of upstream messages. |
| Message senders | Specify a time period and view the number of message senders. |
| Peak concurrent online users | Specify a time period and view the number of concurrent online users. |
| One-to-one upstream messages | Specify a time period and view the number of one-to-one upstream messages. |
| One-to-one message senders | Specify a time period and view the number of one-to-one message senders. |
| Group upstream messages | Specify a time period and view the number of group upstream messages. |
| Group message senders | Specify a time period and view the number of group message senders. |
| Message sending groups | Specify a time period and view the number of groups that send messages. |
| New groups | Specify a time period and view the number of new groups. |
| Total groups | Specify a time period and view the total number of groups. |
| Data export | Specify a time period and export data. |

### Real-time monitoring
The [statistics and analytics](https://console.cloud.tencent.com/im) feature in the IM console allows you to view operations data in various dimensions.

| Statistic Type | Description |
| -------- | ---------- |
| Current online users  | Number of online users in real time     |
| One-to-one messages today  | Total number of one-to-one messages of the current day   |
| Ordinary group messages today | Number of non-audio-video group messages of the current day |
| Audio-video group messages today | Number of audio-video group messages of the current day  |

### Support for private deployment
Private deployment allows an enterprise to deploy systems directly to its own servers and keep data locally. IM provides the private deployment feature to assist enterprises in the deployment, implementation, and operation and maintenance of the private version. If needed, please apply for the [IM private service](https://intl.cloud.tencent.com/apply/p/itvi76h023).
>?To apply for the IM private service, you need to log in with your root account of Tencent Cloud.
