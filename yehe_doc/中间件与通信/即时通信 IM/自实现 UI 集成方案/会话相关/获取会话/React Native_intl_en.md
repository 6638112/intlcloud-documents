## Feature Description

The IM SDK provides an API for getting conversations, which can be used to get the `V2TimConversation` object information of one or multiple specified conversations.

### Getting a specified conversation

Call `getConversation` ([TS](https://comm.qq.com/im-react-native-doc/classes/ConversationManager________.V2TIMConversationManager.html#getConversation)) to get the information of a conversation, which is a `V2TimConversation` object.

Below is the sample code:

```javascript
const conv = await conversationManager.getConversation("conversationID");
```

### Getting specified conversations

Call `getConversationList` ([TS](https://comm.qq.com/im-react-native-doc/classes/ConversationManager________.V2TIMConversationManager.html#getConversationList)) to get the list of specified conversations that stores `V2TimConversation` objects.

Below is the sample code:

```javascript
const count = 10;
const nextSeq = "";

const convList = await conversationManager.getConversationList(count, nextSeq);
```


