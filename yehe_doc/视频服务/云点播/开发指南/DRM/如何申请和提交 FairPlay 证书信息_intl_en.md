## Instructions

### Overview

This document shows you how to apply for a FairPlay certificate from Apple and submit the following information to Tencent Cloud VOD:

- FairPlay Streaming (FPS) certificate (format: CER)
- Private key file (format: PEM)
- Private key password
- Application secret key (ASK)

## Step 1. Request FairPlay Streaming Deployment Package

1. Go to the [Apple FairPlay page](https://developer.apple.com/streaming/fps/), scroll to the bottom, and click **Request FPS Deployment Package**. A form will pop up.

> Note: You need to log in with an Apple developer account.

2. Fill out the form and submit it.

3. After your request is approved, you will be issued an `FPS_Deployment_Package.zip` package.

## Step 2. Create a Private Key and a Certificate Signing Request (CSR)

Unzip `FPS_Deployment_Package.zip` and create a password-protected private key file and a CSR file as instructed in the guide document (PDF) in the package.

1. Run the command below to create a private key file (`privatekey.pem`):

   ```shell
openssl genrsa -aes256 -out privatekey.pem 1024
   ```
   You need to set a password (preferably not longer than 32 characters) for the private key. Note the password for later use.
   
   ![image-20220421115813168](https://qcloudimg.tencent-cloud.cn/raw/ce0f6e159601c772694e79c69648e343.png)
   
2. Run the command below to create a CSR file (`certreq.csr`):

   ```shell
   openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
   ```
   You need to enter the private key password.
   
   ![image-20220421115929084](https://qcloudimg.tencent-cloud.cn/raw/25c7097a4633a2429b0f7173c0f255b6.png)


## Step 3. Generate the FPS Certificate

Get the FPS certificate and ASK from the [Apple developer page](https://developer.apple.com/account).

1. Go to the [Apple developer page](https://developer.apple.com/account) and click **Certificates, IDs & Profiles** in the left sidebar.

   ![image-20220419113745847](https://qcloudimg.tencent-cloud.cn/raw/29e8bb1b63a60c877f17dd0c39d9e8d5.png)

2. Click **+**.

   ![image-20220419113637808](https://qcloudimg.tencent-cloud.cn/raw/4b88b93e4450b7171f09a3b75e2cb2bc.png)

3. Select **FairPlay Streaming Certificate** and click **Continue**.

   ![image-20220419114215512](https://qcloudimg.tencent-cloud.cn/raw/00fa1494b1256c9b4e1d769356450721.png)

4. Click **Choose File**, select the `certreq` file created in Step 2, and click **Continue**.

   ![image-20220419114506263](https://qcloudimg.tencent-cloud.cn/raw/52c2834bf36f4074e7f9f731aefc8948.png)

5. Copy and note the ASK, enter it into the input field below, and click **Continue**.

   ![image-20220419114920781](https://qcloudimg.tencent-cloud.cn/raw/8e55fb6e817a2279f6b2cea3418506f7.png)

6. A window will pop up to confirm that you have saved the ASK. Click **Generate**.

   > Note: Make sure you save a copy of the ASK. You will be unable to view it afterwards.

   ![image-20220419115103618](https://qcloudimg.tencent-cloud.cn/raw/808347b36d824de46b6cbb84654d20c8.png)

7. After the above steps are completed, the FPS certificate generated (type: FairPlay Streaming) will appear in the certificate list.

   ![image-20220419115340087](https://qcloudimg.tencent-cloud.cn/raw/ee831cfc5c26f37bdc09c9a50bab5ef5.png)

8. Click **Download** to download the FPS certificate (`fairplay.cer`).

   ![image-20220419115536031](https://qcloudimg.tencent-cloud.cn/raw/d7e7ad03c0168b61db084cfee762f6cc.png)


## Step 4. Submit the Certificate Information in the Tencent Cloud VOD Console

1. Log in to the VOD console.
2. Click **Video Processing** in the left sidebar and then click **DRM Configuration**.
3. Submit the certificate information, including the certificate file (`fairplay.cer`), private key file (`privatekey.pem`), private key password, and ASK.

