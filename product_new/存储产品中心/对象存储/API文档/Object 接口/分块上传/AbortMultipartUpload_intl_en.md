## Description
This API is used to abort a multipart upload and delete the uploaded parts. If you call this API and there is an `Upload Part` request that is using the multipart upload, the request will fail. If the `uploadId` does not exist, `404 NoSuchUpload` will be returned.

>  It is recommended to either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

## Request

### Sample Request
```shell
DELETE /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

See the details below:

| Parameter Name | Description | Type | Required |
|---|---|---|---|
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |

### Request Headers
This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

### Request Body
The request body of this request is empty.

## Response

### Response Headers

This API only uses common response headers. For more information on common request headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

### Response Body
The response body is empty.

#### Error Code

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Example

### Request
```shell
DELETE /exampleobject?uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 26 Oct 2013 21:22:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484728626;32557624626&q-key-time=1484728626;32557624626&q-header-list=host&q-url-param-list=uploadId&q-signature=2d3036b57cade4a257b48a3a5dc922779a56****
```

### Response
```shell
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 26 Oct 2013 21:22:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI5MzlfOTgxZjRlXzZhYjNf****
```
