## Feature description

This API is used to determine whether the specified object exists and whether you have the permission to access it. You can use this API to get the object metadata if you can access it. To make this request, you need to have read permission for the object or the object needs to have public read permission enabled.

#### Versioning

With versioning enabled, you can specify the `versionId` request parameter to get the metadata of a specific version of the object. If the version ID you specify corresponds to a delete marker, an HTTP `404` status code (Not Found) will be returned. If no version ID is specified, the metadata of the latest version will be returned.

## Request

#### Sample request 

```shell
HEAD /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

| Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, the latest version will be queried | string | No |

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| If-Modified-Since | If the object is modified after the specified time, HTTP status code `200` (OK) will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned. | string | No |
| If-Unmodified-Since | If the object is not modified after the specified time, HTTP status code `200` (OK) will be returned; otherwise, HTTP status code `412` (Precondition Failed) will be returned. | string | No |
| If-Match | If the `ETag` of the object is the same as the specified value, HTTP status code `200` (OK) will be returned; otherwise, HTTP status code `412` (Precondition Failed) will be returned. | string | No |
| If-None-Match | If the `ETag` of the object is different from the specified value, HTTP status code `200` (OK) will be returned; otherwise, HTTP status code `304` (Not Modified) will be returned. | string | No |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, you will need to specify the headers related to server-side encryption to decrypt the object. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| Cache-Control  | Cache directives as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Content-Disposition                                         | File name as defined in RFC 2616, which will be returned only if it is contained in the object metadata | String  |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Expires                                                    | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string  |
| x-cos-meta-\* | Contains user-defined metadata and header suffixes | string |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA`, `ARCHIVE` and `DEEP_ARCHIVE`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). This header will be returned only if the storage class of the object is not `STANDARD`. | Enum |
| x-cos-storage-tier                                           |  Specifies the access tier for the object if it is stored in the INTELLIGENT TIERING storage class. Valid values: FREQUENT, INFREQUENT.  |  enum  |

#### Archived Object-Related Headers

