## Overview

`TUIPusher` and `TUIPlayer` are our web-based open-source components for interactive live streaming (UI included). You can use them together with our basic SDKs such as [TRTC](https://intl.cloud.tencent.com/product/trtc) and [IM](https://intl.cloud.tencent.com/product/im) to quickly equip your live streaming applications (corporate live streaming, live shopping, vocational training, remote teaching, etc.) with web-based publishing and playback capabilities.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports only 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

Strengths:
+ A general-purpose live streaming solution with UI that includes common live streaming features such as device selection, beauty filters, publishing, playback, and live chat, helping you quickly bring your services to the market
+ Easy integration into Tencent Cloud’s basic SDKs, including TRTC, IM, and Superplayer, for excellent flexibility and scalability
+ Web-based, easy-to-use, and quick updates

![](https://qcloudimg.tencent-cloud.cn/raw/d1670385df8944886472e6c17d577949.png)

## Demos

We provide a [TUIPusher Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html) and a [TUIPlayer Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html), with user and room management systems, for you to experiment with the features of the components.
>! You need to log in with two different accounts to try `TUIPusher` and `TUIPlayer` at the same time. 

### `TUIPusher` features
- Capturing and publishing streams from camera and mic
  - Customizing video parameters including frame rate, resolution, and bitrate
  - Applying beauty filters and setting beauty filter parameters
- Capturing and publishing data from the screen
- Publishing to the TRTC backend and Tencent Cloud’s CDNs
- Text chatting with the anchor and other audience members
- Getting the audience list and muting audience members

### `TUIPlayer` features
- Playing the audio/video stream and screen sharing stream at the same time
- Text chatting with the anchor and other audience members
- Three playback options: Ultra-low-latency live streaming (300 ms latency), high-speed live streaming (latency within 1,000 ms), and standard live streaming (ultra-high concurrency)
- Supports desktop and mobile browsers and landscape mode on mobile devices

>! If your browser does not support WebRTC and can play videos only using standard live streaming protocols, please use a different browser to try WebRTC playback.

## Integration

### Step 1. Create an application

> !
>- `TUIPusher` and `TUIPlayer` are based on TRTC and IM. Make sure you use the same `SDKAppID` for your TRTC and IM applications so that they can share your account and authentication information.
>- You can use the basic content filtering capability of IM to filter text messages. If you want to customize restricted words, go to the IM console > **Content Filtering**, and click **Upgrade**.
>- Local `UserSig` calculation is for development and local debugging only and not for official launch. The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).


<dx-tabs>
::: Method 1: Via TRTC
[](id:step1)
#### Step 1. Create a TRTC application
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) and activate [TRTC](https://console.cloud.tencent.com/trtc) and [IM](https://console.cloud.tencent.com/im).
2. In the [TRTC console](https://console.cloud.tencent.com/trtc), click **Application Management > Create Application** to create an application.
![Create application](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)

#### Step 2. Get the TRTC key information
1. In the application list, find the application created and click **Application Info** to view the `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)
2. Select the **Quick Start** tab to view the application’s secret key.
![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)

<dx-alert infotype="explain">
<li>Accounts creating their first application in the TRTC console will get a 10,000-minute free trial package.</li>
<li>After you create a TRTC application, an IM application with the same `SDKAppID` will be created automatically. You can configure package information for the application in the [IM console](https://console.cloud.tencent.com/im).</li></dx-alert>

:::
::: Method 2: Via IM
#### Step 1. Create an IM application
1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**.
![](https://qcloudimg.tencent-cloud.cn/raw/f7497abca24a87c459d34cb849031541.png)
2. In the pop-up window, enter an application name and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/7bef16f8bfd19208eab6051d548d05e4.png)
3. Go to the [overview page](https://console.cloud.tencent.com/im) to view the status, edition, `SDKAppID`, creation time, and expiration time of the application created. Note down the `SDKAppID`.

#### Step 2. Obtain the key and activate TRTC
1. On the [overview page](https://console.cloud.tencent.com/im), click the application created to go to the **Basic Configuration** page. In the **Basic Information** section, click **Display key**, and copy and save the key.
![](https://qcloudimg.tencent-cloud.cn/raw/f211f03fdb78d548aba80fcdd67219a8.png)
<dx-alert infotype="notice">Please store the key information properly to prevent disclosure.</dx-alert>
2. On the **Basic Configuration** page, activate TRTC.
![](https://qcloudimg.tencent-cloud.cn/raw/a202eda15b427b9c24cd4290a79243a7.png)
:::
</dx-tabs>

[](id:step2)
### Step 2. Prepare your project

1. Download the code for `TUIPusher` and `TUIPlayer` at [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web).
2. Install dependencies for `TUIPusher` and `TUIPlayer`.
```bash
cd Web/TUIPusher
npm install

cd Web/TUIPlayer
npm install
```
3. Paste `SDKAppID` and the secret key to the specified locations below in the `TUIPusher/src/config/basic-info-config.js` and `TUIPlayer/src/config/basic-info-config.js` files.

4. Run `TUIPusher` and `TUIPlayer` in a local development environment.
```bash
cd Web/TUIPusher
npm run serve

cd Web/TUIPlayer
npm run serve
```
5. You can open `http://localhost:8080` and `http://localhost:8081` to try out the features of `TUIPusher` and `TUIPlayer`.
6. You can modify the room, anchor, and audience information in `TUIPusher/src/config/basic-info-config.js` and `TUIPlayer/src/config/basic-info-config.js`, but **make sure the room and anchor information is consistent in the two files**.

>!
>- You can now use `TUIPusher` and `TUIPlayer` for ultra-low-latency live streaming. If you want to support high-speed and standard live streaming too, see [Step 3. Enable relay to CDN](#step3).
>- Local calculation of `UserSig` is for development and local debugging only and not for official launch. If your `SECRETKEY` is leaked, attackers will be able to steal your Tencent Cloud traffic.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [Calculating UserSig on the server](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step3)
### Step 3. Enable relay to CDN

Because the high-speed and standard live streaming features of `TUIPusher` and `TUIPlayer` are powered by [CSS](https://intl.cloud.tencent.com/document/product/267), you need to enable relay to CDN to use these features.

1. In the [TRTC console](https://console.cloud.tencent.com/trtc), enable relay to CDN for your application. You can choose **Specified-stream relay** or **Global relay** based on your needs.  
![img](https://qcloudimg.tencent-cloud.cn/raw/2724d9ff0b4c23a30b37feaba6cccbcd.png)
2. On the [Domain Management](https://console.cloud.tencent.com/live/domainmanage) page, add your playback domain name. For detailed directions, please see [Adding Your Own Domain Names](https://intl.cloud.tencent.com/document/product/267/35970).
3. Configure the playback domain name in `TUIPlayer/src/config/basic-info-config.js`.

You can now use all features of `TUIPusher` and `TUIPlayer`, including ultra-low-latency live streaming, high-speed live streaming, and standard live streaming.

[](id:step4)
### Step 4. Apply in a production environment

To apply `TUIPusher` and `TUIPlayer` to a production environment, in addition to integrating them into your project, you also need to do the following:

- Create a user management system to manage user information such as user IDs, usernames, and profile pictures
- Create a room management system to manage room information such as room IDs, room names, and anchors
- Generate `UserSig` on your server
> !
>- In this document, `UserSig` is generated on the client based on the `SDKAppID` and secret key you provide. The secret key may be easily decompiled and reversed, and if your key is disclosed, attackers will be able to steal your traffic. Therefore, **this method is for local debugging only**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig during production?](https://intl.cloud.tencent.com/document/product/647/35166).
- Submit account information such as user information, room information, `SDKAppID`, and `UserSig` to `store` of `vuex` for global storage, as shown in `TUIPusher/src/pusher.vue` and `TUIPlayer/src/player.vue`. Then you will be able to use all publishing and playback features of the two components. The diagram below shows the workflow in detail:
![](https://qcloudimg.tencent-cloud.cn/raw/30e959d1b4605532f6d4cac190cdd1df.png)

## FAQs
### How do I use beauty filters on the web?
See [Enabling Beauty Filters](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html).

### How do I implement the screen sharing feature on the web?
See [Screen Sharing](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html).

### How do I implement the on-cloud recording feature on the web?
1. For information about how to enable **on-cloud recording**, see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).
2. If you enable **specified user recording**, you can start recording on the web by specifying `userDefineRecordId` when calling the [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient) API.
	
### How do I publish a stream to CDN on the web?
See [Publishing to CDN](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html).

### How do I enable high-speed playback on the web?
Publish streams to CDNs using the TRTC web SDK and play the streams over WebRTC.

## Notes
### Supported platforms

| Operating System | Browser                   | Required Version | TUIPlayer | TUIPusher | TUIPusher Screen Sharing           |
| :------- | :--------------------------- | :----------------- | :------------------------- | :-------- | :--------------------------- |
| macOS   | Safari         | 11+                | Supported      | Supported      | Supported (on Safari 13+)  |
| macOS   | Chrome         | 56+                | Supported      | Supported      | Supported (on Chrome 72+)  |
| macOS   | Firefox        | 56+                |Supported      | Supported      | Supported (on Firefox 66+) |
| macOS   | Edge           | 80+                | Supported                       | Supported      | Supported                         |
| macOS   | WeChat built-in browser           | -                  | Supported                       | Not supported    | Not supported                       |
| macOS   | WeCom built-in browser           | -                  | Supported                       | Not supported    | Not supported                       |
| Windows   | Chrome         | 56+                | Supported      | Supported      | Supported (on Chrome 72+)  |
| Windows  | QQ Browser (WebKit core) | 10.4+              | Supported                       | Supported      | Not supported                       |
| Windows   | Firefox        | 56+                |Supported      | Supported      | Supported (on Firefox 66+) |
| Windows  | Edge           | 80+                | Supported                       | Supported      | Supported                         |
| Windows   | WeChat built-in browser           | -                  | Supported                       | Not supported    | Not supported                       |
| Windows   | WeCom built-in browser           | -                  | Supported                       | Not supported    | Not supported                       |
| iOS      | WeChat built-in browser                | -                  | Supported                       | Not supported    | Not supported                       |
| iOS      | WeCom built-in browser                | -                  | Supported                       | Not supported    | Not supported                       |
| iOS      | Safari         | -                  | Supported                       | Not supported    | Not supported                       |
| iOS      | Chrome         | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | WeChat built-in browser               | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | WeCom built-in browser               | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | Chrome         | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | QQ Browser            | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | Firefox         | -                  | Supported                       | Not supported    | Not supported                       |
| Android  | UC Browser             | -                  | Supported (only standard live streaming) | Not supported    | Not supported                       |

### Domain requirements
For security and privacy reasons, only HTTPS URLs can access all features of `TUIPusher` and `TUIPlayer`. Therefore, please use the HTTPS protocol for the web page of your application in production environments.
>! You can use `http://localhost` for local development.

The table below lists the supported domain names and protocols.

| Scenario | Protocol | TUIPlayer | TUIPusher | TUIPusher Screen Sharing | Remarks |
| ------- | ------- | ------- | ------- | ------- | ------- |
| Production     | HTTPS        | Supported         | Supported         | Supported     | Recommended |
| Production     | HTTP         | Supported         | Not supported       | Not supported   |   -   |
| Local development | `http://localhost` | Supported         | Supported         | Supported     | Recommended |
| Development | `http://127.0.0.1` | Supported | Supported | Supported   | - |
| Local development | `http://[local IP address]`  | Supported         | Not supported       | Not supported   |   -   |

### Firewall configuration
Firewall restrictions may cause audio/video calls to fail. To avoid this, add the ports and domains specified in [Firewall Restrictions]( https://www.tencentcloud.com/document/product/647/35164) to the allowlist of your firewall.

## Summary
In future versions, we plan to add support for communication between the web components and TRTC native SDKs (such as the iOS SDK and Android SDK), as well as introduce features such as co-anchoring, advanced filters, custom layout, relaying to multiple platforms, and image/text/music upload.

If you have any requirements or feedback, contact colleenyu@tencent.com.

