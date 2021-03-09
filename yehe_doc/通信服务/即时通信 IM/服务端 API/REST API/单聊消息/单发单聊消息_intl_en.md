## Feature Description 
- When the administrator sends a message to an account, the sender displayed to the recipient is the administrator.
- When the administrator specifies an account to send a message to another account, the sender displayed to the recipient is not the administrator, but the account specified by the administrator.
- This API does not check whether the sender and the recipient are friends or blocklisted by either party or whether the recipient is muted.

>!When calling this API to send a one-to-one message, you must specify whether to synchronize the message to the sender, which is the administrator account or the account specified by the administrator. Synchronization can be implemented via online terminals and roaming servers. This API provides the `SyncOtherMachine` parameter to determine whether to synchronize the message. For more information, see **Sample request packet** below.

## API Call Description
### Sample request URL
```
https://console.tim.qq.com/v4/openim/sendmsg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/openim/sendmsg | The request API |
| sdkappid | The SDKAppID assigned by the IM console when an application is created |
| identifier | The app administrator account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum call frequency

200 calls per second

### Sample request packets
Here, we use sending a text message as an example. To send messages of other types, set `MsgBody` to the corresponding message type. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527).

#### The administrator sends a message to another account.

>!If you do not want to synchronize the message to `From_Account`, set `SyncOtherMachine` to `2`. To synchronize the message to `From_Account`, set `SyncOtherMachine` to `1`.

```
{
    "SyncOtherMachine": 2, // Do not synchronize the message to the sender.
    "To_Account": "lumotuwe2",
    "MsgLifeTime":60, // Retain the message for 60 seconds.
    "MsgRandom": 1287657,
    "MsgTimeStamp": 1557387418,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```

#### The administrator sends a message to another account and forbids callbacks for the message.

>!If you do not want to synchronize the message to `From_Account`, set `SyncOtherMachine` to `2`. To synchronize the message to `From_Account`, set `SyncOtherMachine` to `1`.

```
{
    "SyncOtherMachine": 2, // Do not synchronize the message to the sender.
    "To_Account": "lumotuwe2",
    "MsgLifeTime":60, // Retain the message for 60 seconds.
    "MsgRandom": 1287657,
    "MsgTimeStamp": 1557387418,
    "ForbidCallbackControl":[
        "ForbidBeforeSendMsgCallback",
        "ForbidAfterSendMsgCallback"], // Callback forbidding control option
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```

#### The administrator specifies an account to send a message to another account and set the information of offline push, without synchronizing the message to `From_Account`.
>!If you do not want to synchronize the message to `From_Account`, set `SyncOtherMachine` to `2`.

```
{
    "SyncOtherMachine": 2,
    "From_Account": "lumotuwe1",
    "To_Account": "lumotuwe2",
    "MsgLifeTime":3600, // Retain the message for 1 hour.
    "MsgRandom": 1287657,
    "MsgTimeStamp": 1557387418,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ],
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Desc": "The content to be pushed offline",
        "Ext": "The passthrough content",
        "AndroidInfo": {
            "Sound": "android.mp3"
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1, // If this field is not specified or is set to `0`, the message is counted. If this field is set to `1`, the message is not counted, that is, the icon number in the upper-right corner does not increase.
            "Title":"apns title", // APNs title
            "SubTitle":"apns subtitle", // APNs subtitle
            "Image":"www.image.com" // Image URL
        }
    }
}
```

#### The administrator specifies an account to send a message to another account and allows synchronization of the message to `From_Account` (the sender’s terminal).
>!To synchronize the message to `From_Account`, set `SyncOtherMachine` to `1`.

```
{
    "SyncOtherMachine": 1, // Synchronize the message to the sender.
    "From_Account": "lumotuwe1",
    "To_Account": "lumotuwe2",
    "MsgRandom": 1287657,
    "MsgTimeStamp": 1557387418,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ]
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|----|---------|
| SyncOtherMachine | Integer | No | `1`: synchronize the message to the `From_Account` online terminal and roaming server.<br/>`2`: do not synchronize the message to `From_Account`.<br/>If this field is not specified, the message will be synchronized to the `From_Account` roaming server by default. |
| From_Account | String | No | The UserID of the sender (used to specify the message sender) |
| To_Account | String | Yes | The UserID of the recipient |
| MsgLifeTime | Integer | No | The offline retention period of the message (unit: second); max. period: 7 days (604800 seconds). <li>If this field is set to `0`, the message will only be sent to the recipient online and not retained offline. </li><li>If this field is set to a period longer than 7 days (604800 seconds), the message will still be retained for only 7 days. </li><li>If this field is not set, the message will be retained for 7 days by default.</li> |
| MsgRandom | Integer | Yes | The random number of the message. It is used by the backend for message deduplication within a second. Make sure the random number is entered. |
| MsgTimeStamp | Integer | No | The message timestamp in UNIX format (unit: second) |
| ForbidCallbackControl | Array | No | Message callback forbidding field, which is valid only for this message. `ForbidBeforeSendMsgCallback` forbids the callback before sending the message. `ForbidAfterSendMsgCallback` forbids the callback after sending the message. |
| MsgBody | Object | Yes | Message body. For details on formats, please see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). (Note: a message can contain multiple message elements, in which case `MsgBody` is an array.) |
| MsgType | String | Yes | TIM message object type. Supported message objects include `TIMTextElem` (text message), `TIMFaceElem` (emoji message), `TIMLocationElem` (location message), and `TIMCustomElem` (custom message). |
| MsgContent | Object | Yes | Different message object types (`MsgType`) have different formats (`MsgContent`). For details, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| OfflinePushInfo | Object | No | Offline push information. For details, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |


