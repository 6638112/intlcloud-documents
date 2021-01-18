You can generate UserSig online in the TRTC console, but it should be used only for quick testing at the development stage. For official launch, please [calculate UserSig on the server](https://intl.cloud.tencent.com/document/product/647/35166). This avoids key leakage and prevents attackers from stealing your traffic.


<span id="generate"></span>
## UserSig Generator
Signatures (UserSig) allow you to build trust with Tencent Cloud.

1. Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.
2. In **Signature (UserSig) Generator**, select the application (`SDKAppID`) you created from the drop-down list. A secret key (`key`) is generated automatically.
3. Enter the user name (`UserID`).
4. Click **Generate Signature (UserSig)** to generate your UserSig.


<span id="check"></span>
## Signature (UserSig) Checker
This is used to check the validity of your signature (UserSig).

>! Make sure that you enter the right SDKAppID and UserID for the UserSig you want to verify.

1. Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.
2. In **Signature (UserSig) Checker**, select the application (`SDKAppID`) whose signature you want to verify. A secret key is generated automatically.
3. Enter the user name (`UserID`).
4. Copy and paste the signature (UserSig) that needs verification to **Signature (UserSig)**, and click **Verify Now**.
>? If your UserSig is generated in **Signature (UserSig) Generator**, click **Copy Signature (UserSig)** to copy the signature.
>
5. View the verification results.
	- Example of successful verification:
	- Example of failed verification:


## Documentation
- For more information about UserSig, see [FAQs (UserSig)](https://intl.cloud.tencent.com/document/product/647/35166).
