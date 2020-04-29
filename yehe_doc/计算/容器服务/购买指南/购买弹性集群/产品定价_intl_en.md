Elastic Kubernetes Service (EKS) bills a pod by multiplying the [resource specification](https://intl.cloud.tencent.com/document/product/457/34057) of the pod by the **Unit price of the resource** and **Running time**. The following table shows the unit prices of the CPU and memory resources.

| Billing Item | Original Price | Current Discount | Discount Price |
|---------|---------|---------|---------|
| CPU | 0.000004976 USD per core per second | 20% | 0.000003981 USD per core per second |
| Memory | 0.000002073 USD per GiB per second | 20% | 0.000001658 USD per GiB per second |

> The above offer is valid until 00:00:00 on May 15, 2020. 


## Running Time
The running time is the time that elapses from when a pod fetches the first container image until the pod stops running. The pod is billed for the resources used during this period, which is measured in seconds.


## Billing Examples
#### Example 1
Assume that the specification of pods managed by a Deployment is 2 cores and 4 GB memory, and the number of replicas is fixed at 2. If the period from the time when the Deployment is started to the time when the Deployment is terminated is 5 minutes, the Deployment is billed for the resources used during the running time of 300 seconds (5 minutes × 60 seconds). 

In this case, the running fees of the Deployment = 2 × (2 × 0.000004976 + 4 × 0.000002073) × 300 = 0.019495 USD.


#### Example 2
Assume that a CronJob needs to start 10 pods with 4 cores and 8 GB memory each time and terminate the pods 10 minutes later. If the CronJob executes the job twice a day and this task is managed by EKS, the task is billed as follows:

Daily task fees = 2 × 10 × (4 × 0.000004976 + 8 × 0.000002073) × 600 = 0.437856 USD.
