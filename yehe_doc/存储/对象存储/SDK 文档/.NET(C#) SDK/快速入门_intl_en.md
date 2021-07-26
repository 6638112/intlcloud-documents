## Resources

- Download the XML .NET SDK source code [here](https://github.com/tencentyun/qcloud-sdk-dotnet).
- Download XML .NET SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip).
- For the SDK APIs and their parameters, please see [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com).
- Find the complete code [here](https://github.com/tencentyun/cos-snippets/tree/master/dotnet).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
- For SDK FAQs, please see [.NET (C#) SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40773).


>? If you encounter errors such as non-existent functions or methods when using the SDK, please update the SDK to the latest version and try again.
>


## Step 1. Integrate the SDK

#### Environment dependencies

The .NET SDK is developed based on .NET Standard 2.0.

- For Windows users: Install .NET Core 2.0 or above or .NET Framework 4.6.1 or above. 
- For Linux/Mac users: Install .NET Core 2.0 or above.

#### Installing the SDK

You can install the SDK using NuGet by adding the following to the `csproj` file in your project:

```xml
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

If .NET CLI is used instead, run the following command:

```sh
dotnet add package Tencent.QCloud.Cos.Sdk
```

## Step 2. Initiate COS services

The section below describes how to perform basic COS operations with the .NET SDK, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object.


>? For the definition of terms such as SecretId, SecretKey, and Bucket, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>

Namespaces commonly used in this SDK include:

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

Before making any COS requests, always instantiate the following 3 objects: `CosXmlConfig`, `QCloudCredentialProvider`, and `CosXmlServer`.

- `CosXmlConfig` provides an API to configure the SDK.
- `QCloudCredentialProvider` provides an API to set the key information.
- `CosXmlServer` provides APIs for COS operations.

>? The initialization sample below uses a temporary key. For more information about how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

### 1. Initialize a COS service

```cs
// Initialize CosXmlConfig. 
string appid = "1250000000";// Set the APPID of your Tencent Cloud account.
string region = "COS_REGION"; // Set the default bucket region.
CosXmlConfig config = new CosXmlConfig.Builder()
  .IsHttps(true)  // Set HTTPS as default request method.
  .SetRegion(region)  // Set the default bucket region.
  .SetDebugLog(true)  // Display logs.
  .Build();  // Create a CosXmlConfig object.
```

### 2. Provide access credentials.

The SDK supports three types of access credentials: permanent keys, updated temporary keys, and unchanging temporary keys.

**Type 1: permanent key**

```cs
String secretId = "COS_SECRETID"; // “SecretId of your TencentCloud API key”
String secretKey = "COS_SECRETKEY"; // “SecretKey of your TencentCloud API key”
long durationSecond = 600;          // Validity period of each request signature in seconds
QCloudCredentialProvider cosCredentialProvider = new DefaultQCloudCredentialProvider(
  secretId, secretKey, durationSecond);
```

**Type 2: updated temporary key**

Since temporary keys are short term, you can obtain new ones using the following method:

```cs
public class CustomQCloudCredentialProvider : DefaultSessionQCloudCredentialProvider
{

  // Even if you do not already have a current temporary key, you can still use this method.
  public CustomQCloudCredentialProvider(): base(null, null, 0L, null) {
    ;
  }

  public override void Refresh()
  {
    //... First, request a temporary key from Tencent Cloud.
    String tmpSecretId = "COS_SECRETID"; // “SecretId of the temporary key”;
    String tmpSecretKey = "COS_SECRETKEY"; // “SecretKey of the temporary key”;
    string tmpToken = "COS_TOKEN"; // “Token of the temporary key”;
    long tmpStartTime = 1546860702;// Start time in seconds of the temporary key’s validity period
    long tmpExpireTime = 1546862502;// End time in seconds of the temporary key’s validity period
    // Call the API to update the key
    SetQCloudCredential(tmpSecretId, tmpSecretKey, 
      String.Format("{0};{1}", tmpStartTime, tmpExpiredTime), tmpToken);
  }
}

QCloudCredentialProvider cosCredentialProvider = new CustomQCloudCredentialProvider();
```

**Type 3: unchanging temporary key (not recommended)**

Note that your request may fail if you use an expired temporary key from a previous request.

```cs
String tmpSecretId = "COS_SECRETID"; // “SecretId of the temporary key”;
String tmpSecretKey = "COS_SECRETKEY"; // “SecretKey of the temporary key”;
string tmpToken = "COS_TOKEN"; // “Token of the temporary key”;
long tmpExpireTime = 1546862502;// End time in seconds of the temporary key’s validity period
QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(
  tmpSecretId, tmpSecretKey, tmpExpireTime, tmpToken);
```

### 3. Initialize CosXmlServer.

We recommend using `CosXmlConfig` and `QCloudCredentialProvider` to initialize the `CosXmlServer` service class as a **singleton** in your program.

```cs
CosXml cosXml = new CosXmlServer(config, cosCredentialProvider);
```

## Step 3. Access COS

### Creating a bucket
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  // Execute the request.
  PutBucketResult result = cosXml.PutBucket(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Querying a bucket list
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  // Execute the request
  GetServiceResult result = cosXml.GetService(request);
  // Get the list of all buckets.
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Uploading an object
```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // Identifies the location of the object in the bucket, i.e., the object key
String srcPath = @"temp-source-file";// Absolute path to the local file

// Upload an object.
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath);
uploadTask.SetSrcPath(srcPath);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = await 
    transferManager.UploadAsync(uploadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### Querying an object list

```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  // Execute the request.
  GetBucketResult result = cosXml.GetBucket(request);
  // Bucket information
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // The data is truncated, and the next marker of the data is recorded.
    this.nextMarker = info.nextMarker;
  }
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

### Downloading an object

```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally

// Download an object.
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
  localDir, localFileName);

downloadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
    transferManager.DownloadAsync(downloadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### Deleting an object

```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  // Execute the request.
  DeleteObjectResult result = cosXml.DeleteObject(request);
  // Request successful 
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```