### Sample response packets
- Response to a successful request
```
{
    "ActionStatus": "OK", 
    "ErrorInfo": "", 
    "ErrorCode": 0, 
    "MsgTime": 1572870301,
    "MsgKey": "89541_2574206_1572870301"
}
```

- Response to a failed request
```
{
    "ActionStatus": "FAIL", 
    "ErrorInfo": "Fail to Parse json data of body, Please check it", 
    "ErrorCode": 90001
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode| Integer | Error code. `0`: successful. Other values: failed. |
| ErrorInfo | String | Error information |
| MsgTime | Integer | Message timestamp in the UNIX format |
| MsgKey | String | The unique identifier of the message. This field is required to recall a message. The value is a string of no more than 50 characters. |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 20001 | Invalid request packet. |
| 20002 | UserSig or A2 has expired. |
| 20003 | The UserID of the sender or recipient is invalid or does not exist. Make sure that the UserID has been imported into IM. |
| 20004 | Network exception. Try again. |
| 20005 | Internal server error. Try again. |
| 20006 | The callback before sending a one-to-one message was triggered, and the app backend returned a response to forbid delivering the message. |
| 90001 | Failed to parse the JSON request packet. Make sure the format is valid. |
| 90002 | The `MsgBody` in the JSON request packet does not meet message format requirements or `MsgBody` is not an array. For more information, please see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90003 | The JSON request packet does not contain the `To_Account` field or the `To_Account` field is not a string. |
| 90005 | The JSON request packet does not contain the `MsgRandom` field or the `MsgRandom` field is not an integer. |
| 90006 | The `MsgTimeStamp` field in the JSON request packet is not an integer. |
| 90007 | The `MsgBody` field in the JSON request packet is not an array. Change it to an array. |
| 90009 | The request requires app admin permissions. |
| 90010 | The JSON request packet does not meet message format requirements. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90012 | The account specified in `To_Account` does not exist or has not been registered. Make sure the account has been imported to IM and is correctly spelled. |
| 90026 | The offline retention time of the message is incorrect. Messages cannot be retained offline for more than 7 days. |
| 90031 | The `SyncOtherMachine` field in the JSON request packet is not an integer. |
| 90044 | The `MsgLifeTime` field in the JSON request packet is not an integer. |
| 91000 | Internal service error. Try again. |
| 90992 | Internal service error. Try again. If this error code is returned for all requests and third-party callback is enabled, make sure the app server returns the callback results to the IM backend normally. |
| 93000 | The JSON packet has exceeded the maximum size of 8 KB. |
| 90048 | The requested account does not exist. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openim/sendmsg) to debug this API.

## References
Sending One-to-One Messages to Multiple Users ([v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920))
Querying One-to-One Messages ([v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478))
Recalling One-to-One Messages ([v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015))

## Possible Callbacks

- [Callback Before Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34364)
- [Callback After Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34365)
