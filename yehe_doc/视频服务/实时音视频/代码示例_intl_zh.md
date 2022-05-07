<style>
    .card-container {
        width: 293px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: center;
    }

    .scene-card-container {
        width: 450px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .scene-card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
    }

    .markdown-text-box img {
        box-shadow: none;
    }


    h3 {
        position: relative;
        top: -2px;
    }
		
		@media (max-width: 768px){
				.card-container,
				.scene-card-container{
						width: 100%;
				}
				.scene-card > div{
						width: 100%!important;
						margin-left: 0!important;
				}
				img {
        box-shadow: none;
    }
		}
</style>

## API 示例
<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS API 示例</h3>
                <p>演示如何使用 RTC iOS API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Android API 示例</h3>
                <p>演示如何使用 RTC Android API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                <h3>Windows API 示例</h3>
                <p>演示如何使用 RTC Windows API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/Live_Mac/tree/main/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                <h3>Mac OS API 示例</h3>
                <p>演示如何使用 RTC Mac OS API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Web/tree/main/base-react-next" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web API 示例</h3>
                <p>演示如何使用 RTC Web API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API 示例</h3>
                <p>演示如何使用 RTC Electron API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>
    <a href="https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/index.html" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web 在线 API Examples</h3>
                <p>在线体验 Web API 实现的音视频功能，简单快捷</p>
            </div>
        </div>
    </a>
    <span target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API 快速体验</h3>
                <p style="color:#586376;">
                    下载安装包，支持应用内编辑代码：
                    <a href="https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-windows.zip" download>Windows版</a> &nbsp;&nbsp;&nbsp;
                    <a href="https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-mac.zip" download>Mac版</a>
                </p>
            </div>
        </div>
    </span>
    <a href="https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/a63fddf5902b311356966d44419098db.svg" data-nonescope="true">
                <h3>Flutter API 示例</h3>
                <p>演示如何使用 RTC Flutter API <br>从零开始搭建音视频应用</p>
            </div>
        </div>
    </a>	
</div>

## 场景方案
### 社交娱乐
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/82cfd639a13f1f65cf18c0415bfb37c4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">互动直播</h3>
                <p style="color:#586376;" ;>低代码快速实现视频互动直播场景，如：秀场，电商，赛事</p>
                <a href="https://github.com/tencentyun/TUILiveRoom">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">接入文档</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/bee791cf7cdccf175b70918f83115c7f.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">语音沙龙</h3>
                <p style="color:#586376" ;>组件化 UI 助您低代码快速实现语音沙龙场景</p>
                <a href="https://github.com/tencentyun/TUIChatSalon">GitHub 源码</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/80a7a3e917e4e65908bf2fb1736f7121.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">语音聊天室</h3>
                <p style="color:#586376;" ;>组件化 UI 助您低代码快速实现语音聊天室场景</p>
                <a href="https://github.com/tencentyun/TUIVoiceRoom">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37287">接入文档</a>
            </div>
        </div>
    </div>
		<div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/4651627d75d0e712d8032fb5f6149a3d.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">在线 K 歌</h3>
                <p style="color:#586376;" ;>组件化 UI 助您低代码快速实现在线 KTV 场景</p>
                <a href="https://github.com/tencentyun/TUIKaraoke">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/41940">接入文档</a>
            </div>
        </div>
    </div>
</div>

### 教育
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/1b60d290134f2a93e04dcb453c3dd51f.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">互动课堂</h3>
                <p style="color:#586376" ;>Electron 跨平台组件帮您快速搞定教育课堂</p>
                <a
                    href="https://github.com/TencentCloud/trtc-education-electron">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37278">接入文档</a>
            </div>
        </div>
    </div>
</div>

### 通信
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/c8b92d2457467e3c349cb56e83b37ef4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">多人音视频房间</h3>
                <p style="color:#586376" ;>组件化 UI 助您低代码快速实现音视频房间场景</p>
                <a href="https://github.com/tencentyun/TUIMeeting">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37284">接入文档</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/2dffabbe27521eb08c95dc5e72101886.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">语音通话</h3>
                <p style="color:#586376" ;>组件化 UI 帮助您快速实现一个“类微信”等语音通话场景</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36067">接入文档</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/96f08d55e04928ddd1d731192a3dc8a4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">视频通话</h3>
                <p style="color:#586376" ;>组件化 UI 帮助您快速实现一个“类微信”等视频通话场景</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub 源码</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36065">接入文档</a>
            </div>
        </div>
    </div>
</div>
</div>
