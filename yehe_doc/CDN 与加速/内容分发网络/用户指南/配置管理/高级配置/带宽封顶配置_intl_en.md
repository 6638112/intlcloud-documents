## Configuration Scenario

Tencent Cloud CDN is pay-as-you-go. If you are concerned about excessive bandwidth usage and fee surges due to hotlinking by malicious users, you can set a bandwidth cap to control usage. This feature is only applicable to bill-by-bandwidth users.

Bandwidth cap configuration can detect the bandwidth generated in a statistical period (at a 5-minute granularity) and perform forced origin-pull according to the configuration or disable the CDN service (a 404 error will be returned for all requests) if the threshold is exceeded. This will avoid incurring additional CDN acceleration fees.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click the domain name to enter its configuration page. You will find the bandwidth cap configuration on the **Advanced Configuration** tab. It is disabled by default:
![](https://main.qcloudimg.com/raw/2dc4d64a3c1f4054471a31681c19765e.png)

### Modifying the configuration
#### 1. Modify the configuration
You can toggle the switch to configure the bandwidth threshold:
- For COS origin server domain names, returning a 404 error is the only option when the threshold is reached.
- If the detected domain name bandwidth exceeds the threshold, origin-pull or return of the 404 error for access needs to be implemented across the entire network node by node; therefore, there may be a certain delay for the configuration to take effect.

![](https://main.qcloudimg.com/raw/7520963775f790d2adaf588b9418bd7c.png)

#### 2. Disable the configuration
You can toggle the bandwidth cap switch to disable this feature. When the switch is off, any existing configuration will not take effect in the production environment. If you toggle the switch on, a message will be displayed asking for your confirmation before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/1a18d747e269347c90aa17f116601509.png)

#### 3. Add region-specific configuration
If your acceleration domain name is configured for global acceleration and you want to configure acceleration in and outside Mainland China with different bandwidth cap settings, you can click **Add Special Configuration**.
![](https://main.qcloudimg.com/raw/1a855e379a90af8de76c0ee26727e632.png)

>Currently, an added region-specific configuration item cannot be deleted, it can only be disabled.

## Configuration Sample
Suppose the bandwidth cap configuration of the acceleration domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/772256e11f3c1c9a85ae9cc57315c4f6.png)
The access status will be as follows:
If the bandwidth reaches 11 Gbps in Mainland China and 4 Gbps outside Mainland China, a 404 error will be returned for access requests from all users in Mainland China, while users outside Mainland China can still enjoy the acceleration service.

