## Feature Description
One-to-one messages and group messages can be cleared.
When messages in a conversation are cleared, all the messages in the conversation will be cleared both **locally and from the cloud**, but the conversation itself will not be deleted.

> ?**Do not** use this API if you do not want to clear messages from the cloud.

If the last message is deleted, the `lastMessage` in the conversation will become the last but one message.



### Clearing one-to-one messages

Call `MsgClearHistoryMessage` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgClearHistoryMessage_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_callback_NullValueCallback_)) to clear one-to-one messages.


Sample code:



```c#
TIMResult res = TencentIMSDK.MsgClearHistoryMessage(conv_id, TIMConvType.kTIMConv_C2C, (int code, string desc, string user_data) => {
  // Process the callback logic
 });
```



### Clearing group messages

Call `MsgClearHistoryMessage` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_MsgClearHistoryMessage_System_String_com_tencent_imsdk_unity_enums_TIMConvType_com_tencent_imsdk_unity_callback_NullValueCallback_)) to clear group messages.

Sample code:


```c#
 TIMResult res = TencentIMSDK.MsgClearHistoryMessage(conv_id, TIMConvType.kTIMConv_Group, (int code, string desc, string user_data) => {
  // Process the callback logic
 });
```



