本文主要介绍如何快速地将腾讯云 TRTC Web SDK 集成到您的项目中。

## 支持的平台

WebRTC 技术由 Google 最先提出， Chrome 、Edge 、 Firefox、Safari 、Opera浏览器等均已支持，腾讯云TRTC Web SDK基于WebRTC封装，腾讯云 TRTC Web SDK 详细支持度表格请参见 [支持的平台](https://intl.cloud.tencent.com/document/product/647/41664)。
- 如果您的应用场景主要为教育场景，那么教师端推荐使用稳定性更好的 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 解决方案，支持大小双路画面，更灵活的屏幕分享方案以及更强大的弱网络恢复能力。




> ! 
> - 您可以在浏览器中打开 [TRTC Web SDK 能力测试页面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 检测当前浏览器是否支持 WebRTC 所有能力。例如 WebView 等浏览器环境。
> - 由于 H.264 版权限制，华为 Chrome 88 以下版本，无法使用 H264 编码（即无法推流）。如果您希望在华为设备 Chrome 浏览器中，使用 TRTC Web SDK 推流，请[提交工单](https://console.cloud.tencent.com/workorder/category )申请开通 VP8 编解码。

## URL 域名协议限制
| 应用场景     | 协议             | 接收（播放） | 发送（上麦） | 屏幕分享 | 备注 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 生产环境     | HTTPS 协议        | 支持         | 支持         | 支持     | 推荐 |
| 生产环境     | HTTP 协议         | 支持         | 不支持       | 不支持   |      |
| 本地开发环境 | http://localhost | 支持         | 支持         | 支持     | 推荐 |
| 本地开发环境 | http://127.0.0.1 | 支持         | 支持         | 支持     |      |
| 本地开发环境 | http://[本机IP]  | 支持         | 不支持       | 不支持   |      |
| 本地开发环境 | file:///         | 支持         | 支持         | 支持     |      |

## 防火墙限制
在使用 TRTC Web SDK 时，用户可能因防火墙限制导致无法正常进行音视频通话，请参考 [应对防火墙限制相关](https://www.tencentcloud.com/document/product/647/35164) 将相应端口及域名添加至防火墙白名单中。

## 集成 TRTC Web SDK

### NPM 集成

1. 您需要在项目中使用 npm 安装 SDK 包。
```
npm install trtc-js-sdk --save
```
2. 在项目脚本里引入模块。
```javascript
import TRTC from 'trtc-js-sdk';
```

### Script 集成

您只需要在您的 Web 页面中添加如下代码即可：

```html
<script src="trtc.js"></script>
```

## 相关资源

SDK 下载地址：[单击下载](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip) 。

更详细的初始化流程和 API 使用介绍请参见以下指引：

| 功能                       | Sample Code 指引                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 基础音视频通话 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html) |
| 互动直播 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html) |
| 切换摄像头和麦克风 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html) |
| 设置本地视频属性 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html) |
| 动态关闭打开本地音频或视频 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html) |
| 屏幕分享 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html) |
| 音量大小检测 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html) |
| 自定义采集与自定义播放渲染 | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| 房间内上行用户个数限制     | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html) |
| 背景音乐和音效实现方案     | [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html) |
| 通话前环境与设备检测| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 通话前的网络质量检测| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| 检测设备插拔行为| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| 实现推流到 CDN| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| 开启大小流传输| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 开启美颜| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| 开启水印| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| 实现跨房连麦| [指引链接](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |

>? [单击查看](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html) 更多能力。
