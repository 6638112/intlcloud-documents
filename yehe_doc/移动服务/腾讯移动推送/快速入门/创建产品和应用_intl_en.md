
## Operation Scenarios
This document guides you in how to create products and applications and configure applications in the TPNS Console.

## Prerequisites
You have a Tencent Cloud account. For more information, please see [Signing Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions
### Creating Product
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Product Management** on the left sidebar.
2. Go to the product management page and click **Add Product**.
3. In the pop-up window, enter the product name and product description. Select a product category and service access point. For more information about the service access point, see [Global Deployment](https://intl.cloud.tencent.com/document/product/1024/35233).
4. If you check Android, iOS, or macOS below, the system will create an application on the selected platform by default.
![](https://main.qcloudimg.com/raw/463013c99e476af32767de8b2d48ff49.png)
5. Click **Confirm**. You can click **View User Guide** to complete the access as instructed.
	 ![](https://main.qcloudimg.com/raw/e4f98c5b7a615009ccbff29d0a7fb166.jpg)

### Creating application
After you create a product, if you haven't added the default application, you can follow the steps below to create an application. Only one application can be created per platform. After applications have been created for all three platforms, no new applications can be created.

#### Android application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **Android** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)

#### iOS application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **iOS** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)

#### macOS application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **macOS** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)





### Configuring application
After you create an application, you can follow the steps below to configure it.


#### Android configuration
1. Go to the product list page, select the Android application, and click **Configuration Management**.
2. Enter the application package name for the Android platform and click **Save** to complete basic configuration.
3. You can choose to enable the vendor channel configuration as needed.


#### iOS configuration
1. Go to the product list page, select the iOS application, and click **Configuration Management**.
2. Enter the `BundleID` for the iOS platform and click **Save** to complete basic configuration.
3. Go to the configuration management page, click **Upload Certificate**, enter the certificate password and select a certificate to upload.
4. Click **Upload** to push your selected certificate to the console and complete iOS application configuration.
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)

#### macOS configuration
1. Go to the product list page, select the macOS application, and click **Configuration Management**.
2. Enter the `BundleID` for the macOS platform and click **Save** to complete basic configuration.
3. Go to the configuration management page, click **Upload Certificate**, enter the certificate password and select a certificate to upload.
4. Click **Upload** to push your selected certificate to the console and complete iOS application configuration.
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)


