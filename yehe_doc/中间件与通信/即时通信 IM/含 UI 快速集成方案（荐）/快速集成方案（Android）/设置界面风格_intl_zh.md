本文介绍如何设置界面风格（Android）。

## 设置会话列表
会话列表由标题区 TitleBarLayout 与列表区 ConversationListLayout 组成，每部分都提供了 UI 样式以及事件注册的接口可供修改。
![会话列表](https://qcloudimg.tencent-cloud.cn/raw/d4fa84742e49ed43faa33614f74dbe25.png)

### 设置标题样式

标题区除了本身作为 View 所具有的属性功能之外，还包含左、中、右三块区域，如下图所示：

![标题区结构](https://qcloudimg.tencent-cloud.cn/raw/a6f5e4e2d544041827b7936229a00215.png)

您可参见 [ITitleBarLayout](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICore/tuicore/src/main/java/com/tencent/qcloud/tuicore/component/interfaces/ITitleBarLayout.java) 进行自定义修改。
例如，在会话列表中，隐藏左边的 LeftGroup，设置中间的标题，隐藏右边的文本和图片按钮，代码如下：
（参见 [MainActivity](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/main/MainActivity.java) 中的实现）
```java
mainTitleBar.setTitle(getResources().getString(R.string.conversation_title), ITitleBarLayout.Position.MIDDLE);
mainTitleBar.getLeftGroup().setVisibility(View.GONE);
mainTitleBar.getRightGroup().setVisibility(View.VISIBLE);
mainTitleBar.setRightIcon(R.drawable.more_btn);
```
效果如下图所示：
![标题区效果](https://qcloudimg.tencent-cloud.cn/raw/a89a69445edd8d4a11503e6ab708e6cd.png)
另外，您也可以定制点击事件：

```java
Menu menu = new Menu(this, mainTitleBar);
mainTitleBar.setOnRightClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        if (menu == null) {
            return;
        }
        if (menu.isShowing()) {
            menu.hide();
        } else {
            menu.show();
        }
    }
});
```


### 设置会话列表样式

列表区的自定义 layout 继承自 RecyclerView，登录后 TUIKit 会根据用户名从 SDK 读取该用户的会话列表。
会话列表提供一些常用功能定制，例如，头像是否圆角、背景、字体大小、点击与长按事件等。示例代码如下：

```java
public static void customizeConversation(final ConversationLayout layout) {
    // 从 ConversationLayout 获取会话列表
    ConversationListLayout listLayout = layout.getConversationList();
    listLayout.setItemTopTextSize(16); // 设置 item 中 top 文字大小
    listLayout.setItemBottomTextSize(12);// 设置 item 中 bottom 文字大小
    listLayout.setItemDateTextSize(10);// 设置 item 中 timeline 文字大小
    listLayout.setItemAvatarRadius(5); // 设置 adapter item 头像圆角大小
    listLayout.disableItemUnreadDot(false);// 设置 item 是否不显示未读红点，默认显示
    // 长按弹出菜单
    listLayout.setOnItemLongClickListener(new ConversationListLayout.OnItemLongClickListener() {
        @Override
        public void OnItemLongClick(View view, int position, ConversationInfo conversationInfo) {
            startPopShow(view, position, conversationInfo);
        }
    });
}
```

更多详细信息请参见 [ConversationLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIConversation/tuiconversation/src/main/java/com/tencent/qcloud/tuikit/tuiconversation/setting/ConversationLayoutSetting.java)。


### 设置头像的风格样式

IM SDK 不做头像存储，需要集成者有头像存储接口获取头像 URL，这里 TUIKit 通过随机头像接口进行演示，如何设置头像。
首先您需要在个人资料页面中，上传头像图片，调用修改资料接口。

```java
V2TIMUserFullInfo v2TIMUserFullInfo = new V2TIMUserFullInfo();
// 头像
if (!TextUtils.isEmpty(mIconUrl)) {
    v2TIMUserFullInfo.setFaceUrl(mIconUrl);
}
V2TIMManager.getInstance().setSelfInfo(v2TIMUserFullInfo, new V2TIMCallback() {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess() {
    }
});
```
会话列表设置头像在 [ConversationCommonHolder.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIConversation/tuiconversation/src/main/java/com/tencent/qcloud/tuikit/tuiconversation/ui/view/ConversationCommonHolder.java) 中进行获取展示：
```java
conversationIconView.setConversation(conversation);
```

## 设置聊天窗口的样式
聊天窗口包含标题区 TitleBarLayout，用法与会话列表相同。除此之外，聊天窗口还包含三个区域，从上到下为通知区 NoticeLayout、消息区 MessageRecyclerView 和输入区 InputView，如下图所示：
![聊天界面含更多功能](https://qcloudimg.tencent-cloud.cn/raw/3f32af89097f69fd0c5961e5fdf8ee0c.png)
```java
/**
 * 获取聊天窗口 Input 区域 Layout
 *
 * @return
 */
InputView getInputLayout();
/**
 * 获取聊天窗口 Message 区域 Layout
 *
 * @return
 */
MessageRecyclerView getMessageLayout();

/**
 * 获取聊天窗口 Notice 区域 Layout
 *
 * @return
 */
NoticeLayout getNoticeLayout();
```

更多详细信息请参见 [ChatLayoutSetting.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/setting/ChatLayoutSetting.java)。


### 设置通知区域 NoticeLayout 样式

通知区域由两个 TextView 组成，如下图所示：
![通知区域组成](https://main.qcloudimg.com/raw/1a34baf21414ffe9671a31a7223c6377.png)
效果如下图所示：
![通知效果图](https://qcloudimg.tencent-cloud.cn/raw/86738ac0ff0706f902bfe0db7704db93.png)

```java
// 从 ChatView 获取 NoticeLayout
NoticeLayout noticeLayout = layout.getNoticeLayout();
// 可以使通知区域一致展示
noticeLayout.alwaysShow(true);
// 设置通知主题
noticeLayout.getContent().setText("现在插播一条广告");
// 设置通知提醒文字
noticeLayout.getContentExtra().setText("参看有奖");
// 设置通知的点击事件
noticeLayout.setOnNoticeClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("赏白银五千两");
    }
});
```

### 设置消息区域 MessageRecyclerView 样式

MessageRecyclerView 继承自 RecyclerView ，本文提供自定义修改聊天背景、气泡、文字、是否显示昵称等常见的用法，更多详情请参见 [IMessageProperties.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/ui/interfaces/IMessageProperties.java)。

![消息区域](https://qcloudimg.tencent-cloud.cn/raw/d73552bed43fc4686961ba179bc28ebf.png)

#### 设置聊天窗口的背景色
您可以自定义设置聊天背景。
![更换聊天背景](https://qcloudimg.tencent-cloud.cn/raw/2283b16e6d26db2b16a6a330ac5bd46e.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// 设置聊天背景 //////
messageRecyclerView.setBackground(new ColorDrawable(0xB0E2FF00));
```

#### 设置发送者的头像样式
TUIKit 的界面在显示用户时，会从用户资料中读取头像地址并显示。
![换头像](https://qcloudimg.tencent-cloud.cn/raw/8694f81d7ea4f7dd1232f3e2fd40cae4.png)

```java
// 聊天界面设置头像
if (!TextUtils.isEmpty(msg.getFaceUrl())) {
    List<Object> urllist = new ArrayList<>();
    urllist.add(msg.getFaceUrl());
    if (isForwardMode) {
        leftUserIcon.setIconUrls(urllist);
    } else {
        if (msg.isSelf()) {
            rightUserIcon.setIconUrls(urllist);
        } else {
            leftUserIcon.setIconUrls(urllist);
        }
    }
} else {
    rightUserIcon.setIconUrls(null);
    leftUserIcon.setIconUrls(null);
}
```
如果用户没有设置头像会显示默认头像，您可以自定义设置默认头像、头像是否圆角以及头像大小等。
```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// 设置聊天背景 //////
messageRecyclerView.setBackground(new ColorDrawable(0xFFEFE5D4));
////// 设置头像 //////
// 设置默认头像，默认与朋友与自己的头像相同
messageRecyclerView.setAvatar(R.drawable.ic_more_file);
// 设置头像圆角
messageRecyclerView.setAvatarRadius(50);
// 设置头像大小
messageRecyclerView.setAvatarSize(new int[]{48, 48});
```


#### 设置气泡的背景色
左边为对方的气泡，右边为自己的气泡，您可以自定义设置双方的气泡背景。

![换气泡](https://qcloudimg.tencent-cloud.cn/raw/74152a0169277db622b4f30f177247ea.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// 设置自己聊天气泡的背景
messageRecyclerView.setRightBubble(context.getResources().getDrawable(R.drawable.chat_opposite_bg));
// 设置朋友聊天气泡的背景
messageRecyclerView.setLeftBubble(context.getResources().getDrawable(R.drawable.chat_self_bg));
```


#### 设置发送者的昵称样式
您可以自定义设置昵称的字体大小与颜色等，但双方昵称样式必须保持一致。

![换昵称](https://qcloudimg.tencent-cloud.cn/raw/95b55e1ae2151c8f9ff8e8af11e90a9a.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
////// 设置昵称样式（对方与自己的样式保持一致）//////
messageRecyclerView.setNameFontSize(12);
messageRecyclerView.setNameFontColor(0x8B5A2B00);
```


#### 设置聊天内容样式
您可以自定义设置聊天内容的字体大小、双方字体颜色等，但双方字体大小必须保持一致。

![换聊天内容](https://qcloudimg.tencent-cloud.cn/raw/a50755f23cde5ca63513e8ba4efb79a2.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// 设置聊天内容字体大小，朋友和自己用一种字体大小
messageRecyclerView.setChatContextFontSize(15);
// 设置自己聊天内容字体颜色
messageRecyclerView.setRightChatContentFontColor(0xA9A9A900);
// 设置朋友聊天内容字体颜色
messageRecyclerView.setLeftChatContentFontColor(0xA020F000);
```

#### 设置聊天时间线样式

您可以自定义设置聊天时间线的背景、字体大小以及字体颜色等。

![换时间线](https://qcloudimg.tencent-cloud.cn/raw/ea16f4e4c878f36893500a039b07de11.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// 设置聊天时间线的背景
messageRecyclerView.setChatTimeBubble(new ColorDrawable(0x8B691400));
// 设置聊天时间的字体大小
messageRecyclerView.setChatTimeFontSize(20);
// 设置聊天时间的字体颜色
messageRecyclerView.setChatTimeFontColor(0xEE00EE00);
```


#### 设置聊天的提示信息样式

您可以自定义设置提示信息的背景、字体大小以及字体颜色等。

![换提示消息](https://qcloudimg.tencent-cloud.cn/raw/f744a094b6c4975da9170a25ba550d61.png)

```java
// 从 ChatView 获取 MessageRecyclerView
MessageRecyclerView messageRecyclerView = layout.getMessageLayout();
// 设置提示的背景
messageRecyclerView.setTipsMessageBubble(new ColorDrawable(0xA020F000));
// 设置提示的字体大小
messageRecyclerView.setTipsMessageFontSize(20);
// 设置提示的字体颜色
messageRecyclerView.setTipsMessageFontColor(0x7CFC0000);
```


### 设置输入区域 InputView
输入区域 InputView，包含语音输入、文字输入、表情输入以及更多的“+”输入。

![输入区域](https://qcloudimg.tencent-cloud.cn/raw/53abac7901a717b6a58f2903339dfe0e.png)

#### 隐藏不要的功能

您可以自定义隐藏或展示更多“+”面板的图片、拍照、摄像以及发送文件的功能。

```java
// 从 ChatView 获取 InputLayout
InputView inputView = layout.getInputLayout();
// 隐藏拍照并发送
inputView.disableCaptureAction(true);
// 隐藏发送文件
inputView.disableSendFileAction(true);
// 隐藏发送图片
inputView.disableSendPhotoAction(true);
// 隐藏摄像并发送
inputView.disableVideoRecordAction(true);
```

#### 增加自定义的功能
您可以自定义新增更多“+”面板的动作单元实现相应的功能。

本文以隐藏发送文件，增加一个动作单元且该动作单元会发送一条消息为例，示例代码如下：

```java
// 从 ChatView 获取 InputView
InputView inputView = layout.getInputLayout();
// 隐藏发送文件
inputView.disableSendFileAction(true);
// 定义一个动作单元
InputMoreActionUnit unit = new InputMoreActionUnit();
unit.setIconResId(R.drawable.default_user_icon); // 设置单元的图标
unit.setTitleId(R.string.profile); // 设置单元的文字标题
unit.setOnClickListener(unit.new OnActionClickListener() { // 定义点击事件
    @Override
    public void onClick() {
        ToastUtil.toastShortMessage("自定义的更多功能");
        MessageInfo info = MessageInfoUtil.buildTextMessage("我是谁");
        layout.sendMessage(info, false);
    }
});
// 把定义好的单元增加到更多面板
inputView.addAction(unit);
```

#### 替换点击“+”的事件
您可以自定义替换更多“+”面板的各个动作单元的功能。

![替换事件](https://qcloudimg.tencent-cloud.cn/raw/75df00e962c34a845dbd3de0007303ca.png)

```java
// 从 ChatView 获取 InputView
InputView inputView = layout.getInputLayout();
// 可以用自定义的事件来替换更多功能的入口
inputView.replaceMoreInput(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        ToastUtil.toastShortMessage("自定义的更多功能按钮事件");
        MessageInfo info = MessageInfoUtil.buildTextMessage("自定义的消息");
        layout.sendMessage(info, false);
    }
});
```


#### 替换点击“+”弹出的面板
您可以自定义更多“+”面板的样式、各个动作单元以及其对应的功能。

```java
// 从 ChatView 获取 InputView
InputView inputView = layout.getInputLayout();
// 可以用自定义的 fragment 来替换更多功能
inputView.replaceMoreInput(new CustomInputFragment());
```

新面板 CustomInputFragment 的实现和普通的 Fragment 没有区别，在 onCreateView 时 inflate 自己的 View ，设置事件即可。本文以添加两个按钮 ，点击时弹出 toast 为例，示例代码如下：

```java
public static class CustomInputFragment extends BaseInputFragment {
    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, Bundle savedInstanceState) {
        View baseView = inflater.inflate(R.layout.test_chat_input_custom_fragment, container, false);
        Button btn1 = baseView.findViewById(R.id.test_send_message_btn1);
        btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ToastUtil.toastShortMessage("发送一条超链接消息");
            }
        });
        Button btn2 = baseView.findViewById(R.id.test_send_message_btn2);
        btn2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ToastUtil.toastShortMessage("发送一条视频文字混合消息");
            }
        });
        return baseView;
    }
}
```


