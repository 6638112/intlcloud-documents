## Relevant Resources

- Download the XML Android SDK source code [here](https://github.com/tencentyun/qcloud-sdk-android).
- Download the demo [here](https://github.com/tencentyun/qcloud-sdk-android-samples).
- For SDK APIs and parameters, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Android).
- For the SDK changelog, please see [ChangeLog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

## Preparations

1. You need an Android app, which can be one of your existing projects or a new one.
2. Make sure that your Android app’s target API level is 15 (Ice Cream Sandwich) or above.
3. Prepare a remote address that can be used to obtain your Tencent Cloud temporary key. For more information on temporary keys, please see [Implementing Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Automatic integration (recommended)

#### Standard SDK

Add dependencies to the app-level `build.gradle` file (usually under the app module).
```
dependencies {
	...
    // Add the following line
    implementation 'com.tencent.qcloud:cosxml:5.5.5'
}
```

If you are using Kotlin for development in your project, you can add our KTX extension package, which provides more user-friendly APIs.

```
dependencies {
	...
    // Add the following line
    implementation 'com.tencent.qcloud:cosxml-ktx:5.5.0'
}
```

#### Simplified SDK

If you use only the basic object features such as upload, download, and copy and have tight control over the packet size, you can use the simplified SDK.
>?To integrate the simplified SDK, replace `CosXmlService` with `CosXmlSimpleService`.

First, add the Bintray repository location to your project-level `build.gradle` file.

```
allprojects {
 repositories {
     ...
     // Add a Maven repository
     maven {
         url "https://dl.bintray.com/tencentqcloudterminal/maven"
     }
 }
}
```

Then, change the dependencies to `cosxml-lite` in the app-level `build.gradle` file (usually under the app module).

```
dependencies {
	...
    // Add the following line
    implementation 'com.tencent.qcloud:cosxml-lite:5.5.5'
}
```

#### Disabling MTA reporting

To provide better user experience, we have introduced Mobile Tencent Analytics (MTA) into the SDK to track down and optimize the SDK quality.

To disable the MTA feature, add the following statement to the app-level `build.gradle` file (usually under the app module):

```
dependencies {
	...
    implementation ('com.tencent.qcloud:cosxml:x.x.x'){
        // Add the following line
        exclude group:'com.tencent.qcloud', module: 'mtaUtils'
    }
}
```

### Method 2. Manual integration

#### 1. Download the SDK version

You can directly download the latest SDK version [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-android/latest/qcloud-sdk-android.zip) or find all versions at [SDK Releases](https://github.com/tencentyun/qcloud-sdk-android/releases).

After downloading and decompressing the file, you can see that it contains multiple `JAR` or `AAR` packages as described below. Please choose the ones you want to integrate.

Required libraries:

- cosxml: COS protocol implementation
- qcloud-foundation: foundation library
- [bolts-tasks](https://github.com/BoltsFramework/Bolts-Android): third-party task library
- [okhttp](https://github.com/square/okhttp): third-party networking library
- [okio](https://github.com/square/okio): third-party I/O library

Optional libraries:

- mtaUtils: MTA library for SDK improvement
- mid-sdk: MTA library for SDK improvement
- mta-android-sdk: MTA library for SDK improvement
- LogUtils: log module for SDK improvement
- quic: QUIC protocol, required if you transfer data over QUIC

#### 2. Integrate the SDK into your project

Put your libraries in the app-module `libs` folder and add dependencies to the app-level `build.gradle` file (usually under the app module):

```
dependencies {
	...
    // Add the following line
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
}
```

## Step 2. Configure Permissions

### Network permissions

The SDK needs network permission to communicate with the COS server. Please add the following permission declarations to `AndroidManifest.xml` under the app module:

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

### Storage permissions

If you need to read and write files from external storage, please add the following permission declarations to `AndroidManifest.xml` under the app module:

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

Note that for Android 6.0 (API level 23) or above, you need to dynamically request storage permissions at runtime.

## Step 3. Use the SDK

### 1. Obtain a temporary key

Implement a `BasicLifecycleCredentialProvider` subclass to request a temporary key and return the result.

```java
public static class MySessionCredentialProvider
        extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() 
            throws QCloudClientException {

        // First, obtain the response containing the key from your temporary key server

        // Then, parse the response to obtain the temporary key
        String tmpSecretId = "COS_SECRETID"; // SecretId of the temporary key
        String tmpSecretKey = "COS_SECRETKEY"; // SecretKey of the temporary key
        String sessionToken = "TOKEN"; // Token of the temporary key
        long expiredTime = 1556183496L;// End timestamp (in seconds) of the effective period of the temporary key

        // To avoid request expiration caused by the large discrepancy between the phone’s local time and the standard time, we recommend that the time returning to the server be used as the signature start time.
        // Time returning to the server as the signature start time
        long startTime = 1556182000L; // Start timestamp (in seconds) of the effective period of the temporary key

        // Finally, return the temporary key object
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey,
                sessionToken, startTime, expiredTime);
    }
}
```

The following takes `MySessionCredentialProvider` as the class name example to initialize an instance to provide a key for the SDK.

```java
QCloudCredentialProvider myCredentialProvider = new MySessionCredentialProvider();
```

#### Using a permanent key for local debugging

You can use a Tencent Cloud permanent key for local debugging during the development. **As this method may disclose your key, please change to the temporary key method before launching your application.**

```java
String secretId = "COS_SECRETID"; // SecretId of the permanent key
String secretKey = "COS_SECRETKEY"; // SecretKey of the permanent key

// keyDuration is the effective duration (in seconds) of the key in your request
QCloudCredentialProvider myCredentialProvider = 
    new ShortTimeCredentialProvider(secretId, secretKey, 300);
```

### 2. Initialize the COS service

Use your `myCredentialProvider` instance that provides the key to initialize a `CosXmlService` instance.

`CosXmlService` provides all APIs for accessing COS. We recommend you use it as an **application singleton**.

```java
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
String region = "COS_REGION";

// Create a `CosXmlServiceConfig` object and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use the HTTPS request. HTTP is used by default
        .builder();

// Initialize the COS service to obtain the instance
CosXmlService cosXmlService = new CosXmlService(context, 
    serviceConfig, myCredentialProvider);
```

>? For more information on the abbreviations of the COS bucket regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

#### Using the KTX package to initialize the COS service

If you use KTX, the simplified initialization code is as follows:

```kotlin
val cos = cosService(context = application.applicationContext) {

    configuration {
        setRegion("ap-guangzhou")
        isHttps(true)
    }

    credentialProvider {
        lifecycleCredentialProvider {
            // Fetch credential from backend
            // ...
            return@lifecycleCredentialProvider SessionQCloudCredentials(
                    "temp_secret_id",
                    "temp_secret_key",
                    "session_token",
                    1556183496
            )
        }
    }
}
```

## Step 4. Access COS

### Uploading an object

The SDK supports uploading local files, binary data, URIs, and input streams. The following uses uploading a local file as an example.

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, also known as the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of the local file
String uploadId = null; // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
String uploadId = null; 

// Upload a file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);

// Set the upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### Using the KTX package to upload an object

If you use KTX, please refer to the following sample code for the upload:

```kotlin
// Use the KTX extension of ViewModel
// viewModelScope is the built-in coroutine scope of ViewModel
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }
    // Local sample file
    val sourceFile = File(appContext.externalCacheDir, "sourceFile")

    try {
        // Call the "suspend" function for upload
        val result = `object`.upload(
            localFile = sourceFile,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "upload onProgress:" +
                                " $complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "upload state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Downloading an object

[//]: # (.cssg-snippet-transfer-download-object)
```java
// The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
// If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, also known as the object key
// Path of the local directory
String savePathDir = context.getExternalCacheDir().toString();
// File name saved locally. If not specified (null), it will be the same as the COS file name
String savedFileName = "exampleobject";

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext,
        bucket, cosPath, savePathDir, savedFileName);

// Set the download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback 
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### Using the KTX package to download an object

If you use KTX, please refer to the following sample code for the download:

```kotlin
// Use the KTX extension of ViewModel
// viewModelScope is the built-in coroutine scope of ViewModel
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }

    try {
        // Call the "suspend" function for download
        val result = `object`.download(
            context = appContext,
            destDirectory = appContext.externalCacheDir!!,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "download onProgress: " +
                        "$complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "download state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).
>- The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information. If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes `HeadObject`.
