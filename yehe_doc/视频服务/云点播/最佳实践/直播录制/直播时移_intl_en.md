Time-shift playback in live streaming is based on live recording, live streaming time shifting, and VOD accelerated distribution. After a live streaming starts, a viewer can choose a previous time point other than the current time to start watching. This is commonly used to play back highlights in sport events. Users can change the progress bar to view contents generated earlier than the current time without waiting until the end of the live streaming. At the same time, the live streaming stays the same and users can switch back to the live streaming.

## Features
- Users can specify the time-shift duration allowed for playback (the difference between the playback start time and the current time)
- Users can specify the video streams with specific bitrates for time-shifting when the live stream is recorded in multiple bitrates.

## Prerequisites
- You have [signed up](https://intl.cloud.tencent.com/register) and [logged in to](https://intl.cloud.tencent.com/login) a Tencent Cloud account, and completed the identity verification. Unverified users cannot purchase instances of live streaming time shifting for Chinese mainland.
-  You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Notes:
- To use time-shift playback, you need first enable the [time shifting](#time) feature.
- The smallest time-shift duration is 90s, which means there is a latency of over 90s in the playback content compared with the live streaming content.
- Enabling time shifting will incur VOD traffic and storage fees. For more information, see [VOD Billing Overview](https://cloud.tencent.com/document/product/266/2838).

## Procedure
<span id="step1"></span>
### Step 1. Activate VOD service
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Activate Now**.
2. Check the checkbox to agree to the service agreement, and click **OK** to activate VOD service. Log in to the VOD console.

<span id="step2"></span>
### Step 2. Add domain name of the time-shift playback
To add the Tencent Cloud VOD domain name for time-shift playback, perform the following:
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and click **Distribution and Playback** > **Domain Name** in the left sidebar.
2. Click **Add Domain Name** and enter the VOD domain name. For more information, please see [Distribution and Playback Settings](https://intl.cloud.tencent.com/document/product/266/35572)
3. Configure the new domain CNAME.
<span id="step3"></span>
### Step 3. Bind recording template
1. Log in to the [CSS console](https://console.cloud.tencent.com/live/config/record) and click **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template** to create a recording template. For more information, please see [Recording Template Configuration](https://intl.cloud.tencent.com/document/product/267/34223).
>!
>- Select HLS as the file type.
>- Define the file storage duration, which should be no less than the [time-shift duration](#step4).
2. Bind the recording template with the push domain name to be configured. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).

<span id="step5"></span>
### Step 4. Activate the time shifting feature
You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1), select “CSS” and request to activate time shifting feature and provide the following parameters:
- VOD domain name for time-shift playback added in [Step 2](#step2).
- Recording template ID added in [Step 3](#step3). 
- Define time-shift duration `timeshift_dur` in seconds
>?
	>- Time-shift duration, which refers to the maximum time-shift duration (up to 7 days currently).
	>- The defined duration may not take accurately. We recommend that you adding a little buffer.
	>- Suppose the duration is configured as 7200 (2 hours), you will be able to request time-shifted contents generated less than 2 hours ago (`delay`, or the time-shift duration will range from 90 seconds to 2 hours). When any content generated more than 2 hours ago is requested, `HTTP 404` will be returned even if there is live streaming content.

## Playback Request
### Request URL format
```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### Parameters
| Parameter | Description |
|---------|---------|
| [Domain]       | The registered domain name of the time shifting feature, namely, the time-shift playback domain name you added to the VOD console.     |
| timeshift      | Fixed field which needs no modification                                           |
| [AppName]      | Application name. Suppose your application name is `live`, then enter `live`           |
| [StreamName]   | Stream name. You need fill in the stream name of your request                                 |
| timeshift.m3u8 | Fixed field which needs no modification                                           |
| delay           | The time-shift duration in seconds. This value is larger than or equals to 90. It will default back to 90 if the configured value is less than 90.|

### Sample
Suppose current time-shift domain name is `testtimeshift.com`, time-shift application name is `live` and the stream name is `SLPUrIFzGPE`. If you need to play back live content generated five minutes ago, the request URL should be: 

`http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300`
