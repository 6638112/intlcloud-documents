### 自己发送的消息 `Message.nick` 和 `Message.avatar` 都是空的，该怎么处理才能在界面上正常展示昵称和头像？

可以通过调用 [getMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMyProfile) 获取自己的昵称和头像。

### 如何在直播群中实现禁言功能？

可以将禁言功能通过自定义消息实现，自定义消息中需包含被禁言者的 Members_Account 与禁言时间，通过 [群内发言之前回调](https://intl.cloud.tencent.com/document/product/1047/34374) 将该自定义消息抄送至业务后台，业务后台调用 [批量禁言和取消禁言](https://intl.cloud.tencent.com/document/product/1047/34951) 接口即可实现针对指定用户的禁言功能。

### 如何在直播群中实现踢人功能？

可以将踢人功能通过自定义消息实现，自定义消息中需包含被踢者的 Members_Account，通过将该消息优先级设置为 High 避免因40条/秒消息限频后被后台抛弃，被踢者的 SDK 收到该消息后，调用 [退出群组](https://intl.cloud.tencent.com/document/product/1047/36169) 接口即可在直播群中实现踢人功能。

### 为什么会丢消息？

出现丢消息的可能原因如下：

- 直播群有40条/秒的频率限制，可通过消息发送前回调与消息发送后回调进行判断，若丢失的消息有收到消息发送前回调，未收到消息发送后回调，则该消息被限频。
- 可参考 [常见问题](#p4)，判断是否因为小程序/Web 端退出时，导致 Android/iOS/PC 同步退出。
- 如果是小程序/Web 出现问题，请确认您使用的 SDK 版本是否早于V2.7.6，如果是，请升级最新版。

如果您已排除以上可能性，您可以提交工单联系我们。

### 如何实现点赞/关注数量统计？

先通过自定义消息构建点赞/关注消息类型，当用户在前端点击点赞/关注 icon 触发自定义消息下发后，将点赞/关注消息通过 [群内发言之前回调](https://intl.cloud.tencent.com/document/product/1047/34374) 抄送到业务侧，业务侧根据收到的点赞/关注消息数进行数量统计，每3秒 - 5秒可通过 [修改群基础资料接口](https://intl.cloud.tencent.com/document/product/1047/34962) 将该数据更新进群资料字段中，SDK 通过 [拉取群资料接口](https://intl.cloud.tencent.com/document/product/1047/36169) 即可实现点赞/关注数量统计。

### 如何设置消息优先级更为合理？

为避免重要消息被抛弃，直播间针对所有消息提供3种优先级选择，SDK 获取消息时将会优先获取高优先级消息，针对自定义消息优先级设置建议如下：

- High：红包、礼物、踢人消息。
- Normal：普通文本消息。
- Low：点赞、关注消息。

### 有没有开源的直播组件，可以直接看视频和聊天互动？

有的，且代码开源，详情请参考 [腾讯云 Web 直播互动组件](https://github.com/tencentyun/TWebLive)。
