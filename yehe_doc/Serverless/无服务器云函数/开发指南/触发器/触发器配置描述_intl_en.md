When you call the trigger API [CreateTrigger](https://intl.cloud.tencent.com/document/product/583/18589), the corresponding `TriggerDesc` parameter will be the trigger description, which can be used as instructed in this document.

## Timer Trigger
Please see [Cron Expression](<https://intl.cloud.tencent.com/document/product/583/9708#cron-.E8.A1.A8.E8.BE.BE.E5.BC.8F>).

### Sample TriggerDesc
Triggered once every 5 minutes:
```json
0 */5 * * * * *
```


## API Gateway Trigger

| Name | Type | Required | Description |
| ------- | ----------------------------- | ---- | ---------------------------- |
| api     | [ApigwApi](#ApigwApi)         | No | Creates API configuration for API gateway |
| service | [ApigwService](#ApigwService) | No   | Creates service configuration for API gateway |
| release | [ApigwRelease](#ApigwRelease) | No   | Release environment for created API gateway  |

### ApigwApi<span id="ApigwApi"></span>


| Name | Type | Required | Description |
| -------------------- | ------------------------------------------------- | ---- | ---------------------------------------------------- |
| authRequired         | String                                            | No | Whether authentication is required. Valid values: TRUE, FALSE. Default value: FALSE |
| requestConfig        | [ApigwApiRequestConfing](#ApigwApiRequestConfing) | No | Configuration of request backend API |
| isIntegratedResponse | String                                            | No | Whether to use integrated response. Valid values: TRUE, FALSE. Default value: FALSE |

### ApigwApiRequestConfing<span id="ApigwApiRequestConfing"></span>
| Name | Type | Required | Description |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| method | String | No   | Method configuration of request backend API. Valid values: `ANY`, `GET`, `HEAD`, `POST`, `PUT`, `DELETE` |

### ApigwService<span id="ApigwService"></span>

| Name | Type | Required | Description |
| --------- | ------ | ---- | -------------------------------------------- |
| serviceId | String | No | Apigw Service ID (if this parameter is not passed in, a new service will be created) |

### ApigwRelease<span id="ApigwRelease"></span>

| Name | Type | Required | Description |
| --------------- | ------ | ---- | ------------------------------------------------------------ |
| environmentName | String | Yes | Release environment. Valid values: `release`, `test`, `prepub`. If this parameter is left empty, `release` will be used by default |

### Sample TriggerDesc

```json
{
  "api":{
    "authRequired":"FALSE",
    "requestConfig":{
      "method":"ANY"
    },
    "isIntegratedResponse":"FALSE"
  },
  "service":{
    "serviceName":"SCF_API_SERVICE"
  },
  "release":{
    "environmentName":"release"
  }
}
```



## CKafka Trigger
| Name | Type | Required | Description |
| --------- | ------ | ---- | ---------------------------------------------------------- |
| maxMsgNum | String | Yes | A function invocation will be triggered once every time `maxMsgNum` CKafka messages are aggregated within 5 seconds |
| offset    | String | Yes   | `offset` is the position where consumption of CKafka messages starts. Valid values: `latest`, `earliest`, `timestamp at the millisecond level` |
| retry     | String | Yes   | Maximum number of retries when the function reports an error |


### Sample TriggerDesc
```json
{"maxMsgNum":100,"offset":"latest","retry":10000}
```
```json
{"maxMsgNum":999,"offset":"1595927203000","retry":10}
```

### API request description
To create a CKafka trigger by using an API request, the `TriggerName` field needs to be defined as the `instanceId` and `topicName` of the CKafka instance (`[instanceId]-[topicName]`) to dump to. <br>Below is an example:

```json
TriggerName: "ckafka-8tfxzia3-test"
```



## COS Trigger

| Name | Type | Required | Description |
| ------ | ----------------------- | ---- | -------------------- |
| event  | String                  | Yes   | [COS event type](https://intl.cloud.tencent.com/document/product/583/9707)      |
| filter | [CosFilter](#CosFilter) | Yes   | COS filename filter |

### CosFilter<span id="CosFilter"></span>

| Name | Type | Required | Description |
| ------ | ------ | ---- | --------------------------------- |
| Prefix | String | No   | Prefix rule of file filter                |
| Suffix | String | No   | Suffix rule of file filter, which must begin with `.` |


### COS event conflict rules
- Core concept: an event can trigger a function invocation at most once. If an event is bound to another product, it cannot be bound to a function.
- Set at most one prefix filter and one suffix filter.
- If the `cos:ObjectCreated:*` event is set but no prefix/suffix is set, subsequent binding to any event that starts with `cos:ObjectCreated` will fail.
- The filter will be valid only if both the prefix and suffix are matched, and if there are conflicts with both the prefix and suffix, subsequent binding will fail.

### Sample TriggerDesc
```json
{"event":"cos:ObjectCreated:*","filter":{"Prefix":"","Suffix":""}}
```
>!When `TriggerDesc` is used as a trigger description, the JSON string must be continuous with no spaces contained.

### API request description

To create a COS trigger by using an API request, the `TriggerName` field needs to be defined as the XML API access domain name of the COS bucket to dump to. Below is an example:
```json
TriggerName: "xxx.cos.ap-guangzhou.myqcloud.com"
```
>!To view the access domain name, go to the COS Console > **Bucket List** > **Basic Configuration** > **Basic Information**.


## CMQ Trigger

| Name | Type | Required | Description |
| ------ | ----------------------- | ---- | -------------------- |
| filterType  | String                  | No  |  Message filter type. `1`: tag; `2`: route match	   |
| filterKey | String  | No   | Message filter tag if `filterType` is `1`; `Binding Key` if `filterType` is `2` |

### Sample TriggerDesc
```json
{"filterType":1,"filterKey":["test"]}
```

```json
{"filterType":2,"filterKey":["#test"]}
```

### API request description

To create a CMQ trigger by using an API request, the `TriggerName` field needs to be defined as `CMQ Topic`. Below is an example:
```json
TriggerName: "Tabortest"
```
