The event callback service can notify your server of TRTC events in the form of HTTP/HTTPS requests, including some events of the room and media event groups. To enable the service, you need to provide configuration information to Tencent Cloud.

[](id:deploy)
## Configuration Information
You can configure callback information in the TRTC console, and will receive event callback notifications after the configuration. For detailed directions, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/647/39559).


>!You need to provide the following information:
>- **Required**: An HTTP/HTTPS server address to receive callback notifications
>- **Optional**: A custom key containing up to 32 uppercase and lowercase letters and digits, which is needed for the calculation of signatures

## Timeout and Retry
A notification will be considered failed if the callback server does not receive a response from your server within 5 seconds of message sending. It will try again immediately after the first failure and retry **10 seconds** after every subsequent failure. The retries will stop 1 minute after the first try.

[](id:format)
## Format of Callback Messages

Callbacks are sent to your server in the form of HTTP/HTTPS POST requests, which consist of the following parts:

- **Character encoding**: UTF-8
- **Request**: JSON for the request body
- **Response**: HTTP STATUS CODE = 200. The server ignores the content of the response packet. For protocol-friendliness, we recommend adding `JSON: `{"code":0}` to the response.
- **Packet body sample**: Below is an example of the packet body for room entry under the room event group.
<dx-codeblock>
::: JSON JSON
{
    "EventGroupId": 1,        #Room event group
    "EventType": 103,        #Room entry event
    "CallbackTs": 1615554923704,        #Callback time, in milliseconds
    "EventInfo": {
        "RoomId": 12345,        #Numeric room number
        "EventTs": 1615554922,        #Event occurrence time, in seconds
        "UserId": "test",        #User ID
        "UniqueId": 1615554922656,        #Unique identifier
        "Role": 20,                     #User role: Anchor
        "TerminalType": 3,        #Device type: iOS
        "UserType": 3,        #User type: Native SDK
        "Reason": 1        #Reason: Voluntary entry
	}
}
:::
</dx-codeblock>



## Parameters
[](id:message)
### Callback message parameters

- The header of a callback message contains the following fields.
<table id="header">
<tr><th>Field</th><th>Value</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>Signature value</td>
</tr><tr>
<td>SdkAppId</td><td>SDK application ID</td>
</tr></table>
- The body of a callback message contains the following fields.
<table id="body">
<tr><th>Field</th><th>Type</th><th>Description</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">Event group ID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">Type of callback event</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>Unix timestamp (ms) of callback sending</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">Event information</a></td>
</tr>
</tbody></table>

[](id:eventId)
### Event group ID

| Field            | Value   | Description       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | Room event group |
| EVENT_GROUP_MEDIA | 2    | Media event group |

[](id:event_type)
### Event type

| Field                  | Value   | Description             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | Creating room         |
| EVENT_TYPE_DISMISS_ROOM | 102  | Closing room         |
| EVENT_TYPE_ENTER_ROOM   | 103  | Entering room        |
| EVENT_TYPE_EXIT_ROOM    | 104  | Leaving room          |
|  EVENT_TYPE_CHANGE_ROLE   | 105  |    Switching roles      |
| EVENT_TYPE_START_VIDEO  | 201  | Starting pushing video data |
| EVENT_TYPE_STOP_VIDEO   | 202  | Stopping pushing video data |
| EVENT_TYPE_START_AUDIO  | 203  | Starting pushing audio data |
| EVENT_TYPE_STOP_AUDIO   | 204  | Stopping pushing audio data |
| EVENT_TYPE_START_ASSIT  | 205  | Starting pushing substream data |
| EVENT_TYPE_STOP_ASSIT   | 206  | Stopping pushing substream data |


[](id:event_infor)
### Event information



| Field  | Type   | Description                              |
| ------- | ------ | --------------------------------- |
|RoomId      |     String/Number       |     Room ID, which is of the same type as the room ID on the client    |
|EventTs      |    Number     |      Unix timestamp (seconds) of event occurrence. This field is reserved for compatibility purposes.|
| EventMsTs | Number | Unix timestamp (ms) of event occurrence    |
| UserId | String | User ID |
| UniqueId  | Number | Unique identifier, optional, carried by the room event group. [](id:UniqueId)<br> When a user experiences unusual events such as network change or abnormal exit and reentry, your server may receive multiple callbacks for the entry and exit of the same user. A unique identifier helps identify that the multiple exits and entries are by the same user. |
| Role    | Number | [Role type](#role_type), optional, carried during room entry/exit  |
|TerminalType  |  Number    |   [Device type](#terminal), optional, carried during room entry |
|UserType  |  Number   |    [User type](#usertype), optional, carried during room entry |
| Reason  | Number | [Reason](#reason), optional, carried during room entry/exit |


>! We have developed a policy that prevents repeated callbacks resulting from unusual events on the client. If you start using the callback service after July 30, 2021, the policy will apply by default, and the room event group will no longer carry [UniqueId](#UniqueId).


[](id:role_type)
### Role type

| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | Anchor |
| MEMBER_TRTC_VIEWER | 21   | Audience |


[](id:terminal)
### Device type
| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| TERMINAL_TYPE_WINDOWS | 1 | Windows   |
| TERMINAL_TYPE_ANDROID | 2  | Android  |
| TERMINAL_TYPE_IOS | 3  | iOS |
| TERMINAL_TYPE_LINUX | 4  | Linux |
| TERMINAL_TYPE_OTHER | 100  | Other |

[](id:usertype)
### User type
| Field             | Value   | Description |
| ------------------ | ---- | ---- |
| USER_TYPE_WEBRTC | 1 | WebRTC   |
| USER_TYPE_APPLET | 2  | Mini Program |
| USER_TYPE_NATIVE_SDK | 3  | Native SDK |


[](id:reason)
### Reason

| Field    | Description                              |
| -------  | --------------------------------- |
|Room entry   |<li/>1: Voluntary entry <li/>2: Network change<li/>3: Timeout and retry <li/>4: Co-anchoring |
|Room exit | <li/>1: Voluntary exit <li/>2: Timeout<li/>3: Removed from the room<li/>4: Co-anchoring was canceled.<li/>5: The process was force-killed.<br>**Note: TRTC cannot capture a force-kill event on Android and will send a callback only after timeout (`reason` = `2`).**|




### Signature calculation
Signatures are calculated using the HMAC SHA256 encryption algorithm. Upon receiving a callback message, your server will calculate a signature using the same method, and if the results match, it indicates that the callback is from TRTC and not forged. See below for the calculation method.
```
// In the formula below, `key` is the key used to calculate a signature.
Sign = base64(hmacsha256(key, body))
```

>! `body` is the original packet body of the callback request you receive. Do not make any modifications. Below is an example.
>```
>body="{\n\t\"EventGroupId\":\t1,\n\t\"EventType\":\t103,\n\t\"CallbackTs\":\t1615554923704,\n\t\"EventInfo\":\t{\n\t\t\"RoomId\":\t12345,\n\t\t\"EventTs\":\t1608441737,\n\t\t\"UserId\":\t\"test\",\n\t\t\"UniqueId\":\t1615554922656,\n\t\t\"Role\":\t20,\n\t\t\"Reason\":\t1\n\t}\n}"
>```
