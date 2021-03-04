>? This document introduces the updates to Tencent Container Registry (TCR) Enterprise Edition. For more information about the updates to Tencent Kubernetes Engine (TKE), see [Release Notes](https://intl.cloud.tencent.com/document/product/457/37358).

## January 2021
<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Added support for multi-region replication of a single instance.</td><td>Users can create replicas of an Enterprise Edition instance in multiple regions with the same access domain name and credential as the original Enterprise Edition instance and synchronize underlying image data of the original instance to replicas in real time. After image data is uploaded, it can be downloaded through the local private network in multiple regions.</td><td>Configuring Instance Replication</td></tr>
	<tr><td>Added support for cloud-native artifacts and multi-architecture images.</td><td>Enterprise Edition instances are compatible with cloud-native artifacts (OCI). Image Registry can host Helm charts, CNAB, and other cloud-native artifacts. Enterprise Edition instances can host multi-architecture container images, such as amd64 and arm, for us in IoT and edge computing scenarios.</td><td>-</td></tr>
	<tr><td>Added support for on-demand container image loading.</td><td>An Enterprise Edition instance can enable the on-demand container image loading feature. When cluster nodes pull image data from the Enterprise Edition instance, they can mount pulled data as needed, improving the container startup speed.</td><td>-</td></tr>
	<tr><td>Optimized the private network access feature.</td><td>When a private network access link is created for an instance deployed in China, the VPCDNS can be used to configure private network resolution for the instance access domain name, avoiding the need to use a self-built DNS or configure the host.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35492">Private Network Access Control</a></td></tr>
</table>
## December 2020

<table>
<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
<tr><td>Started commercial billing for TCR Enterprise Edition.</td><td>Enterprise Edition instances have ended beta testing and will be billed. SLA guarantees are provided, and users can purchase instances in pay-as-you-go mode.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td></tr>
<tr><td>Added support for the Virginia and Frankfurt regions.</td><td>TCR Enterprise Edition is now available in the Virginia and Frankfurt regions. For more information about billing, see the Billing Overview.</td><td><ahref="https://intl.cloud.tencent.com/document/product/1051/35483">Billing Overview</a></td></tr>
</table>

## October 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Added support for multiple code sources in the image building feature.</td><td>The private GitLab and TGit code sources are now supported, and the code source authorization process has been optimized. </td><td><a href="https://intl.cloud.tencent.com/document/product/1051/37252">Configuring Image Building</a></td></tr>
	<tr><td>Added support for image filtering in the delivery assembly line deployment feature.</td><td>Local push images can be used to trigger the deployment process, and filtering rules can be configured to deploy only the most recently pushed images that meet the rules.</td><td>Using the Delivery Assembly Line to Implement Container DevOps</td></tr>
</table>

## September 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Added the image tag retention feature.</td><td>Automatic clearing rules can be configured for image tags in a namespace to periodically clear historical image tags. </td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38942">Configuring Image Tag Retention</a></td></tr>
</table>


## August 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Added support for the TCR plug-in for TKE.</td><td>A TKE cluster can install the TCR Enterprise Edition plug-in with one click to enable secret-free pulling of container images and Helm charts through the private network. This significantly improves the application deployment experience.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38386">TKE Clusters Use the TCR Plug-In to Enable Secret-Free Pulling of Container Images Through the Private Network</a></td></tr>
  <tr><td>Added support for Tencent Cloud tags.</td><td>Users can now bind Enterprise Edition instances with Tencent Cloud tags, with which they can perform instance resource filtering and permission management.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35486">Creating an Enterprise Edition Instance</a></td></tr>
</table>

## July 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Launched the delivery assembly line feature.</td><td>After a delivery assembly line is configured, code updates can automatically trigger image building, image push, and application updates. When used with TKE, this feature can quickly implement container DevOps.</td><td>Using the Delivery Assembly Line to Implement Container DevOps</td></tr>
  <tr><td>Updated the Helm chart feature.</td><td>Users can upload and download chart packages through the console. TKE can use TCR private Helm repositories for application deployment.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35493">Managing Helm Charts</a></td></tr>
</table>

## June 2020

<table>
	<tr><th style="width: 25%;">Update</th><th style="width: 50%;">Description</th><th style="width: 25%;">Document</th></tr>
	<tr><td>Started full beta testing for the TCR Enterprise Edition.</td><td>The TCR Enterprise Edition officially began full beta testing. Users can create secure and exclusive Enterprise Edition instances and use image security scanning, cross-region instance synchronization, and Helm chart hosting.</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/35480">TCR Product Overview</a></td></tr>
</table>
