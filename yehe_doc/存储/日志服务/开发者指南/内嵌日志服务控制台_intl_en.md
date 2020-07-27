
## Overview

CLS allows you to embed the [CLS Console](https://console.cloud.tencent.com/cls) into an external system so you can conduct log search and analysis without logging in to Tencent Cloud console. This feature offers benefits as follows:

- Quickly integrate CLS search and analysis capabilities into an external service system (e.g., for business maintenance or operation).
- Easily share your log data with others without needing to manage additional Tencent Cloud sub-accounts.

See the figure below for an overview of this feature:
![img](https://main.qcloudimg.com/raw/c04840e707a3e9aca812d58d9414faea.png)



## Prerequisites


1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) to create a [CAM Role](https://intl.cloud.tencent.com/document/product/598/19381) **with console login permissions**. Set the role entity to root account, e.g. `CompanyOpsRole`. Grant the CAM role appropriate access permissions using policies, e.g. `QcloudCLSReadOnlyAccess` for read-only access. You can create a CAM role in 2 ways: [using the console](#step1) or [using APIs](#step2).
<span id="step1"></span>
 - **Creating a CAM role using the console**:
	1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview).
	2. Click **Roles** in the left sidebar to enter the roles list page.
	3. Select **Create Role** > **Tencent Cloud Account** to create a custom role.
	4. Select **Current root account **, check **Allow current role to log in to the console**, and click **Next**.
	
	>!If the option **Allow current role to log in to the console* is not available, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be whitelisted for this feature.
	5. Set access policies for the role, e.g., the read-only policy `QcloudCLSReadOnlyAccess`, and click **Next**.
	
	6. Enter the role name and click **Done**.
	
<span id="step2"></span>
 - **Creating a CAM role using APIs**:
 For detailed directions, see [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561). Note that you need to enter `1` as the value of ConsoleLogin to allow the role to log in to the console.
 Sample request:
 ```plaintext
https://cam.tencentcloudapi.com/?Action=CreateRole&RoleName=CompanyOpsRole&ConsoleLogin=1&PolicyDocument={"version":"2.0","statement":[{"action":["cls:get*","cls:list*","cls:GetHistogram","cls:GetFastAnalysis","cls:GetChart","cls:ListChart","cls:ListDashboard","cls:GetDashboard","cls:searchLog","cls:downloadLog","cls:pullLogs"],"effect":"allow","principal":{"qcs":["qcs::cam::uin/100001234567:root"]}}]}
 ```
2. Obtain the access key of current user. For more information, see [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228).



## Directions

1. Log in to the web server outside Tencent Cloud.
2. The external web server assigns you the pre-created role created in Prerequisite 1 based on your identity, e.g. CompanyOpsRole.
3. Use the role to access Tencent Cloud STS within the external web server, and call the AssumeRole API with the access key obtained in Prerequisite 2 to request the temporary key for the CAM role CompanyOpsRole.
4. You will get the temporary key when the call succeeds.
5. Generate a login signature using the temporary key with the steps as shown below:
   1. **Sorting parameters**
       Sort parameters to be signed listed below in ascending alphabetical or numerical order. That is, sort the parameters by their first letters, then by their second letters if their first letters are the same, and so on. You can do this with the aid of sorting functions in programming languages, such as the ksort function in PHP.	 
<table>
<thead>
<tr>
<th align="left">Parameter Name</th>
<th align="left">Required</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">action</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Action; fixed as `roleLogin`</td>
</tr>
<tr>
<td align="left">timespace</td>
<td align="left">Yes</td>
<td align="left">Int</td>
<td align="left">Current timestamp</td>
</tr>
<tr>
<td align="left">nonce</td>
<td align="left">Yes</td>
<td align="left">Int</td>
<td align="left">Random integer. Value range: 10000-100000000</td>
</tr>
<tr>
<td align="left">secretId</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Temporary AK returned by STS</td>
</tr>
<tr>
<td align="left">token</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Security Token returned by STS</td>
</tr>
</tbody></table>
 2. **Formatting parameters**
Combine the above sorted parameters into the form of "parameter name=parameter value". Example:
 ```plaintext
 action=roleLogin&nonce=67439&secretId=AKI***PLE&timestamp=1484793352
 ```
 3. **Constructing a signature string**
Construct a signature string in the format of “request method + request CVM + request path + ? + request string”.
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Required</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Request CVM and path</td>
<td align="left">Yes</td>
<td align="left">Fixed as <code>cloud.tencent.com/login/roleAccessCallback</code></td>
</tr>
<tr>
<td align="left">Request method</td>
<td align="left">Yes</td>
<td align="left">GET or POST</td>
</tr>
</tbody>
</table>

		#### Sample signature string
	 ```plaintext
	 GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=AKI***PLE×tamp=1484793352
	 ```
   4. **Generating a signature string**

     Currently, you can sign a string using HMAC-SHA1 or HMAC-SHA256. The sample code in PHP is as follows:
     ```plaintext
     $secretKey = 'Gu5***1qA';
     $srcStr    = 'GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=&timestamp=1484793352';
     $signStr   = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
     echo $signStr;
     ```
     #### Sample code for PHP
     ```
     <?php
     $secretId  = "AKI***";            //Temporary AK returned by STS
     $secretKey = "Gu5***PLE";         //Temporary SecretKey returned by STS
     $token     = "ADE***fds";         //Security Token returned by STS
     $param["nonce"]     = 11886;      //rand();
     $param["timestamp"] = 1465185768; //time();
     $param["secretId"]  = $secretId;
     $param["token"]     = $token;
     $param["action"]    = "roleLogin";
     ksort($param);
     $signStr = "GETcloud.tencent.com/login/roleAccessCallback?";
     foreach ( $param as $key => $value ) {
         $signStr = $signStr . $key . "=" . $value . "&";
     }
     $signStr   = substr($signStr, 0, -1);
     $signature = base64_encode(hash_hmac("sha1", $signStr, $secretKey, true));
     echo $signature.PHP_EOL;
     ```
6. Combine your login information and destination page URL into a login URL.
   1. **Get the CLS console search analysis page URL**.
     ```plaintext
     https://console.cloud.tencent.com/cls/search?region=<region>&logset_id=<logset_id>&topic_id=<topic_id>
     ```
   **Parameters in the CLS console search analysis page URL**:
<table>
<thead>
<tr>
<th align="left">Parameter Name</th>
<th align="left">Required</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">region</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Region abbreviation, e.g. ap-shanghai for Shanghai region. For other available region abbreviations, see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a></td>
</tr>
<tr>
<td align="left">logset_id</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Logset ID</td>
</tr>
<tr>
<td align="left">topic_id</td>
<td align="left">Yes</td>
<td align="left">String</td>
<td align="left">Log topic ID</td>
</tr>
<tr>
<td align="left">start_time</td>
<td align="left">No</td>
<td align="left">String</td>
<td align="left">Start time of logs to search, e.g. 2019-11-13 10:00:00</td>
</tr>
<tr>
<td align="left">end_time</td>
<td align="left">No</td>
<td align="left">String</td>
<td align="left">End time of logs to search, e.g. 2019-11-13 20:00:00</td>
</tr>
<tr>
<td align="left">query</td>
<td align="left">No</td>
<td align="left">String</td>
<td align="left">Keyword search syntax. Reserved URL characters (if any) in keywords must be URL encoded.</td>
</tr>
<tr>
<td align="left">hideWidget</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide the Smart Customer Service icon. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideTopNav</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide the top navigation bar in Tencent Cloud console. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideLeftNav</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide the left sidebar in Tencent Cloud console. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideHeader</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide the top navigation bar in CLS page (title and region options). `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideTopTips</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide the tips in CLS page. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideRegion</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide region options at the top of CLS page. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideLogsetSelect</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide logset options in CLS page. `true`: Yes; `false`: No</td>
</tr>
<tr>
<td align="left">hideTopicSelect</td>
<td align="left">No</td>
<td align="left">Boolean</td>
<td align="left">Indicates whether to hide log topic options in CLS page. `true`: Yes; `false`: No</td>
</tr>
</tbody></table>
 2. Format your login information into a final embedded access URL.
     ```plaintext
     https://cloud.tencent.com/login/roleAccessCallback
	 ?algorithm=<encryption algorithm for signing; currently only supports sha1 (used by default) and sha256
	 &secretId=<secretId for signing>
	 &token=<token for signing>
	 &nonce=<nonce for signing>
	 &timestamp=<timestamp for signing>
	 &signature=<signature string>
	 &s_url=<destination URL after login>
     ```
7. Use the final URL to access the embedded Tencent Cloud console CLS page. The sample below is a URL to the CLS search analysis page:
```plaintext
https://cloud.tencent.com/login/roleAccessCallback?nonce=52055817&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcls%2Fsearch%3Fregion%3Dap-guangzhou%26start_time%3D2020-05-26%25252014%25253A01%25253A18%26end_time%3D2020-05-26%25252014%25253A16%25253A18&secretId=AKID-vHJ7WPHcy_RVIOm-QTIktXOf9S9z_k_JackOp3dyQPJwmDrNLQJuiNuw9******&signature=eXeWaDn6iJlcPp1sqqGd6m9%2FQk****&timestamp=1592455018&token=5e4vuBHL7fBQPi1V9fvSINw4Vu7PSr9Ic3de78b86109c171eb4e3ea27c137c1fIWKU8JC-LO01L87sIYlfTSaHHXeHcqim7Jg9hBuN2nbdfgeBUPXhmpyAk4G6e9bHFZ-7yNRig7Y33CQHxh6jOesP4VfhRzQprWGRtC5No1ty******-aoj_WJhA55oyvqaqxw2jtTdh8nx9OjJr3tlbIa9oJe7aZYoPbdpFqrF6ZjlCPPap2yQB_SkUsWwDl_9BrK2Km3U2IocdvQ7QxrW0ts1aiBi7xtTSJRcfkBYPYEV_YoJrtkhYW3E4L47imA1bfVAjM9F5uKWzVzsDGDT0aCUU9mqdb4vjJrY8tm-wJKKEe8eiyY9EbkH3VWnFV2YocYNDJqFyjKOWR******
```


