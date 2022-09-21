## 功能描述
群成员搜索只能搜索本地存储过的群成员，例如拉取过的群成员列表、拉取过的群成员资料等。

> ? flutter sdk 3.8.0支持，直播群（AVChatRoom）不在本地存储群成员，无法使用群成员搜索功能。

## 搜索本地群组
您可以调用接口 `searchGroupMembers` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html)) 搜索本地群成员。
您可以设置搜索关键字 `keywordList`，并指定搜索的范围，即是否搜索群成员的 `memberUserID`、`memberNickName`、`memberRemark`、`memberNameCard` 字段。

根据 `searchGroupMembers` 入参 `V2TIMGroupMemberSearchParam` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html)) 中的 `groupIDList` 是否为空（`null`/`nil`），分为两种情况：
- 如果设置 groupIDList 为空，代表搜索全部群中的群成员，返回的结果会按照 groupID 进行分类；
- 如果设置 groupIDList 不为空，代表搜索指定群中的群成员。

示例代码如下：



```dart
// 通过关键字、群id搜索群成员
V2TimValueCallback<V2GroupMemberInfoSearchResult> searchGroupMem = await groupManager.searchGroupMembers(param: V2TimGroupMemberSearchParam(groupIDList: ['可指定群ID'],keywordList: ['关键字'],isSearchMemberNameCard: true,isSearchMemberNickName: true,isSearchMemberRemark: true,isSearchMemberUserID: true,));
```



