## <span id="1"></span>The communication between CLB instances and CVM instances is over the public network or private network?
Communication between CLB and CVM instances generates private network traffic, irrespective of whether the account type is bill-by-IP or bill-by-CVM. The traffic routes of the two types are as follows:
- A client accesses a CLB instance over the public network, the CLB instance forwards the traffic to a CVM instance over the private network, then the CVM instance responds to the CLB instance over the private network, finally the CLB instance responds to the client.
- When a CVM instance accesses the public network or is accessed via a public IP, then the CVM instance interacts with a client via a public IP or EIP.
![](https://main.qcloudimg.com/raw/c6b614ebf4e53a7b096c7ef302d5e1ec.png)

## <span id="2"></span>How does the CLB billing work?
CLB billing policies vary by account type. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/214/36999). The main difference between bill-by-IP and bill-by-CVM accounts lays in the billing dimension, other aspects such as service access and monitoring are the same. For more information on differences between account types, please see the **Account Type** paragraphs.
- Bill-by-IP account: For the public network traffic accessing a CLB instance, the public network fee is charged on the CLB instance, rather than a CVM instance. For the traffic accessing via a public IP, the public network fee is charged on the public IP, rather than a CVM instance either.
- Bill-by-CVM account: For the public network traffic accessing a CLB instance or a public IP, the public network fee is charged on a CVM instance, not on the CLB instance or the public IP.

## <span id="3"></span>Can I switch my account type between bill-by-IP and bill-by-CVM?
- You can upgrade your account type from bill-by-CVM to bill-by-IP.
- A bill-by-IP account cannot be returned to a bill-by-CVM account.

## <span id="4"></span>How is the cross-region binding billed?
The cross-region binding fee is charged only if you use the CLB cross-region binding feature. For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).
- Cross region 1.0: the cross-region fee is charged on the CLB instance.
- Cross region 2.0: the cross-region fee is charged on the CCN instance, rather than the CLB instance.

## <span id="5"></span>What is the bandwidth cap of a CLB instance?
- Bill-by-IP account: You need to select the CLB bandwidth cap when you are purchasing a CLB instance. If the bandwidth of a business exceeds the cap, the CLB instance will lose the packet automatically.
- Bill-by-CVM account: You do not need to select the CLB bandwidth cap when you are purchasing a CLB instance. The CLB bandwidth is restricted by the total public network bandwidth of the backend CVM.
