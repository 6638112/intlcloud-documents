Tencent Cloud CLB supports three IP versions: IPv4, IPv6, and IPv6 NAT64. IPv6 CLB supports the TCP, UDP, TCP SSL, HTTP, and HTTPS protocols and provides flexible forwarding capabilities based on domain names and URL paths. This document guides you through how to get started with IPv6 CLB.
>?The IPv6 CLB is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).

## Prerequisites
1. CLB only forwards traffic but cannot process requests; therefore, you need to create a CVM instance that processes user requests and configure its IPv6 settings first.
2. This document takes HTTP forwarding as an example. The corresponding web server (such as Apache, Nginx, or IIS) must be deployed on the CVM instance, and the port used by the server needs to listen on IPv6.

## Limits
- Currently, IPv6 CLB is only supported in the following regions: Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, and Virginia.
- IPv6 CLB does not support classic CLB.
- IPv6 CLB supports obtaining the client's IPv6 source address, which can be directly obtained by layer-4 IPv6 CLB or through the `X-Forwarded-For` header of HTTP layer-7 IPv6 CLB.
- Currently, IPv6 CLB balances the load completely over the public network. Clients in the same VPC cannot access IPv6 CLB over the private network.
- IPv6 implementations are still at the preliminary stage across the internet. In case of access failure, you can [submit a [ticket](https://console.cloud.tencent.com/workorder/category). SLA is not guaranteed during the beta test period.

## Step 1. Create a CVM instance and configure IPv6
1. Log in to a CVM instance in the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) to complete the basic configurations of IPv6.
2. On the CVM instance, run the following commands in sequence to deploy and restart the Nginx service.
```
yum install nginx
service nginx restart
```
3. <span id="check" />Check whether the Nginx service deployed on the CVM instance is listening on IPv6.
   1. Run the following command for check.
```
netstat -tupln
```
![](https://main.qcloudimg.com/raw/5bbe14c9e654b5a451828fa1e4157ac8.png)
   2. Run the following command to open the Nginx configuration file for check.
```
vim  /etc/nginx/nginx.conf
```
![](https://main.qcloudimg.com/raw/ff7718571c02a45f02646ab330c21ee2.png)

## Step 2. Create an IPv6 CLB instance
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/lb).
2. Select options for the following parameters correctly:
 - Billing Mode: Supports pay-as-you-go billing only.
 - Region: select the target region.
 - IP Version: IPv6.
 - Carrier Type: BGP.
 - Network: please select a VPC and subnet that have already obtained IPv6 CIDR.
3. Select various configuration items on the purchase page and click **Buy now**.
4. On the "CLB Instance List" page, select the corresponding region to view the instance just created.
![](https://main.qcloudimg.com/raw/f53a0d3da88b82071960522de6c2fdb8.png)

## Step 3. Create an IPv6 CLB listener
### Configure the HTTP listening protocol and port
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. In the "CLB Instance List", find the created CLB instance and click its ID to enter its details page.
3. In the "Basic Information" module, you can click the modification icon next to the instance name to rename it.
4. In **HTTP/HTTPS Listener** in "Listener Management", click **Create** to create a CLB listener.
![](https://main.qcloudimg.com/raw/301fbda84ff54f2026f79cf7063d3413.png)
5. In the pop-up box, configure the following:
 - Set the name to "IPv6test".
 - Set the listening protocol port to `HTTP:80`.
6. Click **Submit** to create the CLB listener.

### Configure the listener's forwarding rule
1. In "Listener Management", select the new listener IPv6test and click **+** to add a rule.
2. In the pop-up box, configure the domain name, URL path, and balancing method, and click **Next**.
  - Domain Name: the domain name used by your real server, which can contain a wildcard. In this example, `www.qcloudipv6test.com` is used. For more information, please see [Layer-7 Forwarding Domain Name and URL Rules](https://intl.cloud.tencent.com/document/product/214/9032).
  - URL Path: access path of your real server. `/` is used in this example.
  - Select "Weighted Round Robin" for the load balancing mode.
![](https://main.qcloudimg.com/raw/9061484f81b8a09bf194b8e0935d28b9.png)
3. Configure health check: Enable health check, check the default forwarding domain name and path used by the domain name, and click **Next**.
![](https://main.qcloudimg.com/raw/f55355ac26ed08260c631d4e665efbd6.png)
4. Configure session persistence: Enable session persistence, configure the persistence period, and click **Submit**.
![](https://main.qcloudimg.com/raw/e5f710e4dd821a06ef4a6f3d77e0370f.png)

For more information on CLB listeners, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
>?
>- A listener (i.e., listening protocol:port) can be configured with multiple domain names, and a domain name can be configured with multiple URL paths. Select a listener or domain name and click **+** to create a new rule.
>- Session persistence: If session persistence is disabled and a round-robin method is used for scheduling, requests will be assigned to different real servers in sequence; if session persistence is enabled, or it is disabled but ip_hash scheduling is used, requests will always be assigned to the same real server.

### Binding to a CVM
>?Before binding the listener to a CVM instance, please make sure that the CVM instance has obtained an IPv6 address.
>
1. On the "Listener Management" page, select and expand the listener just created and select the domain name and URL path, and the IPv6 information of the CVM instance bound to the URL path will be displayed on the right. Click **Bind**.
2. In the pop-up box, select the CVM instance, set the default Nginx service port to 80, set the weight (10 by default), and click **OK**.
![](https://main.qcloudimg.com/raw/463dfdd5c8bb6772374597673614f2d9.png)
3. After the CVM instance is successfully bound, perform the following:
 - Please check whether the port status is "healthy"; and if yes, please proceed to [Step 4. Test IPv6 CLB](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E6.B5.8B.E8.AF.95-ipv6-.E8.B4.9F.E8.BD.BD.E5.9D.87.E8.A1.A1).
 ![](https://main.qcloudimg.com/raw/1e3fe96b91748271b04f191e7be5a7a6.png)

 - If the port status is "exceptional", please check whether the listener is bound to the correct Nginx server port of the CVM instance, and log in to the CVM instance to check whether the port is normally listening on IPv6. You can perform the check as instructed in [substep 3 in step 1](#check). 
![](https://main.qcloudimg.com/raw/c28a8b4fc331127b8fc5fcc1294f0df9.png)

## Step 4. Test IPv6 CLB
After configuring an IPv6 CLB instance, you can verify whether the architecture takes effect by checking whether different domain names and URLs under a CLB instance can access different real servers, i.e., checking whether the content-based routing feature is available.

Use a client with IPv6 public network access capabilities to access the domain name or IPv6 address of the CLB instance. If it can properly access the web service of the CVM instance, the IPv6 CLB instance is working normally.
1. Go to the [Tencent Cloud DNSPod](https://dnspod.cloud.tencent.com/) to query and register a domain name.
2. Log in to the [DNSPod console](https://console.cloud.tencent.com/cns), click the **domain name** you just purchased, and click **Add Record** on the **Record Management** page to add an AAAA record to the domain name. Enter and save the following content:
   - Host Record: domain name prefix. `www` is used in this example.
   - Record Type: `AAAA record`.
   - Split Zone: Default
   - Record Value: Enter the IPv6 address of the CLB instance.
   - TTL: Leave it as the default value **600s**.
3. After adding the domain name resolution, ping the domain name to verify it.
![]()
4. You can use a browser to access the domain name to verify it,.
![](https://main.qcloudimg.com/raw/77a28d46b830e44db2856b029f5f8697.png)
