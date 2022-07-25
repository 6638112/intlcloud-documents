TCR Enterprise supports the pay-as-you-go billing mode. You can go to the [TCR Purchase Page](https://buy.intl.cloud.tencent.com/tcr) to purchase a TCR Enterprise instance. Tencent Cloud COS will be used at the same time with the instance and costs will be incurred based on your actual usage.

## Billing Mode for TCR Enterprise
TCR provides the pay-as-you-go billing mode:

|Billing Mode | Payment Method | Billing Unit | Use Cases|
|---------|---------|---------|  |
| Pay-as-you-go | [Freeze the fees](https://intl.cloud.tencent.com/zh/document/product/555/12039) at the time of purchase, and the service is billed at an hourly basis. | USD/hour | The unit price is high. This billing mode is applicable to scenarios such as temporary test. |





## Billable Items for TCR Enterprise
<table>
<tr>
<th>Item</th>
<th>Description</th>
<th>Price</th>
</tr>
<tr>
<td>Instance purchasing</td>
<td>TCR Enterprise instances support pay-as-you-go billing mode. The managed service charges differ according to selected regions and specifications.</td>
td>Please refer to <a href="#price">TCR Enterprise Pricing</a>. </td>
</tr>
<tr>
<td>Storage fees</td>
<td>The cloud native artifacts of the TCR Enterprise managed instance, such as container images and Helm charts, are stored in your COS Bucket. Storage and access fees will apply based on actual usage with the selected COS billing mode. Go to the <a href="https://console.cloud.tencent.com/expense/overview">Billing Center</a> to learn more.
<td>Please refer to <a href="https://intl.cloud.tencent.com/pricing/cos">COS Pricing</a></td>
</tr>
<tr>
<td>Traffic</td>
<td>Using the public network to upload and download the cloud native artifacts such as container images and Helm charts will generate public network traffic fees in COS. <br><b>Note: </b>using the instance synchronization feature for cross-regional synchronization of container images and Helm charts will not generate COS public network traffic fees.</td></td>
<td>Please refer to <a href="https://intl.cloud.tencent.com/pricing/cos">COS Pricing</a></td>
</tr>
</table>

## TCR Enterprise Pricing[](id:price)
You can go to the [TCR Purchase Page](https://buy.intl.cloud.tencent.com/tcr) to view the latest pricing and discounts for the TCR Enterprise instances, and go to the Tencent Cloud or consult your sales rep for more information. The following prices are for reference only. The actual price is based on the purchase period and the latest promotional activities.
>! Please log in to TCR to obtain the accurate price.


### Pay-as-you-go (postpaid) price
<table>
<tbody>
<tr>
<th colspan="2">Region</th><th>Basic (USD/hour)</th><th>Standard  (USD/hour)</th><th>Advanced (USD/hour)</th>
</tr>
<tr><td rowspan="3"> Chinese Mainland Regions</td><td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu and Chongqing</td><td>0.14</td><td>0.28</td><td>0.54</td></tr>
<tr><td>Shenzhen Finance, Shanghai Finance and Beijing Finance</td><td>0.23</td><td>0.42</td><td>0.75</td></tr>
<tr><td>Hong Kong (China), and Taipei (China)</td><td>0.20</td><td>0.38</td><td>0.70</td></tr>
<tr><td rowspan="1">Asia Pacific Regions</td><td>Singapore, Seoul, Tokyo, Mumbai, and Bangkok</td><td>0.20</td><td>0.38</td><td>0.70</td></tr>
<tr><td rowspan="1">Europe and North America Regions</td><td>Toronto, Silicon Valley, Virginia, Frankfurt and Moscow</td><td>0.28</td><td>0.50</td><td>0.87</td></tr>
</tbody></table>


>? TCR is currently unavailable in some regions. To learn more, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

## Specification
The TCR specifications are as follows (**✓**: supported; **-**: not supported).

<dx-alert infotype="notice" title="">
When the instance is using the features of Standard or Advanced edition, it is not allowed to degrade the instance specifications to editions which do not support the features. If you want to degrade the specifications, please delete related feature configurations manually first.
</dx-alert>





<table>
<tbody><tr>
<th rowspan="2" style="
    width: 13%;
">Feature Module</th>
<th rowspan="2" style="
    width: 27%;
">Features</th>
<th rowspan="2" style="
    width: 5%;
">TCR Individual</th>
<th colspan="3" style="
    width: 55%;
">TCR Enterprise</th>
</tr>
<tr>
<th>Basic</th><th>Standard</th><th>Advanced</th>
</tr>
<tr>
<td rowspan="1">Service guarantee</td>
<td>SLA</td>
<td>Not supported</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td>
</tr>
<tr>
<td rowspan="5">Instance management</td>
<td>Dedicated registry service</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated domain name access</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Custom access domain name</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated data storage backend</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Temporary/long-term access credential management</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Repository management</td>
<td>Multi-level repository directory</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Helm chart hosting</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500<br>(you can apply to increase the quota)</td>
</tr>
<tr>
<td>Image repository quota</td><td>Guangzhou region: 500, other regions: 100</td><td>1000</td><td>3000</td><td>5000 <br>(you can apply to increase the quota)</td>
</tr>
<tr>
<td>Helm repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000 <br>(you can apply to increase the quota)</td>
</tr>
<tr>
<td rowspan="7">Data security</td>
<td>Encrypted storage of data</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Image vulnerability scanning</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Image tag protection</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Public network access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access quota</td><td>-</td><td>3</td><td>5</td><td>10</td>
</tr>
<tr>
<td>Operation log retention</td><td>-</td><td>7 days</td><td>15 days</td><td>30 days</td>
</tr>
<tr>
<td rowspan="3">Synchronous backup</td>
<td>Multi-region replications for single instance and nearby access</td>
<td>-</td><td>-</td><td>-</td><td>✓</td>
</tr>
<tr>
<td>Cross-instance custom synchronization rules</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Multi-AZ disaster recovery in the same city</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Container DevOps</td>
</tr>
<tr>
<td>Webhook trigger</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Container image compilation and building *</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud native delivery workflow</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated distribution of images</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

>? **Container image compilation and building** feature is based on CODING DevOps service and provides free usage quota. If you need advanced features or want to add quota, please go to CODING DevOps service.


## Free Usage of TCR Individual
TCR Individual service is provided for individual developers. The free usage quota is limited. SLA commitments and relevant compensation are not provided.
