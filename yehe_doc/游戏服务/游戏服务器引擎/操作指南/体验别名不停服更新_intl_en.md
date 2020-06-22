## Overview
This document describes how to update with zero downtime an application with an alias.




## Preparations 
- You have integrated the [ServerSDK code package](https://intl.cloud.tencent.com/document/product/1055/36674). You can also [use the demo package](https://intl.cloud.tencent.com/document/product/1055/36678).
- You have created server fleet 1.
- You have created server fleet 2.
![](https://main.qcloudimg.com/raw/55a163fc4ae8acd7eed20ce7f1e1b805.png)

## Directions
### Creating an alias 
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Alias** on the left sidebar.
2. Select the service region in the top-left corner and click **Create**.
3. Access the alias creation page, enter information such as the name, the alias type, and the description, and click **OK**.
 - Name: enter the alias name.
 - Type: select the alias type.
    - Common alias: it points to a fleet, under which the system will automatically find servers and assign them to clients.
    - Termination alias: it means that a common alias has been terminated. You can describe the reason why the alias cannot be used in the termination information, which will be sent to clients.
 - Associate Server Fleet: select "server fleet 1".
 - Description: enter the description.
4. After configuring the settings, click **OK** to create the alias.
![](https://main.qcloudimg.com/raw/555e3b9d69522de33392167b286e0a70.png)

### Creating a game server session
In addition to integrating the SDK into the code to call a TencentCloud API, you can also use [TencentCloud API debugging](https://console.cloud.tencent.com/api/explorer?Product=gse) to quickly create a session.

If a game server session is successfully created through TencentCloud API debugging, you will see that it is generated in server fleet 1.


### Modifying the alias configuration
1. Access the alias list page, select the created alias, and click **Edit** in the top-right corner.
2. Access the alias editing page, modify the alias configuration, and set "Associate Server Fleet" to "Server fleet 2".

### Creating another game server session
>Create another game server session with the same alias.

After another game server session is created through TencentCloud API debugging, you will see that there is still only one game server session in server fleet 1.

A game server session is generated in server fleet 2. As you can see, the new session is assigned to server fleet 2.



### Notes on zero downtime updates
When the version needs to be updated, you can create a new fleet and point the alias to it.
- Automatic reduction will be performed on the original fleet as the number of game server sessions decrease.
- Automatic expansion will be performed on the new fleet with zero downtime as the number of game server sessions increase.






