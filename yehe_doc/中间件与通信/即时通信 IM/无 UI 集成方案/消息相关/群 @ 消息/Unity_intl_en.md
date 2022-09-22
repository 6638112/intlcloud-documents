## Feature Description
The sender listens for the characters in the input box. When the sender enters @, the group member selection UI will pop up. After the target group members are selected, the message will be displayed in the input box in the format of `"@A @B @C......"`, which can be further edited before sent.
In the group chat list of the receiver's conversation UI, the identifier `"someone@me"` or `"@all"` will be displayed to remind the user that the user was mentioned by someone in the group chat.

> ? Currently, only text @ messages are supported.

## Feature Demonstration

| Listening for the @ character for group member selection                 | Editing and sending the group @ message                                  | Receiving the group @ message                                            |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| ![](https://qcloudimg.tencent-cloud.cn/raw/ed60cac72b215f6e7128cf2533bab2f7.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/fbabe9cac382a7944676565242b29b59.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/b20c30564c78b9fec9ab25260110641f.jpg) |

Figure 1: When the @ character is detected in the input box on the chat UI, the user is redirected to the group member selection UI to select the target group members.
Figure 2: After selecting the target group members, the user goes back to the chat UI to edit and send the group @ message.
Figure 3: If a user is mentioned, the user receives the conversation update, and the "someone@me" information is displayed in the conversation `Cell`.

## Sending a Group @ Message

1. The sender listens for the text input box on the chat UI and launches the group member selection UI. After group members are selected, the ID and nickname information of the members is called back. The ID is used to create the `Message` object, while the nickname is to be displayed in the text box.
2. The sender calls the `MsgSendMessage` API ([c#](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) to create a text @ message, create the `Message` message object, specify the target group members, and send the message object.

Sample code:


```c#
// Create a group @ message
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{new Elem
   {
     elem_type = TIMElemType.kTIMElem_Text,
     text_elem_content = Input.text
   }},
   message_group_at_user_array = userid_list, // List of `UserID` values of users to be mentioned (@) in the group message. To @all, pass in the `kImSDK_MesssageAtALL` field.
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // Async message sending result
});
```



## Receiving a Group @ Message

1. When the conversation is loaded and updated, call the `conv_group_at_info_array` API ([c#](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html#convgroupatinfoarray)) of `ConvInfo` to get the @ data list of the conversation.
2. Call the `conv_group_at_info_at_type` API ([c#](https://comm.qq.com/im/doc/unity/en/types/GroupsAttributes/GroupAtInfo.html)) of the `GroupAtInfo` object in the list to get the @ data type and update it to the @ information of the conversation.

Sample code:


```c#
TIMResult res = TencentIMSDK.ConvGetConvList((int code, string desc, List<ConvInfo> info_list, string user_data)=>{
  foreach (ConvInfo info in info_list)
  {
    foreach (GroupAtInfo at_info in info.conv_group_at_info_array)
    {
      if (at_info.conv_group_at_info_at_type == TIMGroupAtType.kTIMGroup_At_Me) {
        // @me
      }
      if (at_info.conv_group_at_info_at_type == TIMGroupAtType.kTIMGroup_At_All) {
        // @all
      }
      if (at_info.conv_group_at_info_at_type == TIMGroupAtType.kTIMGroup_At_All_At_ME) {
        // @all and @me
      }
    }
  }
});
```


