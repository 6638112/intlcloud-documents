本文针对音视频平台常见的长视频播放场景，推出播放器播放长视频教程。用户将掌握如何在 Web 端、iOS 端、Android 端播放器上播放视频，同时自动切换自适应码流、预览视频缩略图、添加视频打点信息。

## 学习目标
学习本阶段教程，您将掌握：
- 如何在云点播转出自适应码流（播放器能够根据当前带宽，动态选择最合适的码率播放）
- 如何在云点播设置视频打点信息
- 如何在云点播使用雪碧图做缩略图
- 如何使用播放器进行播放

阅读之前，请先确保已经学习播放器指引的 [阶段1：用播放器播放视频](https://intl.cloud.tencent.com/document/product/266/38098) 篇部分，了解云点播 fileid 的概念。

## 操作步骤
### 步骤1：转出自适应码流与雪碧图
本步骤，我们将指导您如何对视频转出自适应码流与雪碧图。
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod)，选择**视频处理设置**>**模板设置**>**转自适应码流模板**，单击**创建转自适应码流模板**。
![](https://qcloudimg.tencent-cloud.cn/raw/e941daca088dbf5ca8a40384fc3ade7f.png)
通过模板创建用户需要的自适应码流，本文创建一条名为 testAdaptive 的自适应码流模板，总共包含三条子流，分辨率分别为480p,720p和1080p。视频码率、视频帧率、音频码率则保持与原视频一致。
![](https://qcloudimg.tencent-cloud.cn/raw/21ee0dba1c79bde7bea922188d8f5b28.png)
2. 选择**视频处理设置**>**模板设置**>**截图模板**，单击**创建截图模板**。
![](https://qcloudimg.tencent-cloud.cn/raw/8bac06234f924cc2d9327b6e9791157d.png)
通过模板创建用户需要的雪碧图，本文创建一个名为 testSprite 的雪碧图模板，采样间隔为5%，小图行数：10，小图列数：10。
![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)
3. 通过任务流，添加自适应码流模板与雪碧图模板。
选择**视频处理设置**>**任务流设置**>**创建任务流**，单击**创建任务流**。
![](https://qcloudimg.tencent-cloud.cn/raw/bc6e4fcd4e53b050fa5f6d59d83608c8.png)
通过任务流，添加用户需要处理的任务，本文为展示播放自适应码流过程，创建了一条 testPlayVideo 的任务流，该任务流仅增加了自适应码流模板和雪碧图模板。
![](https://qcloudimg.tencent-cloud.cn/raw/29ebf8e33157e9c342848c8f1c54ce6d.png)
4. 选择**媒资管理**>**音视频管理**，勾选需要处理的视频，单击**视频处理**>**任务流**，选择任务流模板，发起任务。
![](https://qcloudimg.tencent-cloud.cn/raw/31392ed275f4406b73ceb2d3c866e3ad.png)
5. 至此，我们可以在**音视频管理**>**操作**>**管理**中，能够获取处理后的任务结果。

### 步骤2：增加视频打点信息
本步骤，我们将指导您新增的一组视频打点信息。
1. 进入云点播服务端 API 文档>**媒资管理相关接口**>[**修改媒体文件属性**](https://intl.cloud.tencent.com/document/product/266/37570),单击调试，进入云 API 控制台进行调试。
![](https://qcloudimg.tencent-cloud.cn/raw/69cc5e88d5858b25e6a21e59082c946a.png)
2. 通过参数名称 **AddKeyFrameDescs.N** 添加指定视频打点信息
![](https://qcloudimg.tencent-cloud.cn/raw/85eb2701162edf90c309d161af2bff99.png)
至此您已经完成了在云端上的操作，此时您在云点播已经转出自适应码流，视频雪碧图和添加了相关视频打点信息。

### 步骤3：播放器端集成
本步骤，我们将指导您在 Web 端、iOS 端、Android 端播放器播放自适应码流、添加缩略图与打点信息。

<dx-tabs>
::: Web 端
用户需要集成视立方播放器请参见 [集成指引](https://intl.cloud.tencent.com/document/product/266/33976)，引入播放器 SDK 文件之后，可以**媒资管理**提取上传媒资的 appId 和 fileId 进行播放。

播放器的构建方法为`TCPlayer`, 通过其创建播放器实例即可播放。

#### 1. 在 html 文件放置播放器容器

在需要展示播放器的页面位置加入播放器容器。例如，在 index.html 中加入如下代码（容器 ID 以及宽高都可以自定义）。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### 2. 使用 fileID 播放

在 index.html 页面初始化的代码中加入以下初始化脚本，传入获取到的 fileID 与 appID 即可播放。

```
var player = TCPlayer('player-container-id', { // player-container-id 为播放器容器 ID，必须与 html 中一致
    fileID: '5285890799710670616', // 请传入需要播放的视频 fileID（必须）
    appID: '1400329073' // 请传入点播账号的 appID（必须）
});
```

:::
::: iOS 端
用户需要集成视立方播放器请参见 [集成指引](https://intl.cloud.tencent.com/document/product/266/33976)，集成完后，可以**媒资管理**提取上传媒资的 appId 和 fileId 进行播放。

播放器主类为`SuperPlayerView`，创建后即可播放视频：

```xml
// 引入头文件
#import <SuperPlayer/SuperPlayer.h>

// 创建播放器  
_playerView = [[SuperPlayerView alloc] init];
// 设置代理，用于接受事件
_playerView.delegate = self;
// 设置父 View，_playerView 会被自动添加到 holderView 下面
_playerView.fatherView = self.holderView;
```

#### 使用 fileId 播放

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// 配置 AppId
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710670616"; // 配置 FileId
[_playerView playWithModel:model];
```
:::
::: Android 端
集成视立方播放器请参考[集成指引](https://intl.cloud.tencent.com/document/product/266/33975) ，集成完后，可以**媒资管理**提取上传媒资的 appId 和 fileId 进行播放。

播放器主类为`SuperPlayerView`，创建后即可播放视频：

#### 1. 在布局文件创建SuperPlayerView

```xml
<!-- 播放器-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. 使用 fileId 播放

```java
//在布局文件引入SuperPlayerView ，然后创建实例
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);
//不开防盗链
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// 配置 AppId
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // 配置 FileId
mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## 总结

至此，您就可以在播放器查看雪碧图预览、视频打点信息和自动切换动态自适应码流。更多功能请参见 [功能说明](https://intl.cloud.tencent.com/document/product/266/42965)。




