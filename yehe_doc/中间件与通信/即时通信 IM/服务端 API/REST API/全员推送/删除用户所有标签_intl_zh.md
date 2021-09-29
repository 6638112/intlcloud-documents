## 功能说明
管理员给用户删除所有标签。注意每次最多只能给100个用户删除所有标签。

## 接口调用说明
本功能**仅针对旗舰版客户开放申请（如您降级为专业版将无法使用），您可通过工单申请开通该功能，申请后我们将对您的需求进行评估，需求评估合理后您方可使用该功能**。

### 请求 URL 示例
```
https://xxxxxx/v4/all_member_push/im_remove_all_tags?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
```


### 请求参数说明

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| https   | 请求协议为 HTTPS，请求方式为 POST       |
| xxxxxx |SDKAppID 所在国家/地区对应的专属域名<li>中国：`console.tim.qq.com`<li>新加坡： `adminapisgp.im.qcloud.com`<li>首尔： `adminapikr.im.qcloud.com`<li>法兰克福：`adminapiger.im.qcloud.com` |
| v4/all_member_push/im_remove_all_tags  | 请求接口                  |
| usersig            | App 管理员帐号生成的签名，参见 [UserSig 后台 API](https://intl.cloud.tencent.com/document/product/1047/34385)                            |
| identifier         | 必须为 App 管理员帐号                |
| sdkappid           | 创建应用时即时通信控制台分配的 SdkAppid |
| random             | 32位无符号整数随机数                 |
| contenttype        | 固定值为：json                       |

### 最高调用频率

100次/秒。

### 请求包示例

```
{
	"To_Account": [
		"xiaojun012",
		"xiaojun013"
	]
}
```

### 请求包字段说明

| 字段 | 类型| 属性 | 说明 |
|---------|---------|---------|---------|
| To_Account | String | 必填 |目标用户帐号 |

### 应答包体示例

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### 应答包字段说明


| 字段|类型 |说明 |
|---------|---------|---------|
| ActionStatus| String | 请求处理的结果，OK 表示处理成功，FAIL 表示失败  |
| ErrorCode| Integer | 错误码  |
| ErrorInfo| String | 错误信息  |


## 错误码说明
除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200。**真正的错误码，错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的**。公共错误码（60000到79999）参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 |含义说明 |
|---------|---------|
| 90001 | JSON 格式解析失败，请检查请求包是否符合 JSON 规范。|
| 90009 | 请求需要 App 管理员权限。|
| 90018 | 请求的帐号数量超过限制。|
| 91000 | 服务内部错误，请重试。|

## 接口调试工具
通过 [REST API 在线调试](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/all_member_push/im_remove_all_tags) 工具调试本接口。

## 参考
- [全员推送接口说明](https://intl.cloud.tencent.com/document/product/1047/37165) 
- [全员推送](https://intl.cloud.tencent.com/document/product/1047/37166) 
- [设置应用属性名称](https://intl.cloud.tencent.com/document/product/1047/37167) 
- [获取应用属性名称](https://intl.cloud.tencent.com/document/product/1047/37168) 
- [设置用户属性](https://intl.cloud.tencent.com/document/product/1047/37170)  
- [删除用户属性](https://intl.cloud.tencent.com/document/product/1047/37171)  
- [获取用户属性](https://intl.cloud.tencent.com/document/product/1047/37169)  
- [添加用户标签](https://intl.cloud.tencent.com/document/product/1047/37173)  
- [获取用户标签](https://intl.cloud.tencent.com/document/product/1047/37172)  
- [删除用户标签](https://intl.cloud.tencent.com/document/product/1047/37174)  
