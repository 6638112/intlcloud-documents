## Offline Push Check
### Offline push issue finder
This tool allows you to query issues related to the failure to receive offline messages.

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im) and then click the target IM app card.
2. In the left sidebar, choose **Auxiliary Tools** > **Offline Push Check**.
3. In the **Offline push issue finder** area, enter the UserID.
4. Click **Get device information** to view the uploaded information for the UserID, such as the certificate ID and device token.
 >If no UserID information, such as the certificate ID and device token, has been uploaded, the query ends.
 >
5. Select any certificate ID of the UserID, and then click **Start testing**. You can view the sending result of the test offline message in the **Test results** field.
 - If a success prompt is sent the certificate information you entered on the console is correct and the token was uploaded by calling the SDK API. You can use the [user client status checking tool](#status) for further troubleshooting. 
 - If a failure prompt is sent, you can view the cause of the failure and the solution.
![](https://main.qcloudimg.com/raw/76b40ef61f2034718dc489519d4f7c4d.png)

<span id="status"></span>
### User client status checking tool
This tool automatically obtains the user’s client status and checks whether the user is ready to receive offline push messages.

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im) and then click the target IM app card.
2. In the left sidebar, choose **Auxiliary Tools** > **Offline Push Check**.
3. In the **User client status checking tool** area, enter the UserID.
4. Click **Get status** to view information such as the current status and client type of the UserID.
 If you are prompted that the UserID is ready to receive offline push messages, you can log in with a different UserID on another device to send one-to-one text messages to the current UserID to check whether it can receive the messages.
![](https://main.qcloudimg.com/raw/858a4c73c2dd149933fb6133359ece4c.png)

## UserSig Generation and Verification
### UserSig generator
The system automatically obtains the key of the current app. After entering the UserID, you can use this tool to quickly generate a signature (UserSig) to run through demos and debug features locally. If you need to generate a UserSig for online services, see [Generating a UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im) and then click the target IM app card.
2. In the left sidebar, choose **Auxiliary Tools** -> **UserSig Tools**.
3. In the UserSig Generator area, enter the UserID.
4. Click **Generate UserSig** to generate a UserSig, which expires after 180 days.
5. Click **Copy UserSig** to copy the signature and then paste and save the signature.
![](https://main.qcloudimg.com/raw/858a4c73c2dd149933fb6133359ece4c.png)

### UserSig verification tool
The system automatically obtains the key of the current app. After entering the UserID and UserSig, you can use the tool to quickly check the validity of the UserSig.

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im) and then click the target IM app card.
2. In the left sidebar, choose **Auxiliary Tools** -> **UserSig Tools**.
3. In the UserSig Verification Tool area, enter the UserID and UserSig.
   
4. Click **Verify** to see the verification results.
 - If verification succeeds, you can view the SDKAppID, UserID, generation time, service time, and expiration time of the UserSig in the verification results.
    
 - If verification fails, you can view the cause of failure and solution in the verification results.
    

