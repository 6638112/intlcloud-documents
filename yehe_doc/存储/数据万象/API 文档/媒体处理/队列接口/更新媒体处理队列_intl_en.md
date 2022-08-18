## Feature Description

This API (`UpdateMediaQueue`) is used to update a queue.

## Request

#### Sample request

```plaintext
PUT /queue/p8eb46b8cc1a94bc09512d16c5c4f4d3a HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
    <Name>Queue Name</Name>
    <QueueID></QueueID>
    <State></State>
    <NotifyConfig>
        <Type></Type>
        <Url></Url>
        <Event></Event>
    </NotifyConfig>
</Request>
```

The nodes are described as follows:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>None</td>
      <td>Request container</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
</table>

`Request` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
      <th>Constraints</th>
   </tr>
   <tr>
      <td>Name</td>
      <td>Request</td>
      <td>Template name</td>
      <td>String</td>
      <td>Yes</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>QueueID</td>
      <td>Request</td>
      <td>Channel ID</td>
      <td>String</td>
      <td>Yes</td>
      <td>-</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request</td>
      <td>Channel status</td>
      <td>String</td>
      <td>Yes</td>
      <td>
        1. Active: Jobs in the channel will be scheduled and executed for transcoding by the media transcoding service. <br>2. Paused: The channel is paused, and jobs in it will no longer be scheduled and executed. All jobs in the channel will remain in the `Submitted` status, while jobs being executed will continue without being affected.
      </td>
   </tr>
   <tr>
      <td>NotifyConfig</td>
      <td>Request</td>
      <td>Notification channel</td>
      <td>Container</td>
      <td>Yes</td>
      <td>Third-party callback URL</td>
   </tr>
</table>

`NotifyConfig` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
      <th>Constraints</th>
   </tr>
   <tr>
      <td>Url</td>
      <td>Request.NotifyConfig</td>
      <td>Callback configuration</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>Type</td>
      <td>Request.NotifyConfig</td>
      <td>Callback type. General callback: Url</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>Event</td>
      <td>Request.NotifyConfig</td>
      <td>Job completed: TaskFinish; workflow completed: WorkflowFinish</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request.NotifyConfig</td>
      <td>Callback switch: `Off` or `On`</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
</table>



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <Queue>
        <QueueId></QueueId>
        <Name></Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>mts-topic-1</Url>
            <Type></Type>
            <Event></Event>
        </NotifyConfig>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </Queue>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| Queue              | Response | Queue information. Same as `Response.QueueList` in [DescribeMediaQueues](https://intl.cloud.tencent.com/document/product/1045/43672).  | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```plaintext
PUT /queue/p8eb46b8cc1a94bc09512d16c5c4f4d3a HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Name>Queue Name</Name>
    <QueueID></QueueID>
    <State></State>
    <NotifyConfig>
        <Type></Type>
        <Url></Url>
        <Event></Event>
    </NotifyConfig>
</Request>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <Queue>
        <QueueID></QueueID>
        <Name></Name>
        <State>Active</State>
        <NotifyConfig>
            <Type></Type>
            <Url></Url>
            <Event></Event>
        </NotifyConfig>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </Queue>
</Response>
```
