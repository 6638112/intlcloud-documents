TUIKit 组件在 4.8.50 版本之后基于 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 实现了单聊和群组的视频通话和语音通话功能， 并且实现了 iOS 和 Android 平台的互通，参考本文您只需要简单几步就可以快速集成。
<table style="text-align:center;vertical-align:middle;width: 400px">
  <tr>
    <th style="text-align:center;" width="180px"><b>视频通话<br></b></th>
    <th style="text-align:center;" width="180px"><b>语音通话</b><br></th>
  </tr>
  <tr>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/59713f77fc8e0dbe4787288aba0898f7.jpeg"  />    </td>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/c865abcf5d4cccdfddb0bc152525e4d9.png" />     </td>
	 </tr>
</table>

>!
>- TUIKit 4.8.50 之后的版本音视频通话直接集成在 TUIKit 组件中，并且基于新的信令方案设计。
>- TUIKit 4.8.50 之前的版本音视频通话集成在 iOS 端的 TUIKitDemo 示例中，**新老版本不互通，如果您已经使用之前版本的音视频通话，这里不建议升级，以免出现兼容性问题**。

<span id="Step1"></span>
## 步骤1：开通音视频服务
1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片，进入应用的基础配置页面。
2. 单击【开通腾讯实时音视频服务】区域的【立即开通】。
3. 在弹出的开通实时音视频 TRTC 服务对话框中，单击【确认】。
 系统将为您在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 创建一个与当前 IM 应用相同 SDKAppID 的实时音视频应用，二者帐号与鉴权可复用。

<span id="Step2"></span>
## 步骤2：配置工程文件

1. 在 podfile 文件中添加以下内容。
 ```
// 支持音视频通话 TUIKit 的最低版本为 4.8.50
pod 'TXIMSDK_TUIKit_iOS'                 // 默认集成了 TXLiteAVSDK_TRTC 音视频库
// pod 'TXIMSDK_TUIKit_iOS_Professional' // 默认集成了 TXLiteAVSDK_Professional 音视频库
 ```
2. 执行以下命令，下载第三方库至当前工程。
```
pod install
```


<span id="Step3"></span>
## 步骤3：初始化 TUIKit 
初始化 TUIKit 需要传入 [步骤1](#Step1) 生成的 SDKAppID。
```
[[TUIKit sharedInstance] setupWithAppId:SDKAppID];
```

<span id="Step4"></span>
## 步骤4：登录 TUIKit
登录 IM 需要通过 TUIKit 提供的 `login` 接口，其中 UserSig 生成的具体操作请参见 [如何计算 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。
```
[[TUIKit sharedInstance] login:@"userID" userSig:@"userSig" succ:^{
     NSLog(@"-----> 登录成功");
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> 登录失败");
}];
```

<span id="Step5"></span>
## 步骤5：发起视频或语音通话

<img style="width:180px" src="https://main.qcloudimg.com/raw/17698afaedf9ba86045c03ef85159bec.png"  /> 

当用户点击聊天界面的视频通话或则语音通话时，TUIKit 会自动展示通话邀请 UI，并给对方发起通话邀请请求。

## 步骤6：接受视频或语音通话

<table style="text-align:center;vertical-align:middle;width: 400px">
  <tr>
    <th style="text-align:center;" width="180px"><b>接受视频通话<br></b></th>
    <th style="text-align:center;" width="180px"><b>接受语音通话</b><br></th>
  </tr>
  <tr>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/d4f0d5c7f208932055588c1ac59b9a91.jpg"  />    </td>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/a621580a0553271c70a9fec0738400c5.jpg" />     </td>
	 </tr>
</table>

- 当用户**在线**收到通话邀请时，TUIKit 会自动展示通话接收 UI，用户可以选择同意或则拒绝通话。
- 当用户**离线**收到通话邀请时，是没法感知的，通话邀请目前暂不支持离线推送能力。

## 常见问题
### 1. 若已分别创建实时音视频 SDKAppID 和即时通信 SDKAppID，现需要同时集成 IM SDK 和 TRTC SDK，需要注意什么?

若已分别创建实时音视频 SDKAppID 和即时通信 SDKAppID，即 SDKAppID 不一致场景，则二者帐号与鉴权不可复用，您需要生成实时音视频 SDKAppID 对应的 UserSig 进行鉴权。生成 UserSig 的具体操作请参见 [如何计算 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。

获取实时音视频的 SDKAppID 和 UserSig 后，您需要在 `TRTCCall+Room.swift` 源码中修改以下代码：
```
 func enterRoom() {
	 let param = TRTCParams()
	 // 音视频的 SDKAppID
	 param.sdkAppId = 1000000000 
	 // 音视频 SDKAppID 生成的 UserSig
	 param.userSig = "userSig"
  }
```


### 2. 通话邀请的超时时间默认是多久？怎么修改默认超时时间？
通话邀请的默认超时时间是30s，您可以修改 `TRTCCall.swift` 里的 `timeOut` 字段来自定义超时时间。

### 3. 在邀请超时时间内，被邀请者如果离线再上线，能否收到邀请？
- 如果是单聊通话邀请，被邀请者离线再上线可以收到通话邀请。
- 如果是群聊通话邀请，被邀请者离线再上线不能收到通话邀请。
