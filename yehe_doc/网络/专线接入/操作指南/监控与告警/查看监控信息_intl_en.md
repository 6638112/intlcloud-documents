You can view the network monitoring data of a connection or dedicated tunnel via the console or an API to facilitate the troubleshooting. To use the API, see [Connection Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/10994).

## Directions
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/vpc/dc) console.
2. Perform the following steps to view the network monitoring data of a connection.
 1. Click **Connections** on the left sidebar.
 2. Locate the target connection and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png"  > in the **Monitoring** column.
  > ?Only the monitoring data of operating connections can be viewed.
 3. The **Monitoring** page displays **Network Outbound Bandwidth**, **Network Inbound Bandwidth**, **Packet Loss**, and **Packet Error**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
      - **Network Outbound Bandwidth**: average outbound traffic of the connection per second.
      - **Network Inbound Bandwidth**: average inbound traffic of the connection per second.
      - **Packet Loss**: number of packets discarded on the port per second.
      - **Packet Error**: number of packet errors on the port per second.
 ![](https://main.qcloudimg.com/raw/7309063e57b0df6654c308f36a2fa57d.png)
3. Perform the following steps to view the network monitoring data of a dedicated tunnel.
 1. Click **Dedicated Tunnels** on the left sidebar.
 2. Locate the target dedicated tunnel and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png"  > in the **Monitoring** column.
 3. The **Monitoring** page displays **Network Outbound Bandwidth**, **Network Inbound Bandwidth**, **Packets Out**, and **Packets In**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
      - **Network Outbound Bandwidth**: average outbound traffic of the dedicated tunnel per second.
      - **Network Inbound Bandwidth**: average inbound traffic of the dedicated tunnel per second.
      - **Packets Out**: average outbound packets of the dedicated tunnel per second.
      - **Packets In**: average inbound packets of the dedicated tunnel per second.
 ![](https://main.qcloudimg.com/raw/feba7fdd174ec84fc08e78b86777dfcc.png)
4. Perform the following steps to view the network monitoring data of a direct connect gateway.
 1. Click **Direct Connect Gateway** on the left sidebar.
 2. Locate the target direct connect gateway and click <img width="3%" src="https://main.qcloudimg.com/raw/52d8549cc2412c6527f332a3b88be44d.png" > in the **Monitoring** column.
 3. The **Monitoring** page displays **Network Outbound Bandwidth**, **Network Inbound Bandwidth**, **Packets Out**, and **Packets In**, **Outbound Traffic**, and **Inbound Traffic**. Select **Last 24 hours**, **Last 7 days** or a custom time period to display the monitoring data accordingly.
    - **Network Outbound Bandwidth**: average outbound traffic of the direct connect gateway per second.
    - **Network Inbound Bandwidth**: average inbound traffic of the direct connect gateway per second.
    - **Packets Out**: average outbound packets of the direct connect gateway per second.
    - **Packets In**: average inbound packets of the direct connect gateway per second.
    - **Outbound Traffic**: total outbound traffic of all dedicated tunnels associated with the direct connect gateway.
    - **Inbound Traffic**: total inbound traffic of all dedicated tunnels associated with the direct connect gateway.
![](https://main.qcloudimg.com/raw/0567ea3d423edd4eecee6c083b20c249.png)
