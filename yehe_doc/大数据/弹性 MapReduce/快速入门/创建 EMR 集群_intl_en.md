## Overview

This document describes how to create an EMR cluster in the EMR console.

## Directions

Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Create Cluster** on the cluster list page.

### 1. AZ and software configuration
- **Billing Mode**: only pay-as-you-go billing is supported.
 - Pay-as-you-go: you are charged by usage duration of the cluster. This billing mode requires identity verification and will freeze the amount of 1 hour's usage fees when the cluster is created (vouchers cannot be used here). After this cluster is terminated, the frozen amount will be returned.
- **Region and AZ**: currently supported regions include Guangzhou, Shanghai, Beijing, Hong Kong (China), Singapore, Silicon Valley, Chengdu, Nanjing, Mumbai, and Moscow. Tencent Cloud products in different regions cannot communicate with each another over a private network.
- **Cluster Type**: there are three types of EMR clusters, namely, Hadoop cluster, ClickHouse cluster, and Druid cluster. You can choose one to deploy as needed.
- **Version and Components**: EMR recommends some commonly used combinations of components for Hadoop. You can also combine the components based on your needs.
- **Hive Metadatabase**: if you choose to deploy the Hive component, there are two storage methods for Hive metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster or associate the metadata with EMR-MetaDB or a self-created MySQL database. In the latter case, metadata will be stored in an associated database and will not be terminated when the cluster is terminated.
 ![](https://main.qcloudimg.com/raw/9957344c29a2a76253fbe3179bdf5090.png)
- **[Kerberos Secure Cluster](https://intl.cloud.tencent.com/document/product/1026/31163)**: it specifies whether to enable Kerberos authentication for the cluster. This feature is not required for individual users and disabled by default.
- **[Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530)**: you can create a cluster by entering custom parameters as required. The external cluster access feature is provided as well, so that you can read/write external cluster data after configuring the correct address information in relevant parameters. You can click the icon next to **Software Configuration** to view instructions.
![](https://main.qcloudimg.com/raw/1f9d7eb49c4647c56c43c6fc2d817915.png)

### 2. Hardware configuration
- **High Availability Cluster**: if you select **Enable High Availability**, 2 master nodes, at least 3 core nodes, and 3 common nodes will be enabled in the Hadoop cluster by default. For more information on node types, please see [Node Type Description](https://intl.cloud.tencent.com/document/product/1026/31094).
- **Hardware Configuration**: node specification configuration. EMR provides a variety of node specifications, and you can choose the node type, core quantity, memory size, and disk type and size based on your business needs.
>?Currently, up to 5 cloud disks in multiple types can be mounted to a core node (one type can be selected only once).
- **Cluster Network**: to ensure security of the EMR cluster, all nodes of the cluster are placed in a VPC; therefore, you need to set up a VPC before you can successfully create the EMR cluster.
![](https://main.qcloudimg.com/raw/0c54dcbc87b1e24bab76a291a8057fa7.png)
![](https://main.qcloudimg.com/raw/f8191b84dcfa90995e694b910c18d982.png)

### 3. Basic configuration
- **Cluster Name**: EMR clusters are differentiated by cluster name.
- **Security Group**: the security group has a firewall feature used to set the network access control of the CVM instance. If there is no security group, EMR will automatically create one for you; otherwise, you can choose to use an existing one directly. If the number of security groups has reached the upper limit and new ones cannot be created, you can delete some obsolete ones after checking the [security groups](https://console.cloud.tencent.com/cvm/securitygroup) that are being used.
 - Create Security Group: EMR will create a security group for you and open ports 22 and 30001 and the necessary IP range for communication over the private network.
 - Select Existing EMR Security Group: select an existing EMR security group as the security group for the current instance and open ports 22 and 30001 and the necessary IP range for communication over the private network.
- **Remote Login**: port 22 is usually used for remote login and opened on the newly created security group by default. You can close it based on your business needs.
- **COS**: after COS is activated, the EMR cluster can directly compute the data stored in COS to implement computation/storage separation and reduce the costs of big data processing. To ensure that EMR can access your data stored in COS, please enter your COS API key.
- **Custom Service Role**: it is used to access Tencent Cloud resources. The service type is **Tencent Cloud Product Service**, and the supported role is **Elastic MapReduce**. To query custom service roles, please go to **CAM**.
- **Placement Group**: it is a policy for distributing and placing CVM instances on the underlying hardware. For more information, please see [Placement Group](https://intl.cloud.tencent.com/document/product/213/15486).
- **Login Method**: currently, EMR provides two ways to log in to cluster services, nodes, and MetaDB: custom password and associated key. SSH keys are only used for logging in to the EMR-UI quick entry. The default username is "root", and the username for the WebUI quick entry of the Superset component is "admin".
- **Add Bootstrap Action**: a bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
- **Tag**: you can add tags to clusters or node resources during resource creation to facilitate resource management. Up to 5 tags can be bound, and the tag key must be unique.
 ![](https://main.qcloudimg.com/raw/cc34a62041e39edcb95224a0c10e4f0b.png)

### 4. Creation completion
After completing the configurations above, click **Purchase** to make the payment. Your EMR cluster will be automatically created once the payment is received. Wait for about 10 minutes and then you will find the cluster you just created in the EMR console.

>!You can view the instance information of each node in the CVM console. To ensure that your EMR cluster works properly, do not modify such configuration information.

## Subsequent Steps
After the cluster is successfully created, you can log in to it accordingly to perform further configuration and other operations on it. For specific operations, please see the following documents:
- Cluster login: [Logging in to Clusters](https://intl.cloud.tencent.com/document/product/1026/31101)
- Cluster configuration: [Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530), [Mounting CHDFS](https://intl.cloud.tencent.com/document/product/1026/35773), and [Unified Management of Hive Metadata](https://intl.cloud.tencent.com/document/product/1026/36299)
- Cluster management: [Setting Tag](https://intl.cloud.tencent.com/document/product/1026/34532), [Bootstrap Actions](https://intl.cloud.tencent.com/document/product/1026/34521), [Cluster Termination](https://intl.cloud.tencent.com/document/product/1026/31106)

