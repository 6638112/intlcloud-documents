## Feature Description

This API (`DescribeMediaTemplates`) is used to search for text-to-speech templates.

## Request

#### Sample request

```shell
GET /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---           |:--       |:--                    |   :--     |   :--    |
| Tag           | None        | Template type: Tts       | String    | Yes |
| Category      | None   | Template category: Custom (default) or Official | String    |Yes|
| Ids           | None        | Template ID. If you enter multiple IDs, separate them with commas (,).  | String     |No|
| Name          | None        | Template name prefix              | String     |No|
| PageNumber    | None        | Page number                   | Integer     |No|
| PageSize      | None        | Number of entries per page                 | Integer     |No|


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Tts</Tag>
        <TtsTpl>
            <Mode>Sync</Mode>
            <Codec>pcm</Codec>
            <VoiceType>ruxue</VoiceType>
            <Volume>2</Volume>
            <Speed>200</Speed>
        </TtsTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of templates                       | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| TemplateList       | Response | Template array                       | Container |

`TemplateList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.TemplateList | Template ID                                                      | String    |
| Name               | Response.TemplateList | Template name                                                     | String    |
| BucketId           | Response.TemplateList | Template bucket                                                | String    |
| Category           | Response.TemplateList | Template category: Custom or Official                                | String    |
| Tag                | Response.TemplateList | Template type: Tts                                        | String    |
| UpdateTime         | Response.TemplateList | Update time                                                     | String    |
| CreateTime         | Response.TemplateList | Creation time                                                     | String    |
| Tts                | Response.TemplateList | Template parameters                                                | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Use Cases
#### Use case 1. Querying by template ID
#### Request

```shell
GET /template?ids=A,B,C HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Tts</Tag>
        <TtsTpl>
            <Mode>Sync</Mode>
            <Codec>pcm</Codec>
            <VoiceType>ruxue</VoiceType>
            <Volume>2</Volume>
            <Speed>200</Speed>
        </TtsTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
    <NonExistTIDs>
        <TemplateId>B</TemplateId>
        <TemplateId>C</TemplateId>
    </NonExistTIDs>
</Response>
```

#### Use case 2. Querying by paginated list

#### Request

```shell
GET /template?pageSize=10&pageNumber=1 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Tts</Tag>
        <TtsTpl>
            <Mode>Sync</Mode>
            <Codec>pcm</Codec>
            <VoiceType>ruxue</VoiceType>
            <Volume>2</Volume>
            <Speed>200</Speed>
        </TtsTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```