If the storage class of the object is `ARCHIVE` and `POST Object restore` has been used to restore it, the following response headers will be returned:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| --- | --- | --- |
| x-cos-restore | Indicates the status of the restoration process:<br><li>If the restoration is ongoing, the value of the response header will be `ongoing-request="true"`<li>If the object has already been restored, the response header will include the time when COS will delete the temporary copy, e.g. `ongoing-request="false", expiry-date="Tue, 19 Nov 2019 16:00:00 GMT"` | string
| x-cos-restore-status | This parameter will be returned if the restoration is ongoing, indicating what restoration mode was used and when the restoration was requested, e.g. `tier="bulk"; request-date="Mon, 18 Nov 2019 09:34:50 GMT"`. For more information on restoration modes, see [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | string

**Versioning-Related Headers**

If the target object is from a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side Encryption Headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption headers. For more information, see [Server-side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Use Cases

#### Example 1. Simple example (versioning not enabled)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:17:36 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542656;1586549856&q-key-time=1586542656;1586549856&q-header-list=date;host&q-url-param-list=&q-signature=cde88925e00d1c90ba74985ca43b610bdf6b****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:17:36 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 18:17:25 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MGI4NDBfNjFjODJhMDlfMzY2NjVfMjNi****
```

#### Example 2. Specifying query conditions using request headers and returning a HTTP status code 304 (Not Modified)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Jul 2020 06:51:49 GMT
If-None-Match: "ee8de918d05640145b18f70f4c3aa602"
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1596005509;1596012709&q-key-time=1596005509;1596012709&q-header-list=date;host;if-none-match&q-url-param-list=&q-signature=9d087f05c259ca271efe91fc780cdced75c6****
Connection: close
```

#### Response

```shell
HTTP/1.1 304 Not Modified
Content-Type: application/xml
Content-Length: 0
Connection: close
Date: Wed, 29 Jul 2020 06:51:49 GMT
Server: tencent-cos
x-cos-request-id: NWYyMTFjODVfZDNjODJhMDlfMWU1MWVfOTUy****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODczNTBmNjMwZmQ0MTZkMjg0NjlkNTYyNmY4ZTRkZTk0NzJmZTI0ZmJhYTZmZjYyNmU5ZGNlZDI5YjkyODkwYjNhZjhlNGQ0MDY1ZGIxNDEwMWYwOTg1NDc4Mzg4MTE3****
```

#### Example 3. Specifying query conditions using request headers and returning a HTTP status code 412 (Precondition Failed)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Jul 2020 06:51:50 GMT
If-Match: "aa488bb80185a6be87f4a7b936a80752"
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1596005510;1596012710&q-key-time=1596005510;1596012710&q-header-list=date;host;if-match&q-url-param-list=&q-signature=38afe94fc61ca0b3aa763e00b23fd90ac23e****
Connection: close
```

#### Response

```shell
HTTP/1.1 412 Precondition Failed
Content-Type: application/xml
Content-Length: 0
Connection: close
Date: Wed, 29 Jul 2020 06:51:50 GMT
Server: tencent-cos
x-cos-request-id: NWYyMTFjODZfMzBjMDJhMDlfMmU3ZF9kYTE4****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODczNTBmNjMwZmQ0MTZkMjg0NjlkNTYyNmY4ZTRkZTk0NzJmZTI0ZmJhYTZmZjYyNmU5ZGNlZDI5YjkyODkwYjNhZDRkOWFlZjczOWExNjZmY2RiNjhjNGIwZWQ3YjYw****
```

#### Example 4. Using server-side encryption SSE-COS

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:18:19 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542699;1586549899&q-key-time=1586542699;1586549899&q-header-list=date;host&q-url-param-list=&q-signature=6a6d4dd5b5a9e6379f300715985bfb60b947****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:18:19 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 18:18:08 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MGI4NmJfNmRjMDJhMDlfZGQwNl8xZmE4****
x-cos-server-side-encryption: AES256
```

#### Example 5. Using server-side encryption SSE-KMS

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:18:30 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542710;1586549910&q-key-time=1586542710;1586549910&q-header-list=date;host&q-url-param-list=&q-signature=7c8a1c93b9701e653c2ab00419f976397d00****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:18:30 GMT
ETag: "00ca268468481b847fc2d8a9bd84578d"
Last-Modified: Fri, 10 Apr 2020 18:18:19 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MGI4NzZfN2FjODJhMDlfMjU3N18xYTEz****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### Example 6. Using Server-side Encryption SSE-C

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:18:41 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNE****
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG****
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542721;1586549921&q-key-time=1586542721;1586549921&q-header-list=date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=&q-signature=99ad258fc295f43feb0546bb2346c8269dc5****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:18:41 GMT
ETag: "582d9105f71525f3c161984bc005efb5"
Last-Modified: Fri, 10 Apr 2020 18:18:31 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MGI4ODFfN2NiODJhMDlfMmFmYTVfMWRh****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG****

```

#### Example 7. Requesting the latest version of an object (with versioning enabled)

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:19:15 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542755;1586549955&q-key-time=1586542755;1586549955&q-header-list=date;host&q-url-param-list=&q-signature=7909dc19780873dfaa51c8b238254098ca1a****
Connection: close

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 26
Connection: close
Date: Fri, 10 Apr 2020 18:19:15 GMT
ETag: "22e024392de860289f0baa7d6cf8a549"
Last-Modified: Fri, 10 Apr 2020 18:19:04 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 11596229263574363878
x-cos-request-id: NWU5MGI4YTNfZDZjODJhMDlfYmU0MV8xM2Y5****
x-cos-version-id: MTg0NDUxNTc1MzA5NjQ2ODI5MTg

```

#### Example 8. Requesting a specific version of an object (with versioning enabled)

#### Request

```shell
HEAD /exampleobject?versionId=MTg0NDUxNTc1MzA5NzU4ODg1Mjg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 18:19:04 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586542744;1586549944&q-key-time=1586542744;1586549944&q-header-list=date;host&q-url-param-list=versionid&q-signature=1307acd3e8649087c738ecca452a54fa5a79****
Connection: close

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:19:04 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 18:18:53 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MGI4OThfN2RiNDBiMDlfMTk1MTBfMWZj****
x-cos-version-id: MTg0NDUxNTc1MzA5NzU4ODg1Mjg
```

#### Example 9. Requesting an archived object that is being restored

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 27 Dec 2019 08:19:35 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577434775;1577441975&q-key-time=1577434775;1577441975&q-header-list=date;host&q-url-param-list=&q-signature=72408a09a5fc00d77d389559a0cfa5c98e31****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 27 Dec 2019 08:19:35 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 27 Dec 2019 08:19:23 GMT
Server: tencent-cos
x-cos-request-id: NWUwNWJlOTdfN2VjODJhMDlfOGI1N18yYjYz****
x-cos-restore: ongoing-request="true"
x-cos-restore-status: tier="expedited"; request-date="Fri, 27 Dec 2019 08:19:29 GMT"
x-cos-storage-class: ARCHIVE
```

#### Example 10. Requesting an archived object which has been restored

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 02 Jan 2020 18:09:51 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577988591;1577995791&q-key-time=1577988591;1577995791&q-header-list=date;host&q-url-param-list=&q-signature=ff23b3a44945f019916450add646e963c29b****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 16
Connection: close
Date: Fri, 10 Apr 2020 18:17:36 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Last-Modified: Fri, 10 Apr 2020 18:17:25 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 16749565679157681890
x-cos-request-id: NWU5MWRiZjFfMmViMDJhMDlfNjIwOF8zNTU0****
x-cos-restore: ongoing-request="false", expiry-date="Mon, 13 Apr 2020 16:00:00 GMT"
x-cos-storage-class: ARCHIVE
```
