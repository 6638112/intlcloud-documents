## Feature
Camera push refers to the process of collecting images from the camera of the mobile phone and voice from the microphone, encoding the video and audio data, and pushing the data to the livestreaming cloud platform. Tencent Cloud LiteAVSDK calls the V2TXLivePusher API to provide the camera push capability. The figure below shows the interfaces for camera push operations demonstrated in the LiteAVSDK demo.
![](https://main.qcloudimg.com/raw/f4df6e007076f4629629f5d75f14d86d.png)



## Notes

- **x86 simulator debugging**
The SDK uses a lot of audio and video APIs of the iOS system. These APIs often cannot be used on the x86 simulator that comes with the Mac server. Therefore, if conditions allow, we recommend that you use the real Mac server for debugging.

## Sample Code

| Platform | GitHub URL | Key Class |
|:---------:|:--------:|:---------:|
| iOS | [Github](https://github.com/tencentyun/LiteAVInternational) | CameraPushMainViewController.m |
| Android | [Github](https://github.com/tencentyun/LiteAVInternational) | CameraPusherActivity.java |


## Feature Interfacing

### 1. Download the SDK

[Download](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_International_iOS_lastest.zip) the SDK and follow the instructions in the [SDK integration guide](https://intl.cloud.tencent.com/document/product/1071/38155) to embed the SDK in your application project.

<span id="step2"></span>

### 2. Configure a license for the SDK
Click [Apply for a License](https://console.cloud.tencent.com/live/license) to obtain the license for testing. You will receive two strings. One is the license URL, and the other is the decryption key.

Before you call the LiteAVSDK features in your app, we recommend that you complete the following configurations in `- [AppDelegate application:didFinishLaunchingWithOptions:]`:

```objc
@import TXLiteAVSDK_Professional;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<Obtained license URL>";
    NSString * const licenceKey = @"<Obtained key>";
        
    //TXLiveBase is located in the "TXLiveBase.h" header file.
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

### 3. Initialize the V2TXLivePusher component
First, create a `V2TXLivePusher` instance. Later, this instance can be used to implement all the following push-related capabilities, including starting or stopping stream push, starting or stopping data collection from the camera, starting or stopping data collection from the microphone, starting or stopping headphone monitoring, setting the voice quality, and setting the image quality.

```objectivec    
 V2TXLivePusher *_pusher = [[V2TXLivePusher alloc] init];
 [_pusher setObserver:self];
```

### 4. Enable camera preview
You can call the `setRenderView` API in `V2TXLivePusher` to enable the camera preview for the mobile phone. You must provide a view object for previewing images for the `setRenderView` API.

```objectivec   
 // Create a view object and insert it into the current interface.
 UIView *localView = [[UIView alloc] initWithFrame:self.view.bounds];
 [self.view insertSubview:localView atIndex:0];
 localView.center = self.view.center;
 
 // Enable the local camera preview.
 [_pusher setRenderView:localView];
```

> ! To add the animation effect for a view, you must modify the `transform` attribute of the view, instead of the `frame` attribute.
```objectivec
  [UIView animateWithDuration:0.5 animations:^{
      _localView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
  }];
```

### 5. Start and stop stream push
If you have called the `setRenderView` API to enable camera preview, you can call the `startPush` API of V2TXLivePusher to start pushing streams.

```objectivec 
// Start pushing streams.
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream push.
[_pusher startPush:rtmpUrl];
[_pusher startCamera]; // Start collecting data from the camera.
[_pusher startMicrophone]; // Start collecting data from the microphone.
```

After you complete stream push, you can call the `stopPush` API of V2TXLivePusher to stop stream push.
```objectivec
// Stop pushing streams.
[_pusher setObserver:nil];
[_pusher stopCamera];
[_pusher stopMicrophone];
[_pusher stopPush];
```

-  **How can I obtain a valid push URL?**

After you activate the LVB service, you can choose LVB console > Auxiliary tools > [URL generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate a push URL. For more information, see [Push/Pull URL](https://intl.cloud.tencent.com/document/product/267/31059).
![](https://main.qcloudimg.com/raw/cf62d6a6e117bdb9a8d3ca68bf20a5c4.png)
- **Why is “V2TXLIVE_ERROR_INVALID_LICENSE” returned?**
If the `startPush` API returns “V2TXLIVE_ERROR_INVALID_LICENSE”, license verification has failed. In this case, check whether any problem occurred in [Step 2. Configure a license for the SDK](#step2).


### 6. Push pure audio streams
If you only need to push pure audio streams, perform the following operations:
```objectivec 
// Start pushing streams.
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream push.
[_pusher startPush:rtmpUrl];
[_pusher startMicrophone]; // Start collecting data from the microphone.
```

### 7. Set the video resolution
You can call the `setVideoQuality:resolutionMode:` API of V2TXLivePusher to set the video resolution, aspect ratio, and portrait or landscape mode for the audience.

```objectivec
// Select the portrait mode and set the aspect ratio to 1280x720. The first parameter is the video resolution, and the second parameter is the portrait or landscape mode.
[_pusher setVideoQuality:V2TXLiveVideoResolution_1280x720 resolutionMode:V2TXLiveVideoResolutionMode_Portrait];
```

### 8. Set the beauty filter, whitening, and rosy skin effects.
The beauty filter SDK’s TCBeautyPanel.framework can be introduced to pass in the `V2TXLivePusher ` instance and display the beauty panel (TCBeautyPanel) on the interface. This allows users to set diversified beauty effects.
```objectivec
NSUInteger controlHeight = [TCBeautyPanel getHeight];
CGRect frame = CGRectMake(0, 0, self.view.frame.size.width, controlHeight);
_beautyPanel = [TCBeautyPanel beautyPanelWithFrame:frame
                                         SDKObject:_livePusher];
[ThemeConfigurator configBeautyPanelTheme:_beautyPanel];
_beautyPanel.pituDelegate = self; // Proxy method that is used to set and implement the beauty filter effects.
[_beautyPanel resetAndApplyValues];

#pragma mark - BeautyLoadPituDelegate

- (void)onLoadPituStart {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showInProgressText:@"Start loading resources"];
    });
}

- (void)onLoadPituProgress:(CGFloat)progress {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showInProgressText:[NSString stringWithFormat:@"Loading resources %d %%",(int)(progress * 100)]];
    });
}

