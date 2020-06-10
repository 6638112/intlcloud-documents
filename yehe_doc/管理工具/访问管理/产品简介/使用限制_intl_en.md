| Item | Upper Limit | 
|---------|---------|
| Number of user groups under one root account | 300 | 
| Number of sub-accounts under one root account | 1000 | 
| Number of roles under one root account | 1000 | 
| Number of user groups one sub-account can join | 10 | 
| Number of root accounts one collaborator can collaborate with | 10 | 
| Number of sub-accounts in one a user group | 100 | 
| Number of custom policies that can be created by one root account<sup>1</sup> | 1500 | 
| Number of policies directly associated with one user, user group, or role<sup>2</sup> | 200 | 
| Number of characters in one policy syntax | 4096 | 
>!
>1. COS custom policies are counted toward the total number of custom policies created by a root account. If you see a prompt saying that **The number of custom policies exceeds the upper limit (1,500)**, but the number of CAM custom policies actually has not reached the upper limit, you can go to the [bucket list in the COS Console](https://console.cloud.tencent.com/cos5/bucket) and click a bucket name to enter the permission management page and check whether the number of access control lists (ACLs) has reached the upper limit. 
>2. COS custom policies are counted toward the total number of policies directly associated with a user, user group, or role. If you see a prompt saying that **Failed to associate the policy**, but the number of associated CAM policies actually has not reached the upper limit, you can go to the [bucket list in the COS Console](https://console.cloud.tencent.com/cos5/bucket) and click a bucket name to enter the permission management page and check whether the number of access control lists (ACLs) has reached the upper limit. 
