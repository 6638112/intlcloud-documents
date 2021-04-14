## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API queries the total number of visitors to a shop per hour in the specified time period. Supported time range: last 365 days (including the current day).

Default API request frequency limit: 100 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](https://cloud.tencent.com/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeShopHourTrafficInfo |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| CompanyId | Yes | String | Company ID |
| ShopId | Yes | Integer | Shop ID |
| StartDate | Yes | Date | Start date in yyyy-MM-dd format |
| EndDate | Yes | Date | End date in yyyy-MM-dd format |
| Offset | Yes | Integer | Offset: Pagination control parameter; 0 is passed in for the first page; Offset for the nth page = (n-1)*Limit |
| Limit | Yes | Integer | Limit: Data items per page; maximum value: 100; if over 100, the value will be force specified as 100 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| TotalCount | Integer | Total number of query results |
| ShopHourTrafficInfoSet | Array of [ShopHourTrafficInfo](https://cloud.tencent.com/document/api/860/18465#ShopHourTrafficInfo) | Hourly visitor traffic information |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Number of Hourly Visitors - Success

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeShopHourTrafficInfo
&CompanyId=testCompany1
&ShopId=123
&StartDate=2018-06-01
&EndDate=2018-06-15
&Offset=0
&Limit=100
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "CompanyId": "testCompany1",
    "RequestId": "6ec80684-0879-405e-8932-72e7c0c48ef8",
    "ShopHourTrafficInfoSet": [
      {
        "Date": "2018-06-01",
        "HourTrafficInfoDetailSet": [
          {
            "Hour": 12,
            "HourTrafficCount": 1000
          },
          {
            "Hour": 11,
            "HourTrafficCount": 1000
          }
        ]
      },
      {
        "Date": "2018-06-02",
        "HourTrafficInfoDetailSet": [
          {
            "Hour": 12,
            "HourTrafficCount": 1000
          },
          {
            "Hour": 11,
            "HourTrafficCount": 1000
          }
        ]
      }
    ],
    "ShopId": 123,
    "TotalCount": 2
  }
}
```

### Example 2. Getting Number of Hourly Visitors - Failure

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeShopHourTrafficInfo
&ShopId=123
&StartDate=2018-06-01
&EndDate=2018-06-15
&Offset=0
&Limit=100
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Error": {
      "Code": "InvalidParameter",
      "Message": "Parameter CompanyId is missing"
    },
    "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeShopHourTrafficInfo)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

Only the error codes related to the API are listed below. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/860/18453#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoData | No data. |
| FailedOperation.NoRight | Merchant has no permissions. |
| InternalError | Internal error |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Wrong parameter value |

