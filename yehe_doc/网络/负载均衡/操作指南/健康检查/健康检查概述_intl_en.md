CLB instances determine the availability of real servers through health checks, preventing frontend businesses from being affected by real server exceptions and improving the overall availability of businesses.
- If health check is enabled, the CLB instance will always perform health checks on backend CVM instances regardless of their weights (including 0).
 - If a backend CVM instance is abnormal, the CLB instance will automatically forward new requests to other normal CVM instances, and not to the unhealthy one.
 - Once the abnormal CVM instance is recovered, it will be used in the CLB service again and will receive new requests.
 - If all the real servers are checked as abnormal, requests will be forwarded to all backend CVM instances.
- If health check is disabled, the CLB instance will forward traffic to all real servers including those abnormal ones. Therefore, we strongly recommend enabling health check for the CLB instance to automatically check real servers and remove abnormal ones.

## Health Check Status
The health check status description of backend CVM instances is as the following:

| Status | Description | Whether to Forward Traffic |
| ------- | ----------- | ---------------- |
| Detecting | The status of a new backend CVM instance during the period of check interval × healthy threshold. For example, assume the check interval is 2 seconds and the healthy threshold is 3 times, the backend CVM instance remains in this status for 6 seconds. | No. |
| Healthy | The real server is normal. | Yes. |
| Abnormal | The real server is abnormal. |  <li>No.</li><li> Under the layer-4 listener or layer-7 URL rule, if a CLB instance detects that all real servers are unhealthy, it will forward requests to all real servers.</li>|
| Disabled | Health check is disabled. | Yes. |

