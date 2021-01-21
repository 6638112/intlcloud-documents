Tencent Cloud allows you to create a CLB instance on the official purchase page or via API. The two methods are detailed below:

### Creating a CLB instance on the official purchase page
You can purchase a CLB instance on [Tencent Cloud official website](https://buy.cloud.tencent.com/lb). Private network CLB instances are free of charge, while public network CLB instances charge instance fees on an hourly pay-as-you-go basis. You can purchase public network on [CVM](https://intl.cloud.tencent.com/document/product/213/495). For more information on the network billing modes, please see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).

For the purchase method for bill-by-CVM accounts, please see [Purchase Methods](https://intl.cloud.tencent.com/document/product/214/8849). For users of bill-by-IP accounts, the purchase steps are as follows:
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. For the **Instance type**, **Cloud Load Balancer** is recommended.
3. Select attributes as needed, including the network type and project. For attribute details, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
>?Currently, the static single-line IP is supported only in Hangzhou, Jinan, Fuzhou, Wuhan, Changsha, and Shijiazhuang. For its support in other districts, please see the console. The feature is currently in beta, if you want to try it out, please submit an application. Once you are accepted, you can select an ISP (China Mobile, China Unicom, or China Telecom) on the purchase page.
>
![](https://main.qcloudimg.com/raw/907a33302d20a9b399067bee190a1d78.png)
4. After confirming the order, make the payment using account balance, online banking, WeChat Pay, or QQ Wallet, etc.
5. CLB service will be activated once the payment completes. You can now configure and use the CLB instance.

### Creating a CLB instance via API
To purchase a CLB instance via API, please see **CreateLoadBalancer** in [API Category](https://intl.cloud.tencent.com/document/product/214/33789).
