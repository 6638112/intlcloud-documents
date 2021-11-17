## 操作场景

您可以通过配置 APIGW 来处理 WebHook 的投递事件，通过第三方 WebHook 接收其他系统产生的事件，APIGW 连接器是 HTTP 场景下理想的跨端接收事件的连接器。

APIGW 连接器实现方式为 **Push 模型**，APIGW 会监控请求并生成调用事件投递至事件集，并将相关事件通过事件规则路由到更多服务。



## 前提条件

已 [创建事件集](https://intl.cloud.tencent.com/document/product/1108/42285)。



## 操作步骤


1. 登录 [事件总线控制台](https://console.cloud.tencent.com/eb/)，选择左侧导航栏中的**事件集**。
2. 在“事件集”列表，选择期望配置 TDMQ 连接器的事件集。
3. 在“事件集详情”页事件连接器配置项中单击**添加**
4. 根据页面提示填写相关信息
	 其中**连接器类型**选择**API网关（APIGW）**连接器类型。
5. 单击**确定**完成创建。
6. 选择左侧导航栏中的**事件规则**。
7. 在“事件规则”顶部选框，选择与之前创建一致的事件集信息，并单击**新建事件规则**
8. 根据页面提示填写相关信息
	 其中**云服务类型**选择**API网关（APIGW）**，并配置触发目标端。
9. 单击**确定**即可创建 APIGW 连接器。



#### APIGW 连接器数据结构说明

```plaintext
{
    "specversion": "1.0.2",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "connector:apigw",
    "source": "apigw.cloud.tencent",
    "subjuect": "qcs::apigw:ap-guangzhou:uid1250000000/appidxxx:Serverid/Appid",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "data": {
        "headers": {
            "Accept-Language": "en-US,en,cn",
            "Accept": "text/html,application/xml,application/json",
            "Host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
            "User-Agent": "User Agent String"
        },
        "body": "{\"test\":\"body\"}",
        "stageVariables": {
            "stage": "release"
        },
        "path": "/test/value",
        "queryString": {
            "foo": "bar",
            "bob": "alice"
        },
        "httpMethod": "POST"
    }
}
```

参数说明如下：

| 参数        | 描述                                       |
| ----------- | ------------------------------------------ |
| path        | 记录实际请求的完整 Path 信息。             |
| httpMethod  | 记录实际请求的 HTTP 方法。                 |
| queryString | 记录实际请求的完整 Query 内容。            |
| body        | 记录实际请求转换为 String 字符串后的内容。 |
| headers     | 记录实际请求的完整 Header 内容。           |

