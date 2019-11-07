> ?
>- CDN supports configuring Range GETs, where Range is the HTTP request header used to specify the request for the specified part of a file. For example, `Range: bytes = 0-999` can be used to request the first 1,000 bytes of a file. This feature can increase the delivery efficiency and improve the response speed for large files.
>- The origin server should support Range requests; otherwise, origin-pull will fail.
>-  When Range GETs configuration is enabled, resources will be cached in shards on the node, but the cache expiration time of all shards is the same and in accordance with the user-defined cache expiration rule.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Name Management** on the left sidebar to enter the management page. Find the domain name you want to edit and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/99e0c24b4530c30b9abe27325bb1b317.png)
2. Click **Origin Configuration** and you will see the **Range GETs Configuration** module. The feature is enabled by default.
 ![img](https://main.qcloudimg.com/raw/7653b9061b29fea611ae396df373c2cc.png)

## Sample Case
- If the Range GETs configuration of the `www.test.com` domain name is as follows:
![img](https://main.qcloudimg.com/raw/d08305ba88dd4afc1cca6091b12d9528.png)
Then, when user A makes a request for the `http://www.test.com/test.apk` resource, after the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate a Range GETs request to obtain and cache the resource by shards; if user B also makes a Range request at this time and the shards stored on the node match the specified byte segment in the Range request, the resource will be directly returned to the user without having to wait until all shards are obtained.
- If the Range GETs configuration of the `www.test.com` domain name is as follows:
![img](https://main.qcloudimg.com/raw/2e0aee010a727ec375927482e114a210.png)
  Then, when user A makes a request for the `http://www.test.com/test.apk` resource, after the node receives the request and finds that the cached `test.apk` file has already expired, it will initiate an origin-pull request to directly obtain the entire resource from the origin server and then return it to the user.