- (void)onLoadPituFinished {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showText:@"Successfully loaded resources"];
    });
}

- (void)onLoadPituFailed {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showText:@"Failed to load resources"];
    });
}
```


### 9. Control camera behaviors
V2TXLivePusher provides an API to obtain the video device manager, TXVideoDeviceManager, which is used to control camera behaviors.

| API Function | Description | Remarks |
|---------|---------|---------|
| switchCamera | Switch between the front and rear cameras. | The corresponding function on the Mac platform is `selectCamera`. |
| enableCameraFlash | Enable or disable the flash. | This function is valid only when the current camera is a rear camera. |
| setCameraZoomRatio | Adjust the zoom ratio. | The valid range of the zoom ratio is 1 - 5. Default: 1. |
| setCameraFocusPosition | Set the focus position. | To use this setting, enableCameraAutoFocus must be used to disable auto focus. |

### 10. Set the mirror effect on the audience side
You can call the `setEncoderMirror` API of V2TXLivePusher to set the mirror effect on the audience side. This mirror effect is different from that on the host side. When the host uses the front camera for livestreaming, the view seen by the host is inverted by the SDK by default. Therefore, the host’s display is like looking in a mirror. `setEncoderMirror` only affects the mirror effect on the audience side.


### 11. Set the audio quality
```objectivec
// Pay attention to the calling sequence:
[_pusher setAudioQuality: V2TXLiveAudioQuality_Music]; // You must set the audio quality before pushing streams. Otherwise, the audio quality setting does not take effect.
[_pusher startPush]; // 2
```

### 12. Set the logo watermark

You can call the `setWatermark:position:scale:` API of V2TXLivePusher to allow the SDK to add a watermark to the pushed video stream. The watermark position is determined by the `position` parameter.

- The SDK requires that the watermark image be in png format, instead of jpg, because the png format provides the transparency information and allows the SDK to better address the image aliasing issue. If a jpg image is modified in the Windows system, its extension does not take effect.
- `position` is the normalized coordinates of the watermark image relative to the resolution of the pushed video. If the resolution of the pushed video is 540 × 960, and `position` is set to (0.1, 0.1, 0.1, 0.0), the actual pixel coordinates of the watermark are: 540 × 0.1, 960 × 0.1, Watermark width × 0.1, Automatically calculated watermark height.

```objectivec
UIImage *image = value?[UIImage imageNamed:@"watermark"]:nil;
CGPoint pos = value?CGPointMake(10, 10):CGPointZero;
[_pusher setWatermark:image position:pos scale:1.0];
```

## Event Handling
### 1. Event listening

The SDK uses the `V2TXLivePusherObserver` proxy to set the pusher callback. By setting the callback, you can monitor some callback events of V2TXLivePusher, including the player status, volume callback, statistics, warnings, and error messages. 

### 2. Normal events 
The table below lists the events you will be notified of upon each successful push. If “0” is received, the related event is called successfully.

| Event ID | Value | Description |
| :-------------------  |:-------- |  :------------------------ |
| V2TXLIVE_OK           | 0 | Successfully called the push event. |

### 3. Error notifications 
The push cannot continue because the SDK detected a critical problem. For example, when the user revokes the camera permission for the app, the camera cannot be started.

| Event ID | Value | Description |
| :-------------------  |:-------- |  :------------------------ |
| V2TXLIVE_ERROR_FAILED                 | -1 | Failed. |
| V2TXLIVE_ERROR_INVALID_PARAMETER      | -2 | Invalid parameter. |
| V2TXLIVE_ERROR_REFUSED                | -3 | Refused. |
| V2TXLIVE_ERROR_NOT_SUPPORTED          | -4 | Not supported. |
| V2TXLIVE_ERROR_INVALID_LICENSE        | -5 | Invalid license. |

### 4. Warning events 
The SDK detects some warning events. These events can trigger tentative protection logic or restoration logic. Warnings can often be recovered from.

| Event ID | Value | Description |
| :-------------------  |:-------- |  :------------------------ |
| V2TXLIVE_WARNING_NETWORK_BUSY             |  1101 | Poor network connection. Data upload is blocked because the upstream bandwidth is too low. |
| V2TXLIVE_WARNING_VIDEO_BLOCK              |  2105 | Video lag occurs. |
| V2TXLIVE_WARNING_CAMERA_START_FAILED      | -1301 | Failed to start the camera. This can occur because the camera configuration program (driver) on a Windows or Mac device is abnormal. To solve this problem, disable and then enable the device again, restart the device, or update the configuration program. |
| V2TXLIVE_WARNING_CAMERA_OCCUPIED          | -1308 | Camera occupied. In this case, try to enable another camera. |
| V2TXLIVE_WARNING_CAMERA_NO_PERMISSION     | -1314 | No permission to access the camera. This error often occurs on a mobile device when the permission is revoked by the user. |
| V2TXLIVE_WARNING_MICROPHONE_START_FAILED  | -1302 | Failed to start the microphone. This can occur because the microphone configuration program (driver) on a Windows or Mac device is abnormal. To solve this problem, disable and then enable the device again, restart the device, or update the configuration program. |
| V2TXLIVE_WARNING_MICROPHONE_OCCUPIED      | -1319 | Microphone occupied. For example, if a mobile device has an ongoing call, the attempt to start the microphone will fail. |
| V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION | -1317 | No permission to access the microphone. This error often occurs on a mobile device when the permission is revoked by the user. |
