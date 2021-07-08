## Overview
A [security group](https://intl.cloud.tencent.com/zh/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For specific rules and limitations, please see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750).

>?
>- TencentDB for MySQL security groups currently only support network access control for VPCs and public networks but not the classic network.
>- TencentDB security groups in the Frankfurt, Silicon Valley, Singapore regions currently do not support public network access control.
>- As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
>- TencentDB for MySQL security groups support source and read-only instances.
>- Security groups are not supported for basic single-node TencentDB for MySQL instances.


## Configuring Security Groups for TencentDB
### Step 1. Create a security group
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region, and click **New**.
3. In the pop-up dialog box, configure the following items and click **OK**.
 - **Template**: select a template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
	<tr><th>Template</th><th>Description</th><th>Remarks</th></tr>
	<tr><td>Open all ports</td><td>All ports are open. May present security issues.</td><td>-</td></tr>
	<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This template does not take effect for TencentDB.</td></tr>
	<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, please see "Step 2. Add a security group rule"</a> below.</td><td>-</rd></tr>
</table>
 - **Name**: name of the security group.
 - **Project**: select a project for easier management. By default, **DEFAULT PROJECT** is selected.
 - **Notes**: a short description of the security group for easier management.


### Step 2. Add a security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click **Modify Rule** in the **Operation** column on the row of the security group for which to configure a rule.
2. On the security group rule page, click **Inbound rule** > **Add Rule**.
3. In the pop-up dialog box, set the rule.
 - **Type**: **Custom** is selected by default. You can also choose another system rule template, such as MySQL(3306).
 - **Source** or **Target**: traffic source (inbound rules) or target (outbound rules). You need to specify one of the following options:
<table>
	<tr><th>Source or Target</th><th>Description</th></tr>
	<tr><td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
	<tr><td>A single IPv6 address or an IPv6 range</td><td>In CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</td></tr>
	<tr><td>ID of referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul>
</td><td><ul  style="margin: 0;"><li>To reference the current security group, please enter the ID of security group associated with the CVM.</li><li>You can also reference another security group in the same region and the same project by entering the security group ID.</li></ul>
</td></tr>
	<tr><td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - **Protocol Port**: enter the protocol type and port range or reference a protocol/port or protocol/port group in a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).
  >?To connect to TencentDB for MySQL, port 3306 must be opened.
 - **Policy**: **Allow** or **Reject**. **Allow** is selected by default.
    - **Allow**: traffic to this port is allowed.
    - **Reject**: data packets will be discarded without any response.
 - **Notes**: a short description of the rule for easier management.
4. Click **Complete**.

#### Use case
**Scenario:** you have created a TencentDB for MySQL instance and want to access it from a CVM instance.
**Solution:** when adding security group rules, select MySQL(3306) in **Type** to open port 3306.
You can also set **Source** to all or specific IPs (IP ranges) as needed to allow them to access TencentDB for MySQL from a CVM instance.

| Inbound or Outbound   | Type   | Source                                                    | Protocol and Port | Policy |
|---------|---------|---------|---------|---------|
| Inbound | MySQL(3306) | All IPs: 0.0.0.0/0 <br>Specific IPs: specify IPs or IP ranges | TCP:3306 | Allow |


### Step 3. Configure a security group
A security group is an instance-level firewall provided by Tencent Cloud for controlling inbound traffic of TencentDB. You can associate a security group with an instance when purchasing it or later in the console.

>!Currently, security groups can be configured only for **TencentDB for MySQL instances in VPC**.

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Security Group** tab, click **Configure Security Group**.
3. In the pop-up dialog box, select the security group to be bound and click **OK**. 

## Importing Security Group Rules
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click the ID/name of the desired security group.
2. On the inbound rule or outbound rule tab, click **Import Rule**.
3. In the pop-up dialog box, select an edited inbound/outbound rule template file and click **Import**.
>? As existing rules will be overwritten after importing, we recommend that you export the existing rules before importing new ones.

## Cloning Security Groups
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, locate the desired security group and click **More** > **Clone** in the **Operation** column.
2. In the pop-up dialog box, select the target region and target project, enter the new security group name, and click **OK**. If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

## Deleting Security Groups
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, locate the security group to be deleted and click **More** > **Delete** in the **Operation** column.
2. Click **OK** in the pop-up dialog box. If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.

