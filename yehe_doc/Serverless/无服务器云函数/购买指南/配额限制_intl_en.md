SCF has certain quota limits for each user account.


## Quota Limits

The quota limits for each user account are as follows:

| Item | Default Quota Limit |
| ----------------------------------------------- | ------------ |
| Maximum number of functions per namespace per region | 50 |
| Maximum number of concurrent executions per function | 128,000 MB |
| Total function concurrency quota per region                        | 10          |
| Maximum number of same-type triggers per function | 10 |
| Maximum code size (including bound layers) per function (version) | 500 MB       |
| Total function code size per region                      | 100 GB       |
| Maximum environment variable size per function                          | 4 KB         |

>! 
>- SCF currently supports 10,000-level concurrency, which can effectively support scenarios with high concurrency demand such as ecommerce promotions and parallel processing of medical and biological data.
>- The total function concurrency quota per region on the SCF platform is 128,000 MB, which is shared by all functions by default. You can [customize the concurrency for specific functions](https://intl.cloud.tencent.com/document/product/583/37040) to meet your actual needs. To request an increase in the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) to apply.

The limits for the function runtime environment are as follows:

| Item | Quota Limit |
| -------------------------------- | --------------------------------------------------- |
| Allocated memory | Minimum: 64 MB, maximum: 3,072 MB, in increments of 128 MB starting from 128 MB |
| Temporary cache space, i.e., size of the `/tmp` directory | 512 MB |
| Timeout period | Minimum: 1 second, maximum: 900 seconds |
| Number of file descriptors | 1,024 |
| Total processes and threads | 1,024 |
| Sync request event size | 6 MB |
| Sync request response size | 6 MB |
| Async request event size | 128 KB |

>! If the size of a Base64-encoded file is below 6 MB, you can pass the encoded file to SCF through [API Gateway](https://intl.cloud.tencent.com/product/apigateway). Otherwise, we recommend you upload the file to [COS](https://intl.cloud.tencent.com/product/cos) and pass the object address to SCF first. Then, SCF will pull the file from COS to complete the upload.



## Limit Increase

Currently, the limits that can be increased include:
- Maximum number of functions
- Total function concurrency quota per region
- Maximum number of triggers per function
- Maximum code size per function
- Total function code size per region

To increase the limits, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) and state the items you want to increase and to what quantities you want to increase them to.
