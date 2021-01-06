Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Callback Configuration** in the left sidebar. You can configure callback URLs and decide which callbacks to enable according to your business needs.

## Configuring Callback URLs

1. On the **Callback Configuration** page, click **Edit** in the callback URL configuration area.
2. In the callback URL configuration dialog box that pops up, enter the callback URL.
 >?
 >- The callback URL must start with `http://` or `https://`.
 >- If you have not yet applied for a domain name, you can directly configure an IP address, for example, `http://123.123.123.123/imcallback`.
 >
3. Click **OK** to save the configuration.

## Configuring Event Callbacks
1. On the **Callback Configuration** page, click **Edit** in the event callback configuration area.
2. In the event callback configuration dialog box that pops up, check the desired callbacks.
 ![](https://main.qcloudimg.com/raw/aeaa08f9aa11578ee0e4c7778fb32cc7.png)
3. Click **OK** to save the configuration.

## Downloading an HTTPS Mutual Authentication Certificate
After configuring callback URLs, you can download an HTTPS mutual authentication certificate from the console for future use.
>? You can configure mutual authentication based on your actual needs. For the detailed configuration methods, see [Mutual Authentication Configuration](https://intl.cloud.tencent.com/document/product/1047/34379).

1. Go to the [console](https://console.cloud.tencent.com/im-detail/callback-setting), open the **[Callback Configuration](https://console.cloud.tencent.com/im-detail/callback-setting)** page, and click **Download HTTPS Mutual Authentication Certificate** in the callback URL configuration area in the upper-right corner.
![](https://main.qcloudimg.com/raw/c9ecc4110b317d69eafa0fda2d034159.png)
2. In the certificate download dialog box that pops up, click **Download**.
![](https://main.qcloudimg.com/raw/33e01ce0443b5c7f341a5fcac2b95215.png)
3. Save the certificate file.


## Subsequent Operations
After configuring callback URLs and enabling the corresponding event callbacks, you can refer to [Third-Party Callbacks](https://intl.cloud.tencent.com/document/product/1047/34354) to use the corresponding callback features in order to obtain user and operation information in real time.
