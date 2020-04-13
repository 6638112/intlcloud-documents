## Configuration Scenario

CDN will shard files to improve storage efficiency when caching resources. It also supports Range requests. For example, if a request carries HTTP header `Range: bytes = 0-999`, the first 1,000 bytes of the file will be returned to the user.

After Range GETs is enabled, if a partial file requested by a user has expired, CDN will perform Range GETs to pull and cache the required partial file and return it to the user. After Range GETs is disabled, even if a user only requests a partial file, CDN will pull the entire file and then cache it before returning the requested partial file to the user.

Enabling Range Gets can greatly increase the delivery efficiency of large files, improve response time, and reduce the pressure on the origin server.

> Note:
>
> When Range GETs is enabled, resources will be cached in shards on the node, and these shards have the same cache expiration time and follow the cache expiration rule defined by the user.

## Configuration Guide

### Viewing configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Origin Configuration** tab, find Range GETs configuration, which is disabled by default. It is enabled by default for domain names of COS origin servers:
![img](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)

### Modifying configuration

You can enable or disable Range GETs. To enable it, first confirm that the origin server supports Range requests, otherwise the operation may fail.
![img](https://main.qcloudimg.com/raw/0c7d65308c5ae22693bb29b51345ce83.png)

> Note:
>
> If your acceleration domain name is configured for global acceleration, the Range GETs configuration will take effect globally. It does not distinguish between requests from and outside of Mainland China.

## Configuration Sample

Suppose the Range GETs configuration of the domain name `cloud.tencent.com` is as follows:
![img](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)
User A makes a request for the `http://cloud.tencent.com/test.apk` resource. After the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate a Range GETs request to get and cache the resource by shards. If user B also makes a Range request at this time and the shards stored on the node match the specified byte segments in the Range request, the resource will be directly returned to user B without waiting to have all shards obtained.