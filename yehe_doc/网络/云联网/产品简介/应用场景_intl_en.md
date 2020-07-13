## Scenario 1. Building a Hybrid Cloud
#### Scenario description
You have business VPC and disaster recovery VPC in the cloud as well as self-built IDC off the cloud and you want to achieve resource interconnection.

#### Solution
Multiple cloud IDCs can be built in Tencent Cloud and then connected to local IDCs through Direct Connect lines, creating a hybrid cloud that enables cloud-based disaster recovery and elastic business deployment. 
After creating a CCN instance, you only have to join the Direct Connect gateway connecting the IDC, elastic business VPCs and backup IDC to the instance, eliminating the need to create multiple peering connections and dedicated tunnels, and generating routes automatically to significantly simplify configuration.
Outcomes:
- There is no need to create multiple peering connections for interconnecting multiple VPCs. Once they are joined to CCN, the routes are automatically distributed with no repeated operations required.
- Direct Connect gateway can be joined to CCN and multiple VPCs can be connected through one dedicated tunnel, meeting your needs for interconnection between local IDC and cloud data.

![](https://main.qcloudimg.com/raw/d3f95cbed44e0fc8cb29692c259d2985.svg)

## Scenario 2. Online Education
#### Scenario description
In online education scenarios, teachers and students are located all over the world and there are many VPCs. To interconnect them one by one through peering connection, it requires the creation of many connections. In addition, live broadcasting platforms for online education are required to build high-quality interconnection covering multiple regions so as to ensure clear audio and video communications during cross-regional transfer.

#### Solution
Based on CCN's coverage in over 20 regions around the globe, POP access VPCs in multiple regions can be joined to CCN with easy operations and management; leveraging the intelligent full-mesh scheduling capability, any two points can be interconnected through the shortest path on the private network with no public network bypassing and link congestion, providing global multi-point interconnection with reduced latency. 
Outcomes:
- Teachers and students have local access to the services with high transfer quality and low delay guaranteed.
- Once joined to CCN for the first time, the VPCs in different regions can interconnect with all instances without having to set up connections one by one.

![](https://main.qcloudimg.com/raw/e54118915b4ab0690980b7905b25fd1b.svg)

## Scenario 3. Gaming Acceleration
#### Scenario description 
Online games typically have players all over the world who need to access latency-sensitive services. It requires the deployment of multiple servers in many regions to enable local assess for players and meet their gaming needs in scenarios such as cross-server PVP battles.
#### Solution 
Based on CCN's coverage in over 20 regions around the globe, POP access VPCs in multiple regions can be joined to CCN with easy operations and management; based on full-mesh network topology and monitoring of routing and real-time bandwidth and with no public network bypassing or link congestion, CCN uses an intelligent scheduling system to achieve low-latency interconnection, allowing global players to battle on the same servers for an ultimate gaming experience. 
Outcomes:
- Players have local access to the service VPCs with low latency.
- Full-mesh topology supports multi-region VPC joining for building a global network.

![](https://main.qcloudimg.com/raw/1af02ff907b2eb9cea38a05b2a27b8e7.svg)
