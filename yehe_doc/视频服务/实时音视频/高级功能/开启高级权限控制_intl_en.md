## Introduction

If you want to impose restrictions on room entry or mic-on for certain rooms, that is, only specified users are allowed to enter a room or mic on, and you are worried that permission verification, if implemented on the client, would be easy to crack and attack, then you can consider **Enabling Advanced Permission Control**.

You do not need to enable advanced permission control in the scenarios below:

- Scenario 1: There are more viewers, the better and no requirements for permission control of room entry.
- Scenario 2: There is no urgent need to prevent attackers from cracking the client.

You are recommended to enable advanced permission control for better security in the scenarios below:

- Scenario 1: There are video or audio calls with high security requirements.
- Scenario 2: There are different access permissions for different rooms.
- Scenario 3: There are permission controls for viewer’s mic-on.


## Supported Platforms

|   iOS    | Android  | Mac OS  | Windows  | Electron |  Chrome browser |
| :------: | :------: | :------: | :------: | :------: |  :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |     &#10003;    |

## Principles of Advanced Permission Control

Once the advanced permission control is enabled, the backend service system of TRTC will verify the UserSig (a room entry ticket), as well as the permission ticket called **PrivateMapKey**, which contains an encrypted roomid and an encrypted permission bit list.

Since PrivateMapKey contains roomid, users cannot enter the specified room when only providing UserSig but no PrivateMapKey.

The eight bits in a byte, which is used by “permission bit list” of PrivateMapKey, respectively represents the eight specific feature permissions of the user who holds the ticket in the room specified by the ticket.

| Bits    | Binary | Decimal | Permission Description                             |
| ------- | ---------- | :--------: | ------------------------------------ |
| The first bit | 0000 0001  |     1      | Permission for room creation                       |
| The second bit | 0000 0010  |     2      | Permission for room entry                       |
| The third bit | 0000 0100  |     4      | Permission for sending audio                       |
| The fourth bit | 0000 1000  |     8      | Permission for receiving audio                       |
| The fifth bit | 0001 0000  |     16     | Permission for sending video                       |
| The sixth bit | 0000 1000  |     8      | Permission for receiving video                       |
| The seventh bit | 0100 0000  |     64     | Permission for sending substream video (namely screen sharing) |
| The eighth bit | 1000 0000  |    128     | Permission for receiving substream video (namely screen sharing) |


## Enabling Advanced Permission Control
<span id="step1"></span>
### Step 1: Log in to TRTC console and enable permission key.

1. On TRTC console, click **Application Management**(https://console.cloud.tencent.com/trtc/app) in the left sidebar.
2. Select an application you want to enable advanced permission control in the right application list, and click **Application Info**.
3. Enable **Start permission key** in “Application Info” tab, and then click **Confirm** in the pop-up window.
![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)

>!When a certain SDKAppid enables advanced permission control, all users using this SDKAppid need to pass in `privateMapKey` parameter in `TRTCParams` to successfully enter the rooms (as described in [Step 2](#step2)). So please make sure you want to enable this feature if there are users using this SDKAppid online.

<span id="step2"></span>
### Calculate `privateMapKey` on your server.

As `PrivateMapKey` aims to prevent the client from being reversely cracked (i.e., non-members can enter high-level rooms), it should be calculated on your server and then returned to your application. Please do not calculate on your application directly.

Three samples of code for calculating `PrivateMapKey` are provided for Java, PHP, and Node.js, respectively, which can be directly downloaded and integrated into your server.

| Programming Language |                         Key Function                         |                           Download Link                           |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
|   Java   | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
|    GO    | `GenPrivateMapKey` and `GenPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
|   PHP    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
|  Node.j  | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
|  Python  | `genPrivateMapKey`and `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
|    C#    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |

<span id="step3"></span>
### Step 3: Distribute `PrivateMapKey` from your server to your application.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)
As shown in the figure above, the PrivateMapKey will be distributed to your application after being calculated on your server, and then the application will deliver it to SDK in two ways below:

#### Solution 1: Deliver to SDK when calling `enterRoom`.
You can set **privateMapKey** in [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) when calling the `enterRoom` API of `TRTCCloud` to control the permission of room entry.

This scheme of verifying PrivateMapKey when entering the room is simple, and is suitable for scenarios where the user's permissions can be confirmed before the user enters the room.


#### Solution 2: Update to SDK through experimental APIs.
During live streaming, there are often co-anchoring scenarios where viewers can mic on and become an anchor. In this case, TRTC will verify the `PrivateMapKey` carried in the entry parameter `TRTCParams` again when entering the room. If you set a short validity period for `PrivateMapKey` such as 5 minutes, it will be easy to trigger a verification failure and cause the user to be kicked out of the room.

To solve this problem, in addition to extending the validity period (for example, changing "5 minutes" to "6 hours"), you can also reapply for a `PrivateMapKey` from your server and update it to SDK by calling the SDK’s experimental API `updatePrivateMapKey` before viewers switch their identities to anchors through `switchRole`. Sample code is as follows:

```java
JSONObject jsonObject = new JSONObject();
try{
    jsonObject.put("api", "updatePrivateMapKey");
    JSONObject params = new JSONObject();
    params.put("privateMapKey", "xxxxx"); // Fill in a new privateMapKey
    jsonObject.put("params", params);
    mTRTCCloud.callExperimentalAPI(jsonObject.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
```

## FAQs
<span id="q1"></span>
#### 1. Why can't I enter any online room?

Once room permission control is enabled, all rooms under the current `SDKAppid` can be entered only after `privateMapKey` is set in `TRTCParams`, so if your online business is in operation and the relevant logic of `privateMapKey` has not been added to it, please do not enable this feature.

<span id="q2"></span>
#### 2. What is the difference between PrivateMapyKey and UserSig?

`UserSig` is the required field of `TRTCParams`, which is used to check whether the current user is authorized to use the TRTC cloud service so as to prevent attackers from stealing the traffic in your `SDKAppid` account.

`PrivateMapKey` is an optional field of `TRTCParams`, which is used to check whether the current user is authorized to enter the room with the specified `roomid` and the user’s permissions in the room. It is only necessary if your business needs to distinguish between different users.
