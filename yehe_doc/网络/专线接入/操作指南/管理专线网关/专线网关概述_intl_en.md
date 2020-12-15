A direct connect gateway is a traffic entry for Direct Connect that is used to connect Tencent Cloud VPCs with connections (dedicated tunnels). There are two types: VPC-based direct connect gateway and CCN-based direct connect gateway, which are suitable for different use cases.

## VPC-based Direct Connect Gateway
As shown in the Direct Connect network architecture, dedicated tunnel mode will affect the destination IP range of the IDC routes to Tencent Cloud VPCs. See the following table for details.
<table>
<tr>
<th>Dedicated Tunnel Mode</th>
<th>IDC Routes to Tencent Cloud</th>
</tr>
<tr>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tr>
</table>
For example, if a VPC-based direct connect gateway is used between Tencent Cloud VPCs and a IDC in the Direct Connect network architecture, the routes for different dedicated tunnels are configured as follows:

- For a static dedicated tunnel, the destination IP range of IDC routes to Tencent Cloud VPCs is configured in the local router, such as VPC CIDR block (172.21.0.0/16).
- For a BGP dedicated tunnel, the destination IP range of IDC routes to Tencent Cloud VPCs is the VPC CIDR block (172.21.0.0/16) obtained by the local router based on the BGP protocol.

## CCN-based Direct Connect Gateway
A CCN-based direct connect gateway can associate one CCN with multiple dedicated tunnels to implement the interconnection between VPCs and IDCs. As shown in the Direct Connect network architecture, both the creation time of the direct connect gateway and dedicated tunnel mode will affect the destination IP range of the IDC routes to Tencent Cloud VPCs. See the following table for details.
<table>
<tr>
<th>Creation Time</th>
<th>Dedicated Tunnel Mode</th>
<th>IDC Routes to Tencent Cloud</th>
</tr>
<tr>
<td rowspan="2" >Before 00:00:00 on September 15, 2020</td>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC subnet CIDR block based on the BGP protocol.</td>
</tr>
<tr>
<td rowspan="2" >After 00:00:00 on September 15, 2020</td>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tr>
</table>
In a Direct Connect network architecture, if the direct connect gateways A and B are created before and after September 15, 2020, 00:00:00 respectively, the routes for different dedicated tunnel mode are as follows:

- When both dedicated tunnels are static, the destination IP range of IDC routes to Tencent Cloud VPCs is the VPC CIDR block (172.21.0.0/16) configured in the local router. The direct connect gateways A and B have the same routes and receive local IDC traffic evenly.
- When both dedicated tunnels are BGP, the destination IP range synced from the direct connect gateway A to local router based on the BGP protocol is the subnet CIDR blocks (172.21.0.0/20, 172.21.16.0/20), while that synced from the direct connect gateway B is the VPC CIDR block (172.21.0.0/16). The route with the longest mask will be matched and used for forwarding. Therefore, the local router will forward all traffic to the direct connect gateway A. The traffic will be forwarded to the direct connect gateway B only when the direct connect gateway A fails and loses routes.
>? You can submit a ticket to change the routing policy of the direct connect gateway B to VPC CIDR block or subnet CIDR block.
>
