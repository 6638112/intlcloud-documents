## Overview

Mobile live streaming uses mainly the portrait mode, but TRTC supports both the landscape and portrait modes and therefore needs to implement different page orientation logics. This document describes:
- How to implement the portrait mode, for example, for video calls like those on WeChat;
- How to implement the landscape mode, for example, for video conferencing services such as Zoom;
- How to customize settings for the rotation degree and fill mode of the local image and remote images.

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## Supported Platforms

|   iOS    | Android  | macOS  | Windows  | Electron |  Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  × |


## Portrait Mode
To deliver experience similar to that of WeChat video calls, you need to do two things.

<span id="step1"></span>
### 1. Set the page orientation of your app to the portrait mode.
### iOS
Set the page orientation in Xcode > **General** > **Deployment Info** > **Device Orientation**.
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

Alternatively, use the `supportedInterfaceOrientationsForWindow` method in `Appdelegate`.

```
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
```
>? This [CSDN article](https://blog.csdn.net/DreamcoffeeZS/article/details/79037207) offers a detailed guide on page orientation and adaptation on iOS for developers.

#### Android
Set the `screenOrientation` attribute of the activity element to `portrait`:
```
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
```

<span id="step2"></span>
### 2. Set the resolution mode of the SDK to portrait.
When you use the `setVideoEncoderParam` API of `TRTCCloud` to set video encoding parameters, set `resMode` to `TRTCVideoResolutionModePortrait`.
<span id="example_code"></span>
Below is the sample code.
#### iOS
```
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; // Set the resolution mode to portrait.

[trtc setVideoEncoderParam: encParam];
```
#### Android
```
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT; //Set the resolution mode to portrait.
trtc.setVideoEncoderParam(encParams);
```

## Landscape Mode
The steps to implement the landscape mode for your app are similar to the steps of implementing the portrait mode, except that different values are used for the parameters in step 1 and step 2.
In particular, regarding the value of `resMode` in `TRTCVideoEncParam` in [step 2](#step2),
- on iOS, set it to `TRTCVideoResolutionModeLandscape`.
- on Android, set it to `TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE`.

## Custom Settings

The TRTC SDK provides a wide range of API functions for the setting of the rotation degree and fill mode of the local image and remote images.

| API Function | Setting | Note |
|---------|---------| ----- |
| setLocalViewRotation | The clockwise rotation degree of the local image preview | Valid values: 90 degrees, 180 degrees, 270 degrees |
| setLocalViewFillMode | The fill mode of the local image preview | Depending on the setting, the image may be cropped or may have black bars. |
| setRemoteViewRotation | The clockwise rotation degree of remote video images | Valid values: 90 degrees, 180 degrees, 270 degrees |
| setRemoteViewFillMode | The fill mode of remote video images | Depending on the setting, the image may be cropped or may have black bars. |
| setVideoEncoderRotation | The clockwise rotation degree of encoded images | Valid values: 90 degrees, 180 degrees, 270 degrees |

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
Given that page orientation involves adaptation during video recording and CDN relayed live streaming, the TRTC SDK provides a simple gravity-sensing adaptation feature, which you can enable using the `setGSensorMode` API of `TRTCCloud`.

Currently, the feature supports only 180-degree adaptive rotation. This means that when a user's phone is turned 180 degrees, the orientation of the user’s image seen by remote users remains the same, but this does not work when the phone is turned 90 degrees or 270 degrees. Since the feature is achieved through encoder-based rotation adjustment, adaptive rotation is also possible for recorded videos and videos played via HTML5 players.

> ! Another way to achieve adaptive rotation is embedding the gravity direction of a video in the information of each video frame, and adjusting the rotation degree of the video at the viewer end. This scheme requires the introduction of additional transcoding resources to adjust the orientation of recorded videos as expected and is therefore not recommended.
