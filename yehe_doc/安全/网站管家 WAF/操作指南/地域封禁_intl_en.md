## Overview
This region blocking feature can use a blacklist to block all access sources from overseas countries and regions as well as provinces and regions of China.

## Configuration
1. Assume that you have purchased the WAF service. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia), select **Web Application Firewall**>**Defense settings** in the left sidebar to enter the defense settings page, and click the domain name you want to protect.
 ![](https://main.qcloudimg.com/raw/c34767bb72e2b047fcb1e084d6d6f38b.png)
2. Select the **Basic Settings** tab, and click **Choose Blocked Region** in the lower right corner to enter the configuration page.
 ![](https://main.qcloudimg.com/raw/d5fe88e4584bd0a8cff572c9d4a22f51.png)
3. Check the boxes for the regions in China you want to block. For overseas regions, you can select them by searching or with a drop-down list. Then, click **Confirm**.
 ![](https://main.qcloudimg.com/raw/8a8f3433a2baf81a0ed1f7a99a5c6932.png)
4. Once completed, region blocking will be enabled instantly.
 ![](https://main.qcloudimg.com/raw/9435bca728b75dd920a84096e7d9643a.png)
5. Now you will be unable to visit your website from any of the blocked regions. For example, if you block all foreign regions, and visit a WAF-protected website with an overseas IP address, WAF will notify you that you have been blocked with an error page as shown below:
 ![](https://main.qcloudimg.com/raw/5d694217bed9bd731eb7ce3473a8f32d.png)

[Previous: Leak Protection](https://intl.cloud.tencent.com/document/product/627/14582)
[Next: BOT Behavior Management](https://intl.cloud.tencent.com/document/product/627/15340)
