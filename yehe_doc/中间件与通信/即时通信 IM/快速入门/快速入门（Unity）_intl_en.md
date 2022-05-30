This document describes how to quickly run the IM demo for Unity.

## Environment Requirements

| Platform | Version |
|---------|---------|
| Unity | 2019.4.15f1 or later |
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions


[](id:step1)
### Step 1. Create an IM app
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the provided service and all its data are lost. Please proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. Select **[Auxiliary Tools](https://console.cloud.tencent.com/im-detail/tool-usersig)** > **UserSig Generation and Verification** on the left sidebar. Create a `UserID` and the corresponding `UserSig`, and copy the signature information for use in [Step 5](#step5).
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### Step 2. Create a Unity project
Use Unity to create a project and record the project directory.

[](id:step3)
### Step 3. Modify the dependency file
1. Open the project with an IDE (such as Visual Studio Code):
![](https://qcloudimg.tencent-cloud.cn/raw/4ea52e320700dc37770a5405ac14d1a7.jpg)
2. Find Packages/manifest.json based on the directory, and modify dependencies as follows:
```json
{
	"dependencies":{
  "com.tencent.imsdk.unity":"https://github.com/TencentCloud/TIMSDK.git#unity" 
  }
}
```

[](id:step4)
### Step 4. Load dependencies
Open the project in the Unity Editor, wait until dependencies are loaded, and confirm the Tencent Cloud IM is successfully loaded.
![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

[](id:step5)
### Step 5. Test script
1. [Download the test script](https://github.com/TencentCloud/TIMSDK/blob/master/Unity/im_unity_sdk_plus/Assets/Demo/TestApi.cs), decompress the file, import the decompressed file to the project, and bind TestApi.cs to any scenario.
![](https://qcloudimg.tencent-cloud.cn/raw/b4d770775523fdd76b75f1d80f07c925.jpg)
2. Select and run the scenario, and enter the `SDKAppID`, `UserID`, and `UserSig` obtained in [Step 1](#step1) to start the test.
![](https://qcloudimg.tencent-cloud.cn/raw/940da8044cd80db27d08a7b0dff45b94.png)

## FAQs

### What platforms are supported?
iOS, Android, Windows, and macOS are supported.

### What should I do if clicking **Build And Run** for an Android device triggers an error, stating no available device is found?
Check that the device is not occupied by other resources. Alternatively, click **Build** to generate an APK package, drag it to the simulator, and run it.

### What should I do if an error occurs during the first run for an iOS device?
If an error is reported for an iOS device after the demo configured as above is run, choose **Product** > **Clean** to clean the product, and build the demo again. You can also close Xcode and open it again, and then build the demo again.
### What should I do if Unity v2019.04 on an iOS device reports the following error?
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Choose **Window** > **Package Manager** on the toolbar of the Editor and downgrade Unity Collaborate to 1.2.16.

### What should I do if Unity v2019.04 reports the following error for iOS?
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
Open the source code and delete the code snippet of `|| VersionControlSettings.mode != "Visible Meta Files"`.
