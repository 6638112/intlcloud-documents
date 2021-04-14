## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBResourceUsage) is used to view the usage information of database instance resources.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeDBResourceUsage. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. |
| StartTime | Yes | Date | Start date. Format: yyyy-mm-dd. |
| EndTime | Yes | Date | End date. Format: yyyy-mm-dd. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| BinlogDiskAvailable | [MonitorData](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#MonitorData) | Available space of a binlog disk (in GB) |
| DataDiskAvailable | [MonitorData](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#MonitorData) | Available space of a disk (in GB) |
| CpuUsageRate | [MonitorData](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#MonitorData) | CPU utilization |
| MemAvailable | [MonitorData](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#MonitorData) | Available space of memory (in GB) |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 View the usage information of instance resources

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBResourceUsage
&InstanceId=tdsql-ige1a5k3
&StartTime=2018-03-19
&EndTime=2018-03-19
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "BinlogDiskAvailable": {
      "Data": [
        1,
        1,
        1
      ],
      "EndTime": "2018-03-24 23:59:59",
      "StartTime": "2018-03-24 00:00:00"
    },
    "CpuUsageRate": {
      "Data": [
        1,
        1,
        1
      ],
      "EndTime": "2018-03-24 23:59:59",
      "StartTime": "2018-03-24 00:00:00"
    },
    "DataDiskAvailable": {
      "Data": [
        1,
        1,
        1
      ],
      "EndTime": "2018-03-24 23:59:59",
      "StartTime": "2018-03-24 00:00:00"
    },
    "MemAvailable": {
      "Data": [
        1,
        1,
        1
      ],
      "EndTime": "2018-03-24 23:59:59",
      "StartTime": "2018-03-24 00:00:00"
    },
    "RequestId": "32a93b23-cbd8-48a9-a75a-2274625099ca"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBResourceUsage)

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
| FailedOperation.OssOperationFailed | Failed to request backend APIs |
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.InnerSystemError | Internal system error |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.ShardNotExist | Shard does not exist |
| ResourceNotFound.NoInstanceFound | The specified database instance is not found |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

