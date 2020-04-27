## Configuration Scenario
SEO optimization configuration is a feature that solves the problem of incorrect weights for domain name searches due to frequent IP changes by CDN after a domain name is connected to CDN. By identifying whether an access IP belongs to a search engine, you can choose to directly pull the resource from the origin server, ensuring the stability of search engine weights.

>
> - As search engine IPs are updated very frequently, Tencent Cloud CDN can only guarantee that most but not all search engine IPs can be identified.
> - The SEO optimization configuration feature is available only when the connected domain name is your **own**. After this feature is enabled, if a domain name has multiple origin server addresses, the first one will be the default origin-pull address.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click the domain name to enter its configuration page. You will find the SEO optimization configuration on the **Advanced Configuration** tab. It is disabled by default:
![](https://main.qcloudimg.com/raw/44f35a715f922cda12191d50e1cfc723.png)

### Modifying the configuration
Toggle the switch to enable or disable SEO optimization configuration:
![](https://main.qcloudimg.com/raw/8ea737dbd456397286f3ef8ff965aaf2.png)

>  If your domain name is configured for global acceleration, the SEO optimization configuration will take effect globally once enabled. This configuration does not distinguish between requests from Mainland China and from outside Mainland China.

