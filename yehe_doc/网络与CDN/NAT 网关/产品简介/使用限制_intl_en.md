This document describes the usage rules and limits of NAT gateways.

>? NAT Gateway supports TCP, UDP and ICMP, while ESP and AH for the GRE tunnel and IPSec cannot be used for the NAT Gateway, and ALG technologies are not supported. This is specific to NAT Gateway and irrelevant to service providers. Nevertheless, these supported protocols can mostly meet your application demands.

## Use Rules

Note the following when using NAT Gateway:

- After a NAT Gateway is deleted, the associated EIPs are disassociated but not released.
- A NAT Gateway cannot be associated with security groups. However, you can bind security groups to instances within the VPC subnet to control their inbound and outbound traffic.
- The inbound and outbound traffic of the NAT Gateway cannot be directly controlled by the network ACL. Instead, you can use network ACL to control the traffic of the subnet associated with the NAT Gateway.
- You cannot use VPC peering connection or VPN connection to route traffic to a NAT Gateway.
For example, a NAT Gateway enables traffic from VPC1 to the Internet, and VPC1 establishes a peering connection with VPC2. In this case, all the resources within VPC2 can access VPC1, but cannot access the Internet through the NAT Gateway.

## Rule Limits
- When an EIP is disassociated from a NAT gateway, the SANT rule is also deleted if the EIP is the only EIP.
- If the subnet configured for a SNAT rule does not exist, the SNAT rule is deleted as well.
- If the CVM configured for a SNAT rule does not exist, the SNAT rule is also deleted if this is the last CVM; otherwise, the CVM is deleted from the SNAT rule.
- Restricted by standard protocols, for the NAT gateways with the same protocol/destination IP/destination port, the number of maximum connections = the number of bound EIPs × 55000. To increase the number of connections, bind new EIPs or adjust the destination IP/port.

## Service Quota
The following table lists the restrictions on the supported resources for the NAT Gateway. For limits on other VPC resources, see [Quota Limit](https://intl.cloud.tencent.com/document/product/215/38959).
<table>
<tbody>
<tr>
<th >Resource</th>
<th >Limit</th>
</tr>
<tr>
<td >Number of NAT Gateways per VPC</td>
<td >3</td>
</tr>
<tr>
<td >Number of EIPs per NAT Gateway</td>
<td >10</td>
</tr>
<tr>
<td >Maximum forwarding capability per NAT Gateway</td>
<td >5 Gbps</td>
</tr>
<tr>
<td >Maximum number of forwarding rules per NAT Gateway</td>
<td >200</td>
</tr>
<tr>
<td >Number of SNAT rules per NAT Gateway</td>
<td >200</td>
</tr>
<tr>
</tbody></table>
