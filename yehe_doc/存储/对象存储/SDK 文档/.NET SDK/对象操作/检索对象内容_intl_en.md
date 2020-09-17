## Overview

This document provides an overview of the API and SDK code samples related to extracting object content.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object (in CSV or JSON format) |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Extracting Object Content

#### API description 

This API is used by the COS Select feature to extract objects in the following formats:

* CSV: an object is stored in CSV format with its data records separated with a specific delimiter.
* JSON: an object is stored in JSON format, which can be either a JSON file or a JSON list.

> !
>- To use COS Select, you must have the permission for `cos:GetObject`.
>- CSV- or JSON-formatted objects need to be encoded in UTF-8.
>- COS Select can extract CSV- or JSON-formatted objects compressed by gzip or bzip2.
>- COS Select can extract CSV- or JSON-formatted objects encrypted with SSE-COS.

#### Sample code

[//]: # ".cssg-snippet-select-object"
```cs
try
{
    string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
    string key = "exampleobject"; // Object key

    SelectObjectRequest request = new SelectObjectRequest(bucket, key);

    ObjectSelectionFormat.JSONFormat jSONFormat = new ObjectSelectionFormat.JSONFormat();
    jSONFormat.Type = "DOCUMENT";
    jSONFormat.RecordDelimiter = "\n";
    
    string outputFile = "select_local_file.json";

    request.setExpression("Select * from COSObject")
            .setInputFormat(new ObjectSelectionFormat(null, jSONFormat))
            .setOutputFormat(new ObjectSelectionFormat(null, jSONFormat))
            .SetCosProgressCallback(delegate (long progress, long total) {
                Console.WriteLine("OnProgress : " + progress + "," + total);
            })
            .outputToFile(outputFile)
            ;

    SelectObjectResult selectObjectResult =  cosXml.selectObject(request);
    Console.WriteLine(selectObjectResult.stat);
}
catch (COSXML.CosException.CosClientException clientEx)
{
    Console.WriteLine("CosClientException: " + clientEx.StackTrace);
    Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
    Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SelectObject.cs).

