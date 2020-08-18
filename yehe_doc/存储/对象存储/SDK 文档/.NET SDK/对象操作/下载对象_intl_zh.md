## 简介

本文档提供关于对象的下载操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 下载对象       | 下载一个对象至本地        |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 高级接口（推荐）

### 下载对象

高级接口支持暂停、恢复以及取消下载请求，同时支持断点下载功能。

#### 示例代码一: 下载对象

[//]: # (.cssg-snippet-transfer-download-object)
```cs
// 初始化 TransferConfig
TransferConfig transferConfig = new TransferConfig();

// 初始化 TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
String cosPath = "exampleobject"; //对象在存储桶中的位置标识符，即称对象键
string localDir = System.IO.Path.GetTempPath();//本地文件夹
string localFileName = "my-local-temp-file"; //指定本地保存的文件名

// 下载对象
 // COS_REGION 为存储桶所在地域
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, "COS_REGION", cosPath, 
  localDir, localFileName);

// 同步调用
var autoEvent = new AutoResetEvent(false);

downloadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};
downloadTask.successCallback = delegate (CosResult cosResult) 
{
    COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = cosResult 
      as COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult;
    Console.WriteLine(result.GetResultInfo());
    string eTag = result.eTag;
    autoEvent.Set();
};
downloadTask.failCallback = delegate (CosClientException clientEx, CosServerException serverEx) 
{
    if (clientEx != null)
    {
        Console.WriteLine("CosClientException: " + clientEx);
    }
    if (serverEx != null)
    {
        Console.WriteLine("CosServerException: " + serverEx.GetInfo());
    }
    autoEvent.Set();
};
transferManager.Download(downloadTask);
// 等待任务结束
autoEvent.WaitOne();
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs) 查看。

#### 示例代码二: 下载暂停、继续与取消

对于下载任务，可以通过以下方式暂停：

[//]: # (.cssg-snippet-transfer-download-object-pause)
```cs
downloadTask.Pause();
```

暂停之后，可以通过以下方式续传：

[//]: # (.cssg-snippet-transfer-download-object-resume)
```cs
downloadTask.Resume();
```

也通过以下方式取消下载：

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```cs
downloadTask.Cancel();
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs) 查看。

#### 示例代码三: 批量下载

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```cs
TransferConfig transferConfig = new TransferConfig();

// 初始化 TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
string localDir = System.IO.Path.GetTempPath();//本地文件夹

for (int i = 0; i < 5; i++) {
  // 下载对象
  string cosPath = "exampleobject" + i; //对象在存储桶中的位置标识符，即称对象键
  string localFileName = "my-local-temp-file"; //指定本地保存的文件名
  // COS_REGION 为存储桶所在地域
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, "COS_REGION", cosPath, 
    localDir, localFileName);
  transferManager.Download(downloadTask);
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs) 查看。

## 简单操作

### 下载对象

#### 功能说明

下载一个 Object（文件/对象）至本地（GET Object）。

#### 示例代码

[//]: # (.cssg-snippet-get-object)
```cs
try
{
  string bucket = "examplebucket-1250000000"; //存储桶，格式：BucketName-APPID
  string key = "exampleobject"; //对象键
  string localDir = System.IO.Path.GetTempPath();//本地文件夹
  string localFileName = "my-local-temp-file"; //指定本地保存的文件名
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  //设置签名有效时长
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  //设置进度回调
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //执行请求
  GetObjectResult result = cosXml.GetObject(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs) 查看。

