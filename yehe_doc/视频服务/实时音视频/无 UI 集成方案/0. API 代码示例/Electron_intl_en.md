This document describes how to quickly run the TRTC-API-Example for Electron.

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions
[](id:step1)
### Step 1. Create an application
1. In the TRTC console, click **Development Assistance** > [Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart).
2. Select **New** and enter an application name such as `TestTRTC`. If you have already created an application, select **Existing**.
3. Add or edit tags according to your needs and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)

>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and TRTC-API-Example source code

1. TRTC-API-Example source code
```shell script
git clone https://github.com/tencentyun/TRTCSDK
cd Electron/TRTC-API-Example
```

[](id:step3)
### Step 3. Configure TRTC-API-Example project files

1. Find and open `Electron/TRTC-API-Example/assets/debug/gen-test-user-sig.js`.
3. Set parameters in `gen-test-user-sig.js` as follows:
	<ul><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
	<li/>SECRETKEY: An empty string by default. Set it to the actual key.</ul>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of TRTC-API-Example**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Compile and run the demo
```shell
npm install
cd src/app/render/main-page
npm install

cd ../../..
npm run start
```

## FAQs
### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and, in **Step 2: obtain the secret key to issue UserSig**, click **HMAC-SHA256**.
  - Upgrade

  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. What are the restrictions of the firewall?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, you can refer to [Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) to troubleshoot the issue.
