## Overview


## Preparations 
- You have integrated the [ServerSDK code package](https://intl.cloud.tencent.com/document/product/1055/36674). You can also [use the demo package](https://intl.cloud.tencent.com/document/product/1055/36678).  
- You have created server fleet 1 (in the Shanghai region).
- You have created server fleet 2 (in the US region).



## Directions
### Creating a game server queue
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Game Server Queue** on the left sidebar.
2. Select and add the created server fleets "Shanghai - server fleet 1" and "US - server fleet 2" to the queue.
3. Access the server fleet details page and modify the delay policy: 
 - In the first 10 seconds, servers in regions where the delay for all players is below 80 ms will be matched first.  
 - In the subsequent 10 seconds (i.e., in the first 20 seconds), servers in regions where the delay for all players is below 100 ms will be matched first.
 - Afterwards, servers in regions where the delay for all players is below 150 ms will be matched. 


### Using the queue to create a game server session

Place a game server session. In addition to integrating the SDK into the code to call a TencentCloud API, you can also use [TencentCloud API debugging](https://console.cloud.tencent.com/api/explorer?Product=gse) to quickly create a session.

**Input parameters**:  
- The delay for player 1 is 100 ms to Shanghai and 50 ms to Silicon Valley.
- The delay for player 2 is 60 ms to Shanghai and 80 ms to Silicon Valley.




Since the delay policy specifies that in the first 10 seconds, servers in regions where the delay for all players is below 80 ms will be matched first, the game server session will be scheduled to the Silicon Valley region.  



**The test result returned after the API call: the game server session is scheduled to "Silicon Valley - server fleet 2"**.