## TCP Health Check
For layer-4 TCP listeners, you can configure TCP health check to obtain the status of backend CVM instances through SYN packets, i.e., TCP three-way handshake. Also, to this end, you can customize the request and return content of the protocol.
![](https://main.qcloudimg.com/raw/cf6f20300968e1a38c576177d0bbb9ae.png)
TCP health check mechanism is as follows:
1. A CLB instance sends an SYN connection request packet to (the private IP and health check port of) a backend CVM instance.
2. After receiving the SYN request packet, the backend CVM instance will return an SYN-ACK response packet if the port is listening normally.
3. If the CLB instance receives the returned SYN-ACK response packet within the response timeout, it indicates that the real server is normal and the health check result is successful. Then the CLB instance will send the backend CVM instance a TCP Reset (RST) packet to cut the TCP connection.
4. If the CLB instance does not receive the returned SYN-ACK response packet within the response timeout, it indicates that the real server is abnormal and the health check result is failed. Then the CLB instance will send the backend CVM instance a TCP Reset (RST) packet to cut the TCP connection.

## UDP Health Check
For layer-4 UDP listeners, you can configure UDP health check to obtain the status of backend CVM instances by running the Ping command and sending UDP detection packets to the health check port. Also, to this end, you can customize the request and return content of the protocol.
![](https://main.qcloudimg.com/raw/f1337ea9d93269444851722287fada55.png)
UDP health check mechanism is as follows:
1. A CLB instance sends a Ping command to the private IP of a backend CVM instance.
2. Then the CLB instance sends a UDP detection packet to the (private IP and health check port of the) backend CVM instance.
3. If the Ping command succeeds and the backend CVM instance does not return the error `port XX unreachable` within the response timeout, it indicates that the real server is normal and the health check result is successful.
4. If the Ping command fails or the backend CVM instance returns the error `port XX unreachable` within the response timeout, it indicates that the real server is abnormal and the health check result is failed.

>!
1. UDP health checks are based on ICMP, therefore, backend CVM instances need to be allowed to reply ICMP packets (i.e., Ping command is supported) and ICMP "port unreachable" packets (i.e., the port can be detected).
2. If a Linux server is used as the backend CVM instance, the speed of the server to send ICMP packets will be limited during high concurrency as the Linux server has a mechanism of defending itself from ICMP attacks. In this case, although the real server is abnormal, it cannot return the error `port XX unreachable` to the CLB instance. Then the CLB instance will determine that the health check result is successful, so the actual status of the real server cannot be returned.
Solution: You can configure the UDP health check with custom input and output strings. So in a health check, the custom input string will be sent to the real server, and the result will be determined as successful only after the CLB instance receives the custom response string. This method is based on the real server, which needs to process the health check input string and return the custom output string.

## <span id="http"></span>HTTP Health Check
For layer-4 TCP listeners and layer-7 HTTP/HTTPS listeners, you can configure HTTP health check to obtain the status of backend CVM instances by sending HTTP requests.
![](https://main.qcloudimg.com/raw/05b201f2ae815fbe4ba215add02593c0.png)
HTTP health check mechanism is as follows:
1. According to the health check configuration, a CLB instance can send HTTP requests (with the target domain name specified) to (the private IP, health check port, and check path of) a backend CVM instance.
2. After receiving the request, the backend CVM instance will return the corresponding HTTP status code.
3. If the CLB instance receives the returned HTTP status code within the response timeout and the HTTP status code matches the set one, it indicates that the health check result is successful, otherwise, failed.
4. If the CLB instance does not receive the response from the backend CVM instance within the response timeout, it indicates that the health check result is failed.

>? For layer-7 HTTPS listeners, if HTTP is selected as the backend protocol of the HTTPS listener's forwarding rules, HTTP health check will be conducted; if HTTPS is selected, HTTPS health check will be conducted.
HTTPS health checks are basically the same as <a href="#http">HTTP health checks</a>. The difference is that in HTTPS health checks, HTTPS requests are sent and the backend CVM instance status is determined by the returned HTTPS status code.
>
## Health Check Time Window
CLB health check mechanism improves business availability, but frequent health check failures can cause unnecessary server switches, compromising system availability. Therefore, health check status can be switched between healthy and abnormal only if the results are being the same in a health check time window for several times. The health check time window is based on the factors below:
<table>
<tr>
<th>Health Check Configuration</th>
<th>Description</th>
<th>Default Value</th>
</tr>
<tr>
<td>Response timeout</td>
<td><ul><li>Maximum response timeout for a health check.</li><li>If a real server fails to respond within the timeout, it is considered as abnormal.</li><li>Value range: 2-60 seconds.</li></ul></td>
<td>2 seconds</td>
</tr>
<tr>
<td>Check interval</td>
<td><ul><li>Interval between two health checks.</li><li>Value range: 5-300 seconds.</li></ul></td>
<td>5 seconds</td>
</tr>
<tr>
<td>Unhealthy threshold</td>
<td><ul><li>If the health check result is failed for n (a customizable value) times, it is considered that the backend CVM instance is unhealthy, and the status displayed in the console is **Abnormal**.</li><li>Value range: 2-10 times.</li></ul></td>
<td>3 times</td>
</tr>
<tr>
<td>Healthy threshold</td>
<td><ul><li>If the health check result is successful for n (a customizable value) times, it is considered that the backend CVM instance is healthy, and the status displayed in the console is **Healthy**.</li><li>Value range: 2-10 times.</li></ul></td>
<td>3 times</td>
</tr>
</table>

The calculations of **layer-4 health check time window** are as follows:
>?Layer-4 health check, namely the TCP health check or UDP health check, the time interval between two checks is the set value, no matter the result is successful or whether the response times out.
>
- Time window of a health check with a failed result = Check interval × (Unhealthy threshold - 1)
In the example below, the health check response timeout is 2 seconds, check interval is 5 seconds, and the unhealthy threshold is 3 times, so the time window of a health check with a failed result = 5 x (3-1) = 10 seconds.
![](https://main.qcloudimg.com/raw/7fc4163c89513d99c3d45e2af2dba2c9.png)
- Time window of a health check with a successful result = Check interval × (Healthy threshold - 1)
In the example below, the period of a successful health check response is 1 second, check interval is 5 seconds, and the healthy threshold is 3 times, so the time window of a health check with a successful result = 5 x (3-1) = 10 seconds.
![](https://main.qcloudimg.com/raw/62453871d0485d82cccf6f9dbbee00ed.png)

The calculations of **layer-7 health check time window** are as follows:
- Time window of a health check with a failed result = Response timeout × Unhealthy threshold + Check interval × (Unhealthy threshold - 1)
In the example below, the health check response timeout is 2 seconds, check interval is 5 seconds, and the unhealthy threshold is 3 times, so the time window of a health check with a failed result = 2 x 3 + 5 x (3-1) = 16 seconds.
![](https://main.qcloudimg.com/raw/44261e232878486de7e7d84c6e9c4768.png)
- Time window of a health check with a successful result = Period of a successful health check response × Healthy threshold + Check interval × (Healthy threshold -1)
In the example below, the period of a successful health check response is 1 second, check interval is 5 seconds, and the healthy threshold is 3 times, so the time window of a health check with a successful result = 1 x 3 + 5 x (3-1) = 13 seconds.
![](https://main.qcloudimg.com/raw/394261592166455a2cee02dcba41dbb3.png)
