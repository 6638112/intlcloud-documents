CCN is currently in beta test. To try it out, please submit an application for approval.


## Resource Limits
The table below lists the limits on the supported CCN resources. 
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of CCN instances per account</td>
<td>5 </td>
</tr>
<tr>
<td>Number of network instances that can be bound to one CCN instance</td>
<td>25 </td>
</tr>
</table>

## Feature Limits
**Non-transferrable with a peering connection**

The presence of a peering connection does not affect the interconnection implemented after a VPC is joined to CCN. CCN only distributes routes to the network instances associated with it for interconnection.
For example, as shown in the figure below, a peering connection has been established between VPC1 and VPC2. After VPC1 is added to a CCN instance, only VPC1 can interconnect with network instances VPC3 and IDC in CCN, while VPC2 can only interconnect with VPC1 through the peering connection but not other instances in CCN.
![Image description](https://main.qcloudimg.com/raw/f764269dbb106d6f6f47bd8470bb3aa5.png)

## Route Limits
To ensure that the interconnection between multiple network instances is smooth, CCN restricts the CIDR blocks of the network instances.

### Limits on VPC CIDR blocks

CCN restricts CIDR blocks at the subnet level: two subnets with identical CIDR blocks in different VPCs cannot interconnect (see below for route validity rules); accordingly, even if the CIDR blocks of two VPCs overlap, as long as their subnets have different CIDR blocks, you can still add them to CCN for interconnection.

### Rules for CIDR overlapping conflict

1. If the CIDR blocks of network instances overlap, only the route of the network instance that is first associated with the CCN instance will take effect.
2. For a network instance already in CCN, if a route conflict occurs due to operations such as subnet creation, the new route will not take effect, and the existing valid route will remain valid.

### Rules for CIDR inclusive conflict

If the CIDR blocks of multiple network instances have an inclusive conflict, only the route of the network instance that is first associated with the CCN instance will take effect. However, you can enable invalid routes in the route table, which, once enabled, will forward data based on the longest mask matching rule.

#### Example of an inclusive conflict
Assume that VPC 1 is first associated with CCN instance A, the CIDR block of its subnet A is `10.0.1.0/20`, and it can interconnect with other network instances in CCN instance A. Then, VPC 2 is associated with CCN instance A, and the CIDR block of its subnet B is `10.0.1.0/24`, which is included in the CIDR block of subnet A in VPC 1. In this case, a CIDR inclusive conflict occurs. As a result, the routing policy of subnet B in VPC 2 will become invalid by default, and VPC 2 cannot interconnect with other network instances in CCN instance A.

However, you can enable this invalid route in the route table of subnet B, which can forward data according to the longest mask matching rule. If the destination IP address of the routing policy is `10.0.1.0/24`, the data will be forwarded to subnet B in VPC 2 based on the rule.




