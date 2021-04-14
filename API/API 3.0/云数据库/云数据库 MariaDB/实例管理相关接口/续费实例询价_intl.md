## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeRenewalPrice) is used to query the renewal price when you renew a database instance.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeRenewalPrice. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID to be renewed, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |
| Period | No | Integer | Renewal period (in month). It defaults to 1 if left empty. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Original price (in 0.01 CNY) |
| Price | Integer | Actual price (in 0.01 CNY). It may be different from the original price depending on the discount. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the renewal price of a database instance

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeRenewalPrice
&InstanceId=tdsql-fdpjf5zh
&Period=1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "OriginalPrice": 21120,
    "Price": 21120,
    "RequestId": "5b637383-8059-b0f8-3dcd-59fbdff262b6"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeRenewalPrice)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.QueryPriceFailed | Failed to query the price |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.SpecIdIllegal | No specification of a database instance found |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

