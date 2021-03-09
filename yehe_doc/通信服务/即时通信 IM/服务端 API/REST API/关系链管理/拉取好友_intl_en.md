## Feature Description
- This API is used to pull the data of all friends by page.
- It cannot pull profile data.
- You do not need to specify the fields to pull. By default, all standard and custom friend data will be returned.

## API Call Description
### Sample request URL
```
https://console.tim.qq.com/v4/sns/friend_get?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters
The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/sns/friend_get  | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created |
| identifier | The administrator account of the app. For more information, please see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum call frequency

200 calls per second

### Sample request

```
{
    "From_Account": "id",
    "StartIndex": 0,
    "StandardSequence": 0,
    "CustomSequence": 0
}
```

### Request fields

| Field | Type | Required | Description |
|-------|-------|-------|------|
| From_Account|String |Yes|The UserID of the account that requests to pull friend data|
| StartIndex|Integer |Yes|The starting point of the page to be pulled|
| StandardSequence|Integer |No|The `StandardSequence` returned for the previous friend data pull. If the value of the `StandardSequence` field is the same as that in the backend, the backend will not return standard friend data.|
| CustomSequence|Integer |No|The `CustomSequence` returned for the previous friend data pull. If the value of the `CustomSequence` field is the same as that in the backend, the backend will not return custom friend data.|

### Sample response

```
{
    "UserDataItem": [
        {
            "To_Account": "id1",
            "ValueItem": [
                {
                    "Tag": "Tag_SNS_IM_AddSource",
                    "Value": "AddSource_Type_Android"
                },
                {
                    "Tag": "Tag_SNS_IM_Remark",
                    "Value": "Remark1"
                },
                {
                    "Tag": "Tag_SNS_IM_Group",
                    "Value":["Group1","Group2"]
                },
                {
                    "Tag": "Tag_SNS_IM_AddTime",
                    "Value": 1563867420
                },
                {
                    "Tag": "Tag_SNS_Custom_Test",
                    "Value": "CustomData1"
                }
            ]
        },
        {
            "To_Account": "id2",
            "ValueItem": [
                {
                    "Tag": "Tag_SNS_IM_AddSource",
                    "Value": "AddSource_Type_IOS"
                },
                {
                    "Tag": "Tag_SNS_IM_Group",
                    "Value":["Group1"]
                },
                {
                    "Tag": "Tag_SNS_IM_AddTime",
                    "Value": 1563867425
                }
            ]
        }
    ],
    "StandardSequence": 88,
    "CustomSequence": 46,
    "FriendNum": 20,
    "CompleteFlag": 1,
    "NextStartIndex": 0,
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": "",
    "ErrorDisplay": ""
}
```

### Response fields

| Field | Type | Description |
|------|------|------|
| UserDataItem|Array|The friend object array. Each friend object contains a `To_Account` field and a `ValueItem` array.|
| To_Account | String | The UserID of a friend |
| ValueItem|Array|The array for storing friend data. Each array element contains a `Tag` field and a `Value` field.|
| Tag|String|The name of a friend field|
| Value|String/integer/array|The value of a friend field. For details, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521#.E5.85.B3.E7.B3.BB.E9.93.BE.E5.AD.97.E6.AE.B5">Relationship Chain Fields</a>.|
| StandardSequence|Integer|The sequence for standard friend data. The client can save this sequence and return it to the backend via the `StandardSequence` field in the next request.|
| CustomSequence|Integer|The sequence for custom friend data. The client can save this sequence and return it to the backend via the `CustomSequence` field in the next request.|
| FriendNum|Integer|The total number of friends|
| CompleteFlag|Integer|The ending tag of the page. A non-zero value indicates that all friend data is pulled.|
| NextStartIndex|Integer|The starting point of the next page|
| ActionStatus|String|The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode|Integer|Error code. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo|String|Detailed error information |
| ErrorDisplay|String|Detailed information displayed on the client |

<span id="ErrorCode"></span>
## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app administrator permissions. |
| 30006 | Internal server error. Please try again. |
| 30007 | Network timeout. Please try again later. |


## Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/sns/friend_get) to debug this API.

## References

- Adding Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34905">v4/sns/friend_delete</a>)
- Deleting All Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Verifying Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34907">v4/sns/friend_check</a>)
- Pulling Specified Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)
