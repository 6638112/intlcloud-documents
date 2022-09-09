## Feature Description

Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

## Searching a Local Group

Call the `searchGroups` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#searchGroups)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:

```javascript
// Search for a group by the keyword
const searchGroup = await groupManager.searchGroups({
  keywordList: ["Keyword"],
  isSearchGroupID: true,
  isSearchGroupName: true,
});
```


