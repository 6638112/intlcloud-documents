<span id="23"></span>

**Concepts**
- [What is the difference between a layer-4 and a layer-7 CLB instance?](#1)
- [What is the difference between UDP and TCP protocols?](#2)
- [How does CLB achieve session persistence based on cookies?](#3)
- [What is the real server weight?](#4)

**Health Check**
- [What can I do if a CVM instance exception occurs during health check?](#5)
- [Why is the health check too frequent?](#6)

**Access**
- [HTTP redirection in load forwarding](#7)
- [Which TCP ports can load balancing be performed on?](#8)
- [What can I do if no policy file is returned and the connection is directly closed after a policy request (i.e., flash server request) is sent from port 843?](#9)
- [Can CLB instances directly obtain client IPs?](#10)
- [Can a CVM instance forward traffic from port A to another port on the same server by configuring a private network CLB instance?](#11)
- [Does a backend CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?](#12)
- [Notes on compatible versions if the client and server have different HTTP versions](#13)
- [How to configure the security group of a CLB real server? How to configure the access blocklist?](#14)
- [Is the communication between a CLB instance and its real servers over the private or public network?](#15)
- [Description of pinging CLB VIP](#16)
- [Description of running `Telnet` command to connect CLB listening ports](#17)
- [Description of private network loopback](#18)
- [Notes on the scenarios that if a client accesses the same port of a real server via different intermediate nodes, these nodes cannot be specifically determined](#19)
- [I have configured a backend CVM instance with a security group to block access traffic from the public network and only allow that from CLB instances, but why is it not in effect?](#20)
- [I have configured a CLB instance with a listener and bound the listener to a backend CVM instance, but why there is no CLB monitoring information when the domain name is resolved to the IP of the backend CVM instance and the domain name is being accessed?](#21)
- [I have not created an 843 listener, but why I can successfully run the command `Telnet` for connection?](#22)

<span id="1"></span>
### What is the difference between layer-4 and layer-7 load balancing?
- Layer-4 load balancing is based on IPs and ports.
- Layer-7 load balancing is based on application layer information such as HTTP headers and URLs.

The difference between layer-4 and layer-7 instances is whether layer-4 or layer-7 information is used as the basis for determining how to forward traffic for load balancing on real servers.
For example, a layer-4 CLB instance determines which traffic needs load balancing based on the layer-3 IP address (VIP) and layer-4 port number. It performs Network Address Translation (NAT) on the traffic to be processed, and then forwards it to the real server. It also records which server has processed the TCP or UDP traffic, and forwards all subsequent traffic of this connection to the same server for processing.

A layer-7 CLB instance is layer-4 CLB instance combined with application layer features.
For example, CLB instances of the same web server can identify traffic that needs to be processed based on layer-7 URL, browser type, and language in addition to VIP and port 80.
Layer-7 load balancing is also known as "content exchange", in which an internal server is selected based on meaningful application layer content in the message and the server selection method configured on the CLB instance.

To select the server based on the real application layer content, a layer-7 CLB instance must establish a connection (three-way handshake) with the client as a proxy of the final server to receive the message containing real application layer content from the client. It then selects the internal server according to the specific fields in the message and the server selection method configured on the CLB instance. In this case, the CLB instance is more like a proxy server, establishing a TCP connection with the frontend client and the real server respectively.

[[Back to Top]](#23)

<span id="2"></span>
### What is the difference between UDP and TCP?
TCP is a connection-oriented protocol. Before receiving and sending data, TCP requires a reliable connection to be established with the other side. UDP is a message-oriented (connection-less) protocol. It directly sends data packets without performing a three-way handshake with the other side. UDP is suitable for scenarios that focus more on real-timeliness than reliability, such as video chat, real-time push of financial market information, DNS, and IoT.

[[Back to Top]](#23)

<span id="3"></span>
### How does a CLB instance achieve session persistence based on cookies?
In cookie insertion mode, the CLB instance inserts cookies and the real server does not need to make any modifications. When you make the first HTTP request, it (without a cookie) enters the CLB instance, which then selects a real server based on the load balancing algorithm policy and sends the request to the server. The real server then sends an HTTP response (without a cookie) to the CLB instance, which then inserts the cookie and returns the HTTP response (with a cookie) to the client.

When you make the second HTTP request (with the cookie inserted by the CLB instance last time), it enters the CLB instance, which then reads the session persistence values in the cookie and sends the request (with the same cookie as above) to the specified real server. The server gives an HTTP response. Because the server does not write the cookie, the response does not contain the cookie. When the response traffic re-enters the CLB instance, CLB will write the updated session persistence cookie into the response.

[[Back to Top]](#23)

<span id="4"></span>
### What is the real server weight?
You can specify the forwarding weight for each CVM instance in the real server pool, and the instance with a higher weight will be assigned with more access requests. You can configure the weights of the backend CVM instances based on their service capabilities and statuses.

If you have also enabled session persistence, the same access request may be forwarded to different real servers. We recommend temporarily disabling session persistence and then checking whether the problem persists.

[[Back to Top]](#23)

<span id="5"></span>
### What can I do if a CVM instance exception occurs during health check?
Please troubleshoot by following the steps below:
- Make sure that you access your application service directly via the CVM instance.
- Make sure that the relevant port is enabled on the real server.
- Check whether there is any security software like a firewall in the real server. This may cause the CLB instance to be unable to communicate with the real server.
- Check whether the health check parameters of the CLB instance are configured correctly.
- We recommend using static pages for health checks.
- Check whether there is high load on the CVM instance that leads to slow response.
- Make sure that there are no IP restrictions (`iptables`) on the CVM instance.

[[Back to Top]](#23)

<span id="6"></span>
### Why is the health check too frequent?
Health check packets are sent too frequently. Each health check packet is sent every 5 seconds as configured in the console, but the real server receives one or more health check requests in 1 second. The reasons are:

Highly frequent health check relates to the implementation mechanism of CLB health check. Suppose that 1 million requests from clients are distributed to 4 CLB instances before being sent to real servers, and each CLB instance conducts health checks separately. If the CLB instances are configured to send a health check request every 5 seconds, each CLB instance will send a health check request every 5 seconds. This is why the real server receives multiple health check requests. For example, if there are 8 CLB instances in a cluster and each sends a request every 5 seconds, then the real server may receive 8 health check requests in 5 seconds.

The advantages of this implementation scheme are high efficiency, accurate check, and avoidance of mistaken removal. For example, if a CLB instance in the cluster fails, the other 7 CLB instances can still forward traffic normally.

Therefore, if your real server is checked too frequently, you can configure the check interval to be much longer (for example, 15 seconds).

[[Back to Top]](#23)

<span id="7"></span>
### HTTP redirection in load balancing
When you visit the website `http://example.com` via a browser, a redirection to the root directory is required for the server. When you visit the website `http://example.com/` via a browser, the server will directly return the default page of the website's root directory. Similarly, if `http://cloud.tencent.com/movie` is redirected to `http://cloud.tencent.com/movie/` through URL rewriting, entering `http://cloud.tencent.com/movie` will result in an additional URL rewriting process, leading to slight performance degradation and time consumption, but the results are the same. However, if `http://cloud.tencent.com/product` is redirected to a page other than `http://cloud.tencent.com/product/` through URL rewriting, you need to consider whether to add "/" after the secondary URL.

In Tencent Cloud CLB, if the frontend and backend port numbers are different, "/" needs to be added after the secondary URL upon the visit to the secondary page, so as to avoid port number changes after HTTP redirection and ensure normal page access.

Assume that in layer-7 forwarding, port 80 on the CLB instance and port 8081 on the real server are listened to. If the client accesses `http://www.example.com/movie`, the access request is forwarded to the real server via the CLB instance, and the server redirects the request to `http://www.example.com:8081/movie/ ` (listening port is 8081). In this case, the client access fails (port error).

Therefore, we recommend rewriting the access request to a secondary URL with "/", such as `http://www.example.com/movie/ `. This can avoid HTTP redirection, eliminate unnecessary judgment, and reduce unwanted load. If HTTP redirection is required, make sure that the CLB listening port is the same as that of the real server.

[[Back to Top]](#23)

<span id="8"></span>
### Which TCP ports can load balancing be performed on?
You can perform load balancing for the following TCP ports: 21 (FTP), 25 (SMTP), 80 (HTTP), 443 (HTTPS), 1024–65535, etc.

[[Back to Top]](#23)

<span id="9"></span>
### What can I do if no policy file is returned and the connection is directly closed after a policy request (i.e., flash server request) is sent from port 843?
When the CLB instance receives the policy request from port 843, it will return the general cross-domain policy configuration file. If no policy file is returned and the connection is directly closed, the flash server request may be incorrect.

Make sure the correct flash server request is sent: <policy-file-request/>\0.
>! Note: It must end with `\0` and contain 23 bytes. `\0` indicates a character whose ASCII code is 0 and only occupies 1 byte.

The normal result returned by port 843 is as shown below:
![](https://main.qcloudimg.com/raw/69d807250c1e8e00400eade400453620.png)

[[Back to Top]](#23)

<span id="10"></span>
### Can CLB instances directly obtain client IPs?
Public network layer-7 CLB instances use the `X-Forwarded-For` method to get real client IPs. Acquisition of client IPs is enabled on CLB instances by default but needs to be configured on real servers. For more information, please see [Getting Real Client IPs](https://intl.cloud.tencent.com/document/product/214/3728).

Public network layer-4 CLB instances (over TCP) can directly get real client IPs on backend CVM instances, and no additional configuration is required. For the private network layer-4 CLB instances purchased after October 24, 2016, the Source Network Address Translation (SNAT) is not conducted. They can directly get real client IPs from servers with no additional configuration.

[[Back to Top]](#23)

<span id="11"></span>
### Can a CVM instance forward traffic from port A to another port on the same server by configuring a private network CLB instance?
No. To access port a on server A (10.66.\*.101), the request can be forwarded to port b on server B (10.66.\*.102) via a private network CLB instance. But it cannot be forwarded to port b on the same server A (10.66.\*.101).

[[Back to Top]](#23)

<span id="12"></span>
### Does a backend CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?
- Public network bandwidth is not required for the backend CVM instances bound to the CLB instances of any bill-by-IP accounts.
- No traffic or bandwidth fee is charged for the CLB instances of any bill-by-CVM accounts. Any public network traffic fees generated by CLB service will be charged on the bound backend CVM instances. We recommend choosing bill-by-traffic for public network bandwidth when purchasing the backend CVM instance and configuring a reasonable peak bandwidth threshold, so that you do not need to keep track of the fluctuation in total CLB egress traffic. The traffic of internet web business fluctuates considerably and cannot be predicted accurately. When bill-by-bandwidth is selected, it is not cost-effective to purchase excessive bandwidth, yet packet loss may occur during business peaks if insufficient bandwidth is purchased.

[[Back to Top]](#23)

<span id="13"></span>
### Notes on compatible versions if the client and server have different HTTP versions
#### Forwarding compatibility
- On the frontend (client), HTTP/1.0 and HTTP/1.1 and lower versions are supported.
- On the backend (server), Tencent Cloud uses the HTTP/1.0; HTTP/1.0 and HTTP/1.1 and lower versions are supported.

> ! HTTP/2 is only supported in HTTPS but not in HTTP, and backward compatibility is allowed on both the client and server.

#### Gzip compatibility
- On the frontend (client), Gzip is supported by HTTP/1.0, HTTP/1.1 and lower versions. Additional configuration is not needed because mainstream browsers all support Gzip.
- On the backend (server), because HTTP/1.1 is supported on the CVM instance over Tencent Cloud private network, you do not need to make any configuration, and can directly use HTTP/1.1 configured in Nginx by default to achieve compatibility.

> ! HTTP/2 is only supported in HTTPS, but Gzip can be used in any HTTP version supported by Tencent Cloud.
>

[[Back to Top]](#23)

<span id="14"></span>
### How to configure the security group of a CLB real server? How to configure the access blocklist?
#### Configuring the CLB security group
If security group rules have been configured for a real server, the CLB instance may not be able to communicate with the server. Therefore, in layer-4 and layer-7 forwarding, we recommend configuring the security group of a real server as allowing all access requests. If the security group is enabled and accesses from any protocols or IP segments are denied by default, IPs of all clients need to be configured to the security group rules of the server IP.
For some malicious IPs, you can add them to the top rules of the security group to prevent them from accessing the real server. You can then allow access requests from all IPs (0.0.0.0) to the local service port, so normal clients can access the server. Security group rules are arranged in priority order and matched from top to bottom.

If health check has been configured for layer-7 CLB forwarding in VPC, in the real server security rules, the CLB VIP must be allowed. Otherwise, the health check may fail.

#### Configuring the access blocklist
If you need to configure a blocklist for some client IPs to deny their access requests, you can configure the security group associated with the cloud services. The security group rules need to be configured as follows:
>! Follow the steps below strictly in the given order, otherwise the blocklist configuration may fail.

- Add the client IP and port to be rejected into the security group, and select the option in the policy column to reject access from this IP.
- Add another security group rule after completing the above configuration to allow access requests to the port from all IPs by default.
When the configuration completes, the security group rules are as follows:
```
clientA ip+port drop
clientB ip+port drop
0.0.0.0/0+port accept
```

For more information on the security group, please see [Security Group Configuration of the Real Server](https://intl.cloud.tencent.com/document/product/214/6157).

[[Back to Top]](#23)

<span id="15"></span>
### Is the communication between a CLB instance and its real servers over the private or public network?
A CLB instance always communicates with real servers over the private network, even when the bound CVM instances have public IPs.

[[Back to Top]](#23)

<span id="16"></span>
### Description of pinging CLB VIP 
Public network CLB VIP can be pinged. The requests of pinging the CLB VIP are responded to by the CLB cluster and will not be forwarded to real servers. Private network CLB VIP cannot be pinged, for which we recommend running `Telnet` to test private network CLB instances.

[[Back to Top]](#23)

<span id="17"></span>
### Description of running `Telnet` command to connect CLB listening ports
- If layer-4 listeners (TCP, UDP, and TCP SSL) are not bound with real servers after being created, running the command `Telnet` to connect to their listening ports will fail. It will succeed if they are bound with real servers.
- Running the command `Telnet` to connect to listening ports will succeed for layer-7 listeners (HTTP and HTTPS) not bound with real servers, as CLB instances will respond instead.
- For more information about the port 843, please see [CLB Configuration](https://intl.cloud.tencent.com/document/product/214/5411).

[[Back to Top]](#23)

<span id="18"></span>
### Description of private network loopback
For private network CLB instances, a private IP cannot be both the client and server IP. When the CLB instances read the same client and server IPs, access will fail.
If your client needs to be used as a server, please bind at least 2 real servers. CLB has related policies to prevent automatic loopback. When client A accesses the CLB instance, the CLB instance will automatically schedule the request to a real server other than client A.

[[Back to Top]](#23)

<span id="19"></span>
### Notes on the scenarios that if a client accesses the same port of a real server via different intermediate nodes, these nodes cannot be specifically determined.
When a client accesses the same port of a real server via different intermediate nodes at the same time, these nodes cannot be specifically determined. The scenarios are detailed below:
- A client accesses the same port of a real server via layer-4 and layer-7 listeners of the same CLB instance at the same time.
- A client accesses the same port of a real server via different listeners of different CLB instances at the same time.

Specific reason: the CLB instances pass the client IP to the real server, and `client_ip:client_port -> vip:vport -> rs_ip:rs_port` will change to `client_ip:client_port --> rs_ip:rs_port`.
You can add ports to the real server to avoid this problem.

[[Back to Top]](#23)

<span id="20"></span>
### I have configured a backend CVM instance with a security group to block access traffic from the public network and only allow that from CLB instances, but why is it not in effect?
To allow traffic to access a backend CVM instance passing through a CLB instance, the traffic from the public network needs to be allowed both on the backend CVM and CLB security groups. We recommend only allowing the access traffic from a CLB VIP over the public network on the backend CVM security group first, and then allowing public network access IPs on the CLB security group as needed.

[[Back to Top]](#23)

<span id="21"></span>
### I have configured a CLB instance with a listener and bound the listener to a backend CVM instance, but why there is no CLB monitoring information when the domain name is resolved to the IP of the backend CVM instance and the domain name is being accessed?
There will be monitoring information if the domain name is accessed through the CLB instance. You can resolve the domain name to the VIP of the CLB instance and access the domain name to view the CLB monitoring information.

[[Back to Top]](#23)

<span id="22"></span>
### I have not created an 843 listener, but why I can successfully run the command `Telnet` for connection?
The port 843 is opened by default for users to reset the port for Flash access. If you want to close it, you can just do so by not binding any real servers after configuring the `TCP:843` listener.

[[Back to Top]](#23)
