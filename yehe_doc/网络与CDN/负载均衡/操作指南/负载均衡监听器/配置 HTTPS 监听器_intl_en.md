You can create an HTTPS listener to a CLB instance to forward HTTPS requests from the client. HTTPS is suitable for HTTP applications where data transfer needs to be encrypted.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first.

## Directions

### Step 1. Configure a listener
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the CLB instance list page and click **Configure Listener** in the **Operation** column on the right.
![]()
3. Under **HTTP/HTTPS Listener**, click **Create** and configure the HTTPS listener in the **Create Listener** pop-up window.
**a. Listener creation**
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
<td>Listener name.</td>
<td><span>test-https-443</span></td>
</tr>
<tr>
<td>Listener Protocol and Ports</td>
<td>
<ul><li>Listener protocol: HTTPS is used in this example.</li><li>Listener port: a port used to receive requests and forward them to the real server. Port range: 1-65535. Ports 843, 1020, 1433, 1434, 3306, 3389, 6006, 20000, 36000, 42222, 48369, 56000, and 65010 are system reserved ports and cannot be opened.</li><li>The listener port must be unique in the same CLB instance.</li></ul></td>
<td>HTTPS:443</td>
</tr>
<tr>
<td>Enable Persistent Connection</td>
<td>Once this feature is enabled, persistent connections will be used between CLB and real server, and CLB will no longer pass through the source IP, which can be obtained from XFF. To ensure normal forwarding, enable the "Allow by default" feature in the CLB security group or allow `100.127.0.0/16` in the CVM security group.</td>
<td><span>Existing certificate</span></td>
</tr>
<tr>
<td>Enable SNI</td>
<td>If SNI is enabled, multiple domain names of a listener can be configured with different certificates; if it is disabled, multiple domain names of a listener can be configured with one certificate only.</td>
<td><span>Disabled</span></td>
</tr>
<tr>
<td>SSL parsing method</td>
<td>One-Way authentication and mutual authentication are supported. CLB takes over the overheads of SSL encryption and decryption to guarantee the access security.</td>
<td><span>One-Way authentication</span></td>
</tr>
<tr>
<td>Server certificate</td>
<td>You can select an existing certificate in the <a href="https://console.cloud.tencent.com/ssl">SSL Certificates Service</a> or upload a certificate</td>
<td><span>One-Way authentication</span></td>
</tr>
</tbody>
</table>
 <b>b. Forwarding rule creation</b>
 <table>
<tr>
<th>Forwarding Rule Configuration</th>
<th>Description</th>
<th>Example</th>
</tr>
<tr>
<td>Domain name</td>
<td>Forwarding domain name: <ul style="margin-bottom:0px;"><li>Length: 1 - 80 characters. </li><li>Underscores (_) cannot be the first character. </li><li>Exact and wildcard domain names are supported. </li><li>Regex is supported. </li><li>For detailed configuration rules, see <a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules</a>.</li></ul></td>
<td>www.example.com</td>
</tr>
<tr>
<td>Default Domain Name</td>
<td><li>If all domain names of the listener are not matched, the system will direct requests to the default domain name, making default access controllable. </li><li>Each listener can be configured with one default domain name only.</li></td>
<td>Enabled</td>
</tr>
<tr>
<td>HTTP 2.0</td>
<td>After HTTP 2.0 is enabled, CLB instances can receive HTTP 2.0 requests. CLB instances access real servers over HTTP 1.1 no matter what HTTP version the client uses to access CLB instances.</td>
<td>Enabled</td>
</tr>
<tr>
<td>URL Path</td>
<td>Forwarding URL path: <ul style="margin-bottom:0px;"><li>Length: 1 - 200 characters. </li><li>Regex is supported. </li><li>For detailed configuration rules, see <a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules</a>.</li></ul></td>
<td>/index</td>
</tr>
<tr>
<td>Balancing method</td>
<td>For HTTPS listeners, CLB supports three scheduling algorithms: weighted round robin (WRR), weighted least connections (WLC), and IP hash.<ul style="margin-bottom:0px;"><li>WRR: requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <b>number of new connections</b>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li><li>IP hash: hash keys are used to locate the corresponding servers in the static hash table based on the source IPs of requests. If a server is available and not overloaded, requests will be delivered to it; otherwise, a null value will be returned.</li></ul></td>
<td>WRR</td>
</tr>
<tr>
<td>Backend protocol</td>
<td>Backend protocol is deployed between a CLB instance and a real server: <ul style="margin-bottom:0px;"> <li>If HTTP is selected as the backend protocol, HTTP service should be deployed on the real server.</li><li>If HTTPS is selected as the backend protocol, HTTPS service should be deployed on the real server, and the encryption and decryption of the HTTPS service will consume more resources on the real server.</li></ul></td>
<td>HTTP</td>
</tr>
<tr>
<td>Getting Client IP</td>
<td>Enabled by default.</td>
<td>Enabled</td>
</tr>
<tr>
<td>Gzip Compression</td>
<td>Enabled by default.</td>
<td>Enabled</td>
</tr>
</table>
 <b>c. Health check</b>
For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/39251">Health Check Configuration</a>.</br> 
 <b>d. Session persistence</b>
<table>
<tr>
<th>Session Persistence Configuration</th>
<th>Description</th>
<th>Example</th>
</tr>
<tr>
<td>Session Persistence Switch</td>
<td><ul><li>After session persistence is enabled, CLB listener will distribute access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP address. The access requests from the same IP address are forwarded to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li></ul></td>
<td>Enabled</td>
</tr>
<tr>
<td>Session Persistence Duration</td>
<td><ul><li>If there is no new request within the connection beyond the session persistence duration, session persistence will be disabled automatically.</li><li>Value range: 30-3600s.</li></ul></td>
<td>30s</td>
</tr>
</table>


### Step 2. Bind a real server
1. On the **Listener Management** page, select the created listener `HTTPS:443`. Click **+** on the left to expand the domain names and URL paths, select the desired URL path, and view the real servers bound to the path on the right of the listener.
2. Click **Bind**, select the target real server, configure the server port and weight in the pop-up window.
>? Default port: enter the **Default Port** first and then select the CVM instance. The port of every CVM instance is the default port.
>

### Step 3. Configure a security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 4. Modify and delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the **Listener Management** page and click ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) for modification or ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) for deletion.
