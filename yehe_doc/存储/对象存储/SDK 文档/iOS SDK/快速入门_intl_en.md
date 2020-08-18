## Relevant Resources

- Download the iOS SDK source code [here](https://github.com/tencentyun/qcloud-sdk-ios.git).
- Access the demo [here](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the SDK APIs and their parameters, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

## Preparations

1. Prepare an iOS application; this can be an existing project or a new empty project.
2. Make sure that the application is built using an SDK running on iOS 8.0 or above.
3. Prepare a remote address that can be used to get your Tencent Cloud temporary key. For more information on temporary keys, please see [Practice of Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Integration using CocoaPods (recommended)

#### Standard SDK

Add the following content to the `Podfile` of your project:

```shell
pod 'QCloudCOSXML'
```

#### Disabling MTA reporting

We have introduced Tencent Mobile Analytics (TMA) capabilities into the SDK to keep track of and optimize SDK quality for a better user experience.

If you want to disable this feature, add the following content to the `Podfile` file of your project

```shell
pod 'QCloudCOSXML/WithoutMTA'
```

#### Simplified SDK

If you only need to perform upload and download operations and want a smaller sized SDK, you can use the simplified version, which does not contain the MTA feature.

The simplified SDK is implemented through the CocoaPods subspec feature, so it currently can only be integrated automatically. Add the following content to the `Podfile` of your project:

```shell
pod 'QCloudCOSXML/Transfer'
```

### Method 2. Manual integration

You can directly download the latest version of the SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip) or you can find all of the versions [here](https://github.com/tencentyun/qcloud-sdk-ios/releases).

#### 1. Import binary libraries

Drag **`QCloudCOSXML.framework`, `QCloudCore.framework`, and `libmtasdk.a`** to your project.

![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  

Add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### 2. Configure your project

Set "Other Linker Flags" in "Build Settings" and add the following parameters:

```shell
-ObjC
-all_load
```

![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

## Step 3. Begin Using the SDK

### 1. Import the header file

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXML.h>
```

**swift**

```swift
import QCloudCOSXML
```

For the simplified SDK, import the following:

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
```

**swift**

```swift
import QCloudCOSXMLTransfer
```

### 2. Create a COS instance

#### Method 1. Obtaining a temporary key pair to authenticate requests (recommended)

We recommend using `AppDelegate` for the initialization process. You need to implement the following two protocols:

- QCloudSignatureProvider
- QCloudCredentailFenceQueueDelegate

We provide a `QCloudCredentailFenceQueue` scaffolding tool for you to cache and reuse your temporary key.

We recommend designing the COS instances `QCloudCOSXMLService` and `QCloudCOSTransferMangerService` as **application singletons**.

Please see the following complete sample code:

**Objective-c**

```objective-c
//AppDelegate.m
// `AppDelegate` must follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

@interface AppDelegate()<QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate>

// Scaffolding tool instance
@property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    // Service region abbreviation; for example, `ap-guangzhou` is the abbreviation for the Guangzhou region
    endpoint.regionName = @"COS_REGION";
    // Use HTTPS
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // You are the key provider
    configuration.signatureProvider = self;
    // Initialize the COS instances
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];

    // Initialize the temporary key scaffolding tool
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;

    return YES;
}

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    // Get the temporary key from the backend server synchronously
    //...

    QCloudCredential* credential = [QCloudCredential new];
    // Temporary key's `SecretId`
    credential.secretID = @"COS_SECRETID";
    // Temporary key's `SecretKey`
    credential.secretKey = @"COS_SECRETKEY";
    // Temporary key's `Token`
    credential.token = @"COS_TOKEN";
    // We strongly recommend using the server time as the start time of the signature
    // to avoid signature errors caused by a deviation between your mobile phone's local time and standard time
    credential.startDate = [[[NSDateFormatter alloc] init] 
        dateFromString:@"startTime"]; // Unit: second
    credential.experationDate = [[[NSDateFormatter alloc] init] 
        dateFromString:@"expiredTime"];

    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

// Getting the signature: Here you can see how to get the temporary key and calculate the signature
// You can also customize the signature calculation process
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, 
        NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);
        }
    }];
}


@end
```

**Swift**

```swift
//AppDelegate.swift
// `AppDelegate` must follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate {

    var credentialFenceQueue:QCloudCredentailFenceQueue?;

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();
        // Service region abbreviation; for example, `ap-guangzhou` is the abbreviation for the Guangzhou region
        endpoint.regionName = "COS_REGION";
        // Use HTTPS
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // You are the key provider
        config.signatureProvider = self;

        // Initialize the COS instances
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);

        // Initialize the temporary key scaffolding tool
        self.credentialFenceQueue = QCloudCredentailFenceQueue.init();
        self.credentialFenceQueue?.delegate = self;

        return true
    }

    func fenceQueue(_ queue: QCloudCredentailFenceQueue!, 
        requestCreatorWithContinue continueBlock: 
        QCloudCredentailFenceQueueContinue!) {
        // Get the temporary key from the backend server synchronously
        //...

        let credential = QCloudCredential.init();
        // Temporary key's `SecretId`
        credential.secretID = "COS_SECRETID";
        // Temporary key's `SecretKey`
        credential.secretKey = "COS_SECRETKEY";
        // Temporary key's `Token`
        credential.token = "COS_TOKEN";
        // We strongly recommend using the server time as the start time of the signature
        // to avoid signature errors caused by a deviation between your mobile phone's local time and standard time
        credential.startDate = DateFormatter().date(from: "startTime");
        // Here, the value is measured in seconds
        credential.experationDate = DateFormatter().date(from: "expiredTime");

        let auth = QCloudAuthentationV5Creator.init(credential: credential);
        continueBlock(auth,nil);
    }

    // Getting the signature: Here you can see how to get the temporary key and calculate the signature
    // You can also customize the signature calculation process
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        self.credentialFenceQueue?.performAction({ (creator, error) in
            if error != nil {
                continueBlock(nil,error!);
            }else{
                let signature = creator?.signature(forData: urlRequst);
                continueBlock(signature,nil);
            }
        })
    }
}
```

>!
>- For the abbreviations of different bucket regions, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
>- We recommend requesting data over HTTPS. However, if you want to use HTTP protocol, you need to enable HTTP transfer for your application so that it can run on iOS 9.0 or above. For detailed directions, please see Apple's official documentation [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing_insecure_network_connections).

If your `QCloudServiceConfiguration` has changed, you can register a new instance by using the following method:

```objective-c
+ (QCloudCOSTransferMangerService*) registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key;
```

#### Method 2. Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to switch to the temporary key method before launching your application.**

When using a permanent key, you can choose not to implement the `QCloudCredentailFenceQueueDelegate` protocol.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID"; // Permanent key's `SecretId`
    credential.secretKey = @"COS_SECRETKEY"; // Permanent key's `SecretKey`

    // Use the permanent key to calculate the signature
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] 
        initWithCredential:credential];
    QCloudSignature* signature = [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let credential = QCloudCredential.init();
    credential.secretID = "COS_SECRETID"; // Permanent key's `SecretId`
    credential.secretKey = "COS_SECRETKEY"; // Permanent key's `SecretKey`

    // Use the permanent key to calculate the signature
    let auth = QCloudAuthentationV5Creator.init(credential: credential);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

#### Method 3. Using a backend-calculated signature to authenticate requests

When the signature is generated on the backend, you can choose not to implement `QCloudCredentailFenceQueueDelegate` protocol

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    // Signature expiration time
    NSDate *expiration = [[[NSDateFormatter alloc] init] 
                            dateFromString:@"expiredTime"];
    QCloudSignature *sign = [[QCloudSignature alloc] initWithSignature:
        @"Signature calculated on backend" expiration:expiration];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    // Signature expiration time
    let expiration = DateFormatter().date(from: "expiredTime");
    let sign = QCloudSignature.init(signature: "signature calculated on backend", 
                expiration: expiration);
    continueBlock(signature,nil);
}
```

## Step 4. Access COS

### Uploading object

The SDK allows you to upload local files and binary data in NSData format. The following uses local file upload as an example:

**Objective-C**

```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// Local file path
NSURL* url = [NSURL fileURLWithPath:@"file URL"];
// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body =  url;
// Monitor the upload progress
[put setSendProcessBlock:^(int64_t bytesSent,
                            int64_t totalBytesSent,
                            int64_t totalBytesExpectedToSend) {
    //      bytesSent                   Number of new bytes sent
    //      totalBytesSent              Total number of bytes sent in the upload
    //      totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
}];

// Monitor the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

**Swift**

```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();
// Bucket name in the format: `BucketName-APPID`
put.bucket = "examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = "exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body = NSURL.fileURL(withPath: "Local File Path") as AnyObject;

// Monitor the upload result
put.setFinish { (result, error) in
    // Get the upload result
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    //      bytesSent                   Number of new bytes sent
    //      totalBytesSent              Total number of bytes sent in the upload
    //      totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
};
// Set the upload parameters
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData
    // and can generate a multipart upload request using resumeData.
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>
        .init(request: resumeData as Data?);
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

### Downloading object

**Objective-C**

```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `outputObject` of `finishBlock`.
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// Monitor the download result
[request setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// Monitor the download progress
[request setDownProcessBlock:^(int64_t bytesDownload,
                                int64_t totalBytesDownload,
                                int64_t totalBytesExpectedToDownload) {
    //      bytesDownload                   Number of new bytes downloaded 
    //      totalBytesDownload              Total number of bytes received in the download
    //      totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

**Swift**

```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
// Bucket containing the file
request.bucket = "examplebucket-1250000000";
// Object key
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `outputObject` of `finishBlock`.
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    //      bytesDownload                   Number of new bytes downloaded
    //      totalBytesDownload              Total number of bytes received in the download
    //      totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
}

// Monitor the download result
request.finishBlock = { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

