Player Adapter for Android is a player plugin provided by VOD for customers who want to use a third-party or proprietary player to connect to Tencent Cloud PaaS resources. It is generally used by customers who strongly need to customize player features.



## SDK Download

The Player Adapter SDK and demo for Android can be downloaded [here](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.2.0/TXCPlayerAdapterSDK_1.2.0_Android.zip). 

## Integration Guide

### Integrating the SDK

Integrate the SDK, copy `TXCPlayerAdapter-release-1.0.0.aar` to the `libs` directory, and add dependencies:

```groovy
implementation(name:'TXCPlayerAdapter-release-1.0.0', ext:'aar')
```

Add the script for obfuscation:

```xml
-keep class com.tencent.** { *;}
```

### Using the Player

Declare the variables and then create an instance. The main class of the player is `ITXCPlayerAssistor`, and videos can be played back after it is created.

A `fileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `fileId` to the client.
2. When the video is uploaded to the server, the corresponding `fileId` will be included in the notification of upload confirmation.

If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) and find it. After clicking it, you can view relevant parameters in the video details on the right.

```java
// `psign` is a player signature. For more information on the signature and how to generate it, visit https://cloud.tencent.com/document/product/266/42436.
private String mFileId, mPSign;
ITXCPlayerAssistor mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

Initialization:

```java
// Initialize the component
TXCPlayerAdapter.init(appId); // `appid` can be applied for in Tencent Cloud VOD
TXCPlayerAdapter.setLogEnable(true); // Enable log

mSuperPlayerView = findViewById(R.id.sv_videoplayer);  
mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

Request the video information and play back the video:

```java
mPlayerAssistor.requestVideoInfo(new ITXCRequestVideoInfoCallback() {

    @Override
    public void onError(int errCode, String msg) {
        Log.d(TAG, "onError msg = " + msg);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Toast.makeText(VideoActivity.this, "onError msg = " + msg, Toast.LENGTH_SHORT).show();
            }
        });
    }

    @Override
    public void onSuccess() {
        Log.d(TAG, "onSuccess");
        TXCStreamingInfo streamingInfo = mPlayerAssistor.getStreamingInfo();
        Log.d(TAG, "streamingInfo = " + streamingInfo);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mPlayerAssistor.getStreamingInfo() != null) {
                    // Play back the video
                    mSuperPlayerView.play(mPlayerAssistor.getStreamingInfo().playUrl);
                } else {
                    Toast.makeText(VideoActivity.this, "streamInfo = null", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
});
```

Terminate the player after use

```java
TXCPlayerAdapter.destroy();
```



## SDK API Description

### Initializing TXCPlayerAdatper

This API is used to initialize Adapter each time.

**API**

```java
TXCPlayerAdapter.init(String appId);
```

**Parameter description**

appId: Enter the `appid` (if a subapplication is used, enter the `subappid`). |



### Terminating TXCPlayerAdatper

This API is used to terminate Adapter. It can be called after the program exits.

**API**

```java
TXCPlayerAdapter.destroy();
```



### Creating the Player auxiliary class

An auxiliary class of the player can be used to get the playback `fileId` and process DRM encryption APIs.

**API**

```java
ITXCPlayerAssistor playerAssistor = TXCPlayerAdapter.createPlayerAssistor(String fileId, String pSign);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------- |
| fileId    | String                | The `fileId` of the video to be played. back.                               |
| pSign  | String | The player signature.      |



### Terminating the Player auxiliary class

This API is used to terminate an auxiliary class. You can call it when exiting the player or switching to the next video for playback.

**API**

```
TXCPlayerAdapter.destroyPlayerAssistor(ITXCPlayerAssistor assistor);
```



### Requesting video playback information

This API is used to request the stream information of the video to be played back from the Tencent Cloud VOD server.

**API**

```java
playerAssistor.requestVideoInfo(ITXCRequestVideoInfoCallback callback);
```

**Parameter description**

| Parameter | Type | Description |
| -------- | ---------------------------- | ------------ |
| callback | ITXCRequestVideoInfoCallback | Async callback function. |



### Getting the basic video information

This API is used to get the video information and will take effect only after `playerAssistor.requestPlayInfo` is called back.

**API**

```java
TXCVideoBasicInfo playerAssistor.getVideoBasicInfo();
```

**Parameter description**

The parameters of `TXCVideoBasicInfo` are as follows:

| Parameter | Type | Description |
| ----------- | ------ | ------------------ |
| name        | String | The video name.           |
| duration | Float | The video duration in seconds. |
| description | String | The video description.           |
| coverUrl    | String | The video thumbnail.           |

### Getting video stream information

This API is used to get the video stream information list and will take effect only after `playerAssistor.requestPlayInfo` is called back.

**API**

```java
TXCStreamingInfo playerAssistor.getStreamimgInfo();
```

**Parameter description**

TXCStreamingInfo

| Parameter | Type | Description |
| ---------- | ------ | ---------------------------------------------------------- |
| playUrl | String | The playback URL. |
| subStreams | List   | The adaptive bitrate substream information of the [SubStreamInfo](#SubStreamInfo) type. |

The parameters of `SubStreamInfo` are as follows:[](id:SubStreamInfo)

| Parameter | Type | Description |
| -------------- | ------ | ------------------------------------ |
| type | String | Substream type. Valid values: `video` |
| width | Int | The substream video width in px. |
| height | Int | The substream video height in px. |
| resolutionName | String | The specification name of the substream video displayed in the player. |

### Getting keyframe timestamp information

This API is used to get the video keyframe timestamp information and will take effect only after `playerAssistor.requestPlayInfo` is called back.

**API**

```java
List<TXCKeyFrameDescInfo> playerAssistor.getKeyFrameDescInfo();
```

**Parameter description**

The parameters of `TXCKeyFrameDescInfo` are as follows:

| Parameter | Type | Description |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | "Beginning now..." |



### Getting thumbnail information

This API is used to get the thumbnail information and will take effect only after `playerAssistor.requestPlayInfo` is called back.

**API**

```java
TXCImageSpriteInfo playerAssistor.getImageSpriteInfo();
```

**Parameter description**

The parameters of `TCXImageSpriteInfo` are as follows:

| Parameter | Type | Description |
| --------- | ------ | ---------------------------------- |
| imageUrls | List | Array of thumbnail download URLs of `String` type. |
| webVttUrl | String | Thumbnail VTT file download URL. |