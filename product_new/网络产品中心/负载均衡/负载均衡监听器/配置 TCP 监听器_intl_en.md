## TCP Listener Overview
You can create a TCP listener to a CLB instance to forward TCP requests from the client. TCP is suitable for scenarios that have high requirements for reliability and data accuracy but relatively low requirements for transfer speed, such as file transfer, email messaging, and remote login. For TCP listeners, the real server can directly get the real client IP.

## Prerequisites
You need to [create a CLB instance](http://intl.cloud.tencent.com/document/product/214/6149) first.

## Configuring a TCP Listener
### Step 1. Open the "Listener Management" page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure Listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/376f020caf12788e492e7f7300465ea8.png)
5. The "Listener Management" page is as shown below:
![](https://main.qcloudimg.com/raw/cec2458173b2b16318b14422c96eee26.png)

### Step 2. Configure a listener
Click **Create** in **TCP/UDP Listener** and configure a TCP listener in the pop-up window.
#### 1. Basic configuration
<table>
<thead>
<tr>
<th width="15%">Configuration Item</th>
<th width="70%">Description</th>
<th width="15%">Example</th>
</tr>
</thead>
<tbody><tr>
<td>Name</td>
<td>Listener name</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener protocol and listening port</td>
<td>Listener protocol and listening port. <br><li>Listener protocol: CLB supports various protocols, including TCP, UDP, HTTP, and HTTPS. TCP is used in this example.</li><li>Listening port: A port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listener port must be unique in the same CLB instance.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Balancing method</td>
<td>For TCP listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC). <br><li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

The specific configuration of the created TCP listener is as shown below:
![](https://main.qcloudimg.com/raw/524b3bf6fd376152e3cc7d46d407b93f.png)

#### 2. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Health check can be enabled or disabled. In TCP listeners, CLB instances send SYN packets to the specified server port to perform health checks. | Enabled |
| Response timeout period | <li>Maximum response timeout period for health checks.</li><li>If a real server fails to respond correctly within the timeout period, it is considered abnormal.</li><li>Value range: 2-60s. Default value: 2s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received n times (n is the entered number) in a row are failures, the instance will be considered unhealthy, and the status displayed in the console will be **Abnormal**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| Healthy threshold | <li>If the health check results received n times (n is the entered number) in a row are successes, the instance will be considered healthy, and the status displayed in the console will be **Healthy**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/a222b4ba835564704281f9a72f1f3b5a.png)

#### 3. Session persistence
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Session persistence status | Session persistence can be enabled or disabled. <br><li>If session persistence is enabled, the CLB listener will deliver access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP addresses, i.e., access requests from the same IP address are forwarded to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li> | Enabled |
| Session persistence time | Session persistence time. <br><li>If there is no new request in the connection within the session persistence time, session persistence will be interrupted automatically.</li><li>Value range: 30-3,600s.</li> | 30s |

The specific configuration of session persistence is as shown below:
![](https://main.qcloudimg.com/raw/c074629d85e477f1debf29dba0719899.png)

### Step 3. Bind a real server
1. On the "Listener Management" page, click the created listener `TCP:80` to view the bound real servers on the right of the listener.
![](https://main.qcloudimg.com/raw/3a4dfa05610d1db6c38f6d591da93b38.png)
2. Click **Bind** and select the real server to be bound and configure the server port and weight in the pop-up window.
 1. Add Port: In the "Selected" box on the right, click **Add Port** to add multiple ports for the same CVM instance, such as ports 80, 81, and 82.
 2. Default Port: Enter the "Default Port" first and then select the CVM instance. The port of every CVM instance is the default port.
![](https://main.qcloudimg.com/raw/e0ef33bc1e3de8bd048f22b046dd2d50.png)

After these three steps are completed, the TCP listener rule has been configured as shown below:
![](https://main.qcloudimg.com/raw/c70a8b5b30a7e801b32009b0845c8c0f.png)

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify/delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/b09afd20d73f1f268731fd230f93b70a.png)
