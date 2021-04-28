## Download and Installation

#### Relevant resources

- Download the COS XML SDK resources for Node.js [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- Download the XML SDK for Node.js [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-nodejs-sdk-v5/latest/cos-nodejs-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).
- Find the complete sample code [here](https://github.com/tencentyun/cos-snippets/tree/master/NodeJS).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/CHANGELOG.md).

#### Environmental dependency

1. To use the SDK, your operating environment should have Node.js and npm.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

> ?For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

#### Installing SDK

Install the SDK through npm which can be downloaded [here](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization

#### Initializing with permanent key

First, log into the CAM console, and get your `SecretId` and `SecretKey` from the [Access Key](https://console.cloud.tencent.com/cam/capi) page.
Replace `SecretId`, `SecretKey`, `bucket`, and `region` with the actual values in your development environment. To test file upload, please see the following sample code.

[//]: # (.cssg-snippet-global-init)
```js
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY'
});
```

#### Initializing with temporary key

For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048). The SDK for Node.js supports initialization by passing in a temporary key as shown in the sample code below:

[//]: # (.cssg-snippet-global-init-sts)
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        request({
            url: 'https://example.com/sts',
            data: {
                // The required parameters can be obtained from options
            }
        }, function (err, response, body) {
            try {
                var data = JSON.parse(body);
                var credentials = data.credentials;
            } catch(e) {}
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId, // tmpSecretId of the temporary key
                TmpSecretKey: credentials.tmpSecretKey, // tmpSecretKey of the temporary key
                XCosSecurityToken: credentials.sessionToken, // sessionToken of the temporary key
                ExpiredTime: data.expiredTime, // Expiration timestamp of the temporary key, which is calculated by adding durationSeconds to the timestamp when applying for the temporary key
            });
        });
    }
});
```

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js).

### Configuration items

#### Constructor parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | Yes |
| SecretKey | User SecretKey. We recommend you only use the SecretKey for frontend debugging to avoid key exposure | String | Yes |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: 3 (a request will be made 4 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using `uploadFiles`, if the file size is greater than the value of this parameter (measured in bytes), multipart upload is used; otherwise, simple upload is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10485760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | Protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when the `getService` method is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | Custom request domain name used to call a bucket or object API. <br>You can use a template such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region information passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. If the maximum is exceeded, failed, completed, and canceled tasks will be cleared. Default value: 1000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of `Content-MD5` for file uploads, which calculates the MD5 checksum of the file request body and places it in the `Content-MD5` field of the header. Default value: false | Boolean | No |
| Timeout | Timeout period in milliseconds. Default value: 0, indicating no timeout period. | Number | No |
| KeepAlive              | Indicates that more than one request is sent over one TCP connection. Default value: `true`. This parameter is recommended for a large number of concurrent requests.   | Boolean   | No   |
| StrictSsl              | Strict verification of the HTTPS certificate. Default value: `true` | Boolean | No   |
| Proxy | Uses an HTTP proxy when making requests, such as: `http://127.0.0.1:8080` | String | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required | Function | No |


#### getAuthorization callback function descriptions (using method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting a temporary key | Object   |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as listed below:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |
| StartTime | Key acquisition start time measured in seconds, i.e., the timestamp of the key acquisition time, such as 1580000000. This parameter is used as the signature start time. Passing in this parameter can avoid signature expiration issues due to time deviation on the frontend | String |  No   |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | No |

#### getAuthorization callback function description (using method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object |
| - Method | Method of the current request | String |
| - Pathname | Request path used for signature calculation | String |
| - Key | Object key (object name), which is the unique identifier of the object in the bucket. For more information, please see [Object Overview](https://cloud.tencent.com/document/product/436/13324) | String |
| - Query | Query parameter object of the current request in the format of `{key: 'val'}` | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function |

Once the getAuthorization callback function is finished, it returns one of the following:
Format 1. An Authorization string.
Format 2. An object whose attributes are listed as follows:


| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback, and each time a temporary key is required, it will be returned to the instance by this callback for signature calculation within the instance during each request.

### Creating bucket

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### Querying bucket list

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading object

This API is used to upload small files. For large files, please use the multipart upload API. For more information, please see [Object Operations](https://cloud.tencent.com/document/product/436/36119).

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject',              /* Required */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream('./exampleobject'), // Uploading file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### Querying object list

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading object

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject',              /* Required */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

### Deleting object

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject'       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```
