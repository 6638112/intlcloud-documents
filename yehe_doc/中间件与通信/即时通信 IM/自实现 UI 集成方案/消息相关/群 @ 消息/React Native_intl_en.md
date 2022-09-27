## Feature Description

The sender listens for the characters in the input box. When the sender enters @, the group member selection UI will pop up. After the target group members are selected, the message will be displayed in the input box in the format of `"@A @B @C......"`, which can be further edited before sent.
In the group chat list of the receiver's conversation UI, the identifier `"someone@me"` or `"@all"` will be displayed to remind the user that the user was mentioned by someone in the group chat.

> ? Currently, only text @ messages are supported.

## Feature Demonstration

| Listening for the @ character for selection of group members | Editing and sending the group @ message | Receiving the group @ message |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| ![](https://qcloudimg.tencent-cloud.cn/raw/ed60cac72b215f6e7128cf2533bab2f7.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/fbabe9cac382a7944676565242b29b59.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/b20c30564c78b9fec9ab25260110641f.jpg) |

Figure 1: When the @ character is detected in the input box on the chat UI, the user is redirected to the group member selection UI to select the target group members.
Figure 2: After selecting the target group members, the user goes back to the chat UI to edit and send the group @ message.
Figure 3: If the user is mentioned, the user receives the conversation update, and the "someone@me" information is displayed in the conversation `Cell`.

## Sending a Group @ Message

1. The sender listens for the text input box on the chat UI and launches the group member selection UI. After group members are selected, the ID and nickname information of the members is called back. The ID is used to create the `V2TimMessage` object, while the nickname is to be displayed in the text box.
2. The sender calls the `createTextAtMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#createTextAtMessage)) to create a text @ message, get the `V2TIMMessage` object, and specify the target group members.
3. The sender calls the `sendMessage` API ([TS](https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#sendMessage)) to send the created @ message.

Below is the sample code:

```javascript
const text = "123";
const atUserList = ['user1','user2','all'];

// Create a group @ message
const atMsgRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(text, atUserList);
// Send the group @ message
TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(
          id: atMsgRes.data.id,
          receiver: "",
          groupID: "",
);
```

## Receiving a Group @ Message

1. When the conversation is loaded and updated, call the `groupAtInfolist` API ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimConversation.html#groupAtInfoList)) of `V2TimConversation` to get the @ data list of the conversation.
2. Call the `atType` API ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimGroupAtInfo.html#atType)) of the `V2TimGroupAtInfo` object in the list to get the @ data type and update it to the @ information of the conversation.

Below is the sample code:

```javascript
const nextSeq = "";
const count = 10;
const getConversationList = await TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .getConversationList(nextSeq, count);
if (getConversationList.code == 0) {
  getConversationList.data.conversationList.forEach((element) => {
    element.groupAtInfoList.forEach((element) => {
      if (element.atType == 0) {
        // @me
      }
      if (element.atType == 1) {
        // @all
      }
      if (element.atType == 2) {
        // @all and @me
      }
    });
  });
}
```


