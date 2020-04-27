## Problem Description
Scaling operations may fail due to many reasons. If this happens, troubleshooting in a timely manner can ensure the correct execution of scaling operations.
View the status of the target scaling group in the [scaling group list](https://console.cloud.tencent.com/autoscaling/group). If <img style="margin:-3px 0;" src="https://main.qcloudimg.com/raw/df9771a6e2211e3f418ce257051313c3.png"> appears, the last scaling of the scaling group has failed.
>Hover the cursor over the icon to view the cause of the exception.
>


## Problem Analysis
### Viewing the cause
Tencent Cloud AS provides the industry’s most intelligent method for viewing the cause of failed scaling group operations. Complete the following steps to view the details of a failure:
1. Click the ID of the scaling group failed to be scaled in the [scaling group list](https://console.cloud.tencent.com/autoscaling/group).
2. On the details page of the scaling group, click **Scaling Activity** to view details, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f6a022c51ec8ed3931efd5b7d3902aad.png)

### Troubleshooting based on the reasons
Troubleshoot the problems based on the cause of the failure as instructed below. Common causes of scaling failures are as follows:


### Causes of scaling failures
The causes of scaling failures are classified into the following types:
 - [CVM issues](#cvm)
 - [Image issues](#mirror)
 - [Network issues](#net)
 - [CBS issues](#cbs)
 - [CLB issues](#load)
 - [Other issues](#other)
 

 


## Troubleshooting

<span id="cvm"></span>
### CVM issues
#### The CVM is sold out
Cause: the specified resource inventory is insufficient.
Solution: configure multi-model in the launch configuration, and select another instance specification and availability zone as needed.

#### The CVM model is invalid in the current availability zone
Cause: the specified instance specification is deprecated.
Solution: select an available instance specification in the launch configuration. For more information, see [Instance Specifications](https://intl.cloud.tencent.com/document/product/213/11518).

#### Invalid pairing of the CVM and CBS cloud disk
Cause: the current system disk type does not support the instance model.
Solution: check the scaling configuration and change the system disk type. We recommend that you select premium cloud storage or SSD disks.

#### The CVM instance purchase quota is insufficient
Cause: each user is assigned a CVM purchase quota. For the default quota of pay-as-you-go CVM instances, see [Purchase Limits for Pay-as-You-Go CVM Instances](https://intl.cloud.tencent.com/document/product/213/2664).
Auto scaling does not work for CVMs when this quota is exceeded.
Solution: decrease the number of CVMs for scale-out, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for an increased quota.

#### The CVM model does not exist
Cause: the model specified in the launch configuration is incorrect or deprecated.
Solution: modify the launch configuration.

<span id="mirror"></span>
### Image issues
#### The image does not exist
Cause: the image does not exist or is invalid.
Solution: check the corresponding setting in the launch configuration.

#### The image size exceeds the capacity of the system disk
Cause: the system disk capacity is less than the image size.
Solution: check the launch configuration and increase the system disk capacity or use another image with a smaller size.

<sapn id="net"></span>
### Network issues
#### Only VPC is supported
Cause: the model selected in the launch configuration only supports VPC.
Solution: do not use the model on the basic network. Deselect the model in the launch configuration.

#### The number of IP addresses in the subnet of the VPC is less than the number of instances to be scaled out
Cause: the number of IP addresses in the VPC subnet is limited.
Solution: create a subnet and increase the range of the IP range (CIDR block).


<sapn id="cbs"></span>
### CBS issues
#### CBS cloud disks are sold out
Cause: the specified resource inventory is insufficient.
Solution: enable the default disk feature in the launch configuration.



#### Invalid pairing of the CVM and CBS cloud disk
Cause: the current system disk type does not support the instance model.
Solution: check the scaling configuration and change the system disk type. We recommend that you select premium cloud storage or SSD disks.

<sapn id="load"></span>
### CLB issues
#### The CLB does not exist
Cause: the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure that the status of the CLB instance associated with the scaling group is normal.


#### The listener cannot be detected
Cause: the listener in the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure that the status of the CLB instance associated with the scaling group is normal.

#### The forwarding path does not exist
Cause: the forwarding domain name or URL of the listener in the CLB does not exist or is invalid. Check the relevant configurations in the CLB.
Solution: ensure that the status of the CLB instance associated with the scaling group is normal.

#### The specified CLB is busy
Cause: a CLB task is ongoing.
Solution: reduce manual operations for a scaling group during scaling to avoid mutual operation exclusion.

<sapn id="other"></span>
### Other issues
#### The lifecycle action is abandoned
Cause: a lifecycle hook for scale-out is configured for the scaling group. The hook is triggered during the scale-out of the scaling group and is finally rejected. As a result, the scaling operation is rolled back, and the scaled-out instance is released.
Solution: check the execution policy of the lifecycle hook.
