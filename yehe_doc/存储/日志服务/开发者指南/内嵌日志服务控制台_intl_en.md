## Overview

CLS allows you to embed the [CLS console](https://console.cloud.tencent.com/cls) into an external system so you can conduct log search and analysis without logging in to Tencent Cloud console. This feature offers benefits as follows:

- Quickly integrate CLS search and analysis capabilities into an external service system (e.g., for business maintenance or operation).
- Easily share your log data with others without needing to manage additional Tencent Cloud sub-accounts.

**Sample code for an embedded page: [cls-iframe-demo](https://github.com/TencentCloud/cls-iframe-demo).**

>! This example does not include the authentication logic of external systems. After deployment, all users (even if they have not logged in to Tencent cloud) can view the data under their accounts with the role permissions configured in the example. To ensure data privacy and security, please add the authentication logic of external systems or restrict their access to the private network only to ensure that only authorized users can view the page.
>

See the figure below for an overview of this feature:
![img](https://main.qcloudimg.com/raw/c04840e707a3e9aca812d58d9414faea.png)

## Prerequisites

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) to create a [CAM role](https://intl.cloud.tencent.com/document/product/598/19381) **with console login permissions**. Set the role entity to root account, e.g. `CompanyOpsRole`. Grant the CAM role appropriate access permissions using policies, e.g. `QcloudCLSReadOnlyAccess` for read-only access.
<span id="step1"></span>
 1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
 2. Click **Roles** on the left sidebar to go to the roles list page.
 3. Choose **Create Role** > **Tencent Cloud Account** to create a custom role.
 4. Select **Current root account **, check **Allow the current role to access console**, and click **Next**.
![img](https://qcloudimg.tencent-cloud.cn/raw/1db44714391015369d870e5aabbd0618.png)
>!If the option **Allow the current role to access console** is not available, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for adding the role to the allowlist.
>
 5. Set access policies for the role, e.g., the read-only policy `QcloudCLSReadOnlyAccess`, and click **Next**.
![img](https://qcloudimg.tencent-cloud.cn/raw/853c5443975035744c41ee9c09187eb3.png)
 6. Enter the role name and click **Done**.
![img](https://qcloudimg.tencent-cloud.cn/raw/d45e624e8f71c58d55afe479ed19adc7.png)
<span id="step2"></span>
2. Obtain the access key of the current user. For more information, see [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228).

## Directions

1. Log in to the web server outside Tencent Cloud.
2. The external web server assigns you the pre-created role created in Prerequisite 1 based on your identity, e.g. `CompanyOpsRole`.
3. The web server accesses the Tencent Cloud STS service based on the role name and uses the access key obtained in Prerequisite 2 to call the [AssumeRole](https://intl.cloud.tencent.com/document/product/598/35840) API to apply for a temporary key of `CompanyOpsRole`.
4. Call the [AssumeRole](https://intl.cloud.tencent.com/document/product/598/35840) API to get the temporary key of `CompanyOpsRole`.
5. Generate a login signature using the temporary key with the steps as shown below:
 1. **Sorting parameters**
     Sort parameters to be signed listed below in ascending alphabetical or numerical order. That is, sort the parameters by their first letters, then by their second letters if their first letters are the same, and so on. You can do this with the aid of sorting functions in programming languages, such as the ksort function in PHP.	 
<table>
<thead>
<tr>
<th align="left">Parameter</th>
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
<td align="left">timestamp</td>
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
<h4>Sample signature string</h4>
```plaintext
     GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=AKI***PLE&timestamp=1484793352
```
 4. **Generating a signature string**
Currently, you can sign a string using HMAC-SHA1 or HMAC-SHA256. The sample code in PHP is as follows:
```plaintext
$secretKey = 'Gu5***1qA';
$srcStr    = 'GETcloud.tencent.com/login/roleAccessCallback?action=roleLogin&nonce=67439&secretId=&timestamp=1484793352';
$signStr   = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```
 <h4>Sample code for PHP</h4>
```
     <?php
     $secretId  = "AKI***";            //Temporary AK returned by STS
     $secretKey = "Gu5***PLE";         //Temporary SecretKey returned by STS
     $token     = "ADE***fds";         //Security Token returned by STS
     $param["nonce"]     = 11886;      //rand(10000,100000000);
     $param["timestamp"] = 1465185768; //time();
     $param["secretId"]  = $secretId;
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
https://console.cloud.tencent.com/cls/search?region=<region>&topic_id=<topic_id>
```
   **Parameters in the CLS console search analysis page URL**:
<table>
	<tr><th>Parameter</th><th>Required</th><th>Type</th><th>Description</th></tr>
	<tr><td>region</td><td>Yes</td><td>String</td><td>Region abbreviation, e.g., ap-shanghai for Shanghai region. For other available region abbreviations, see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a></td></tr>
	<tr><td>topic_id</td><td>No</td><td>String</td><td>Log topic ID</td></tr>
	<tr><td>logset_name</td><td>No</td><td>String</td><td>Logset name</td></tr>
	<tr><td>topic_name</td><td>No</td><td>String</td><td>Log topic name</td></tr>
	<tr><td>time</td><td>No</td><td>String</td><td>Time range for log search. Format example:
2021-07-15T10:00:00.000,2021-07-15T12:30:00.000</td></tr>
	<tr><td>queryBase64</td><td>No</td><td>String</td><td>Search and analysis statement, which is base64Url-encoded</td></tr>
	<tr><td>filter</td><td>No</td><td>String</td><td>Filter condition, which is base64Url-encoded. For more information, see <a href="#ParameterDesc">Filter Parameter Description</a></td></tr>
	<tr><td>hideWidget</td><td>No</td><td>Boolean</td><td>Indicates whether to hide agent/documentation button in the bottom-right corner. `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideTopNav</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the top navigation bar in the Tencent Cloud console. `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideLeftNav</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the left navigation bar in the Tencent Cloud console. `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideTopicSelect</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic selection controls (including the region, logset, and log topic controls). `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideHeader</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic selection control and the row where the control resides. `true`: Yes; `false`: No (default). This parameter is valid only when `hideTopicSelect` is `true`.</td></tr>
	<tr><td>hideTopTips</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the announcements on the top of the page. `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideConfigMenu</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the log topic configuration management menu. `true`: Yes; `false`: No (default)</td></tr>
	<tr><td>hideLogDownload</td><td>No</td><td>Boolean</td><td>Indicates whether to hide the raw log download button. `true`: Yes; `false`: No (default)</td></tr>
</table>



>! You can specify the log topic to search using URL parameters in either the following modes:
> - topic_id: use the log topic ID to specify the log topic to search.
> - logset_name+topic_name: use the logset name and log topic name to specify the log topic to search. Note that if the logset or log topic name changes, the URL adopting this mode will become invalid.
>
> - If the `topic_id`, `logset_name`, and `topic_name` parameters exist at the same time, `topic_id` prevails. 

The following figure shows the mappings between hidden parameters and page modules:

 2. Splice your login information and destination page URL into a login URL. **The parameter values should be URL-encoded.**
```plaintext
https://cloud.tencent.com/login/roleAccessCallback
?algorithm=<encryption algorithm for signing; currently only supports SHA1 (used by default) and SHA256
&secretId=<secretId for signing>
&token=<Temporary key token>
&nonce=<nonce for signing>
&timestamp=<Timestamp for signing>
&signature=<Signature string>
&s_url=<Destination URL after login>
```
7. Use the final URL to access the embedded CLS page of the Tencent Cloud console. The sample below is a URL to the CLS search analysis page:
```plaintext
https://cloud.tencent.com/login/roleAccessCallback?nonce=52055817&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcls%2Fsearch%3Fregion%3Dap-guangzhou%26start_time%3D2020-05-26%25252014%25253A01%25253A18%26end_time%3D2020-05-26%25252014%25253A16%25253A18&secretId=AKID-vHJ7WPHcy_RVIOm-QTIktXOf9S9z_k_JackOp3dyQPJwmDrNLQJuiNuw9******&signature=eXeWaDn6iJlcPp1sqqGd6m9%2FQk****&timestamp=1592455018&token=5e4vuBHL7fBQPi1V9fvSINw4Vu7PSr9Ic3de78b86109c171eb4e3ea27c137c1fIWKU8JC-LO01L87sIYlfTSaHHXeHcqim7Jg9hBuN2nbdfgeBUPXhmpyAk4G6e9bHFZ-7yNRig7Y33CQHxh6jOesP4VfhRzQprWGRtC5No1ty******-aoj_WJhA55oyvqaqxw2jtTdh8nx9OjJr3tlbIa9oJe7aZYoPbdpFqrF6ZjlCPPap2yQB_SkUsWwDl_9BrK2Km3U2IocdvQ7QxrW0ts1aiBi7xtTSJRcfkBYPYEV_YoJrtkhYW3E4L47imA1bfVAjM9F5uKWzVzsDGDT0aCUU9mqdb4vjJrY8tm-wJKKEe8eiyY9EbkH3VWnFV2YocYNDJqFyjKOWR******
```

<span id="ParameterDesc"></span>
## Filter Parameter Description

Filter parameters are used to generate the filter condition in the query statement box at the bottom of the page, as shown in the figure blow, and are suitable for fixed search criteria.
![img](https://qcloudimg.tencent-cloud.cn/raw/0e4c485436980cff533aebc657c4ed81.png)

Filter parameters are in JSON format in the following structure:
```
[{
    "key": "action",
    "grammarName": "INCLUDE",
    "values": [{
        "values": ["test1"]
    }]
}]
```
Where:
- `key` indicates the field name for key-value search. For full-text search, leave `key` empty.
- `grammarName` indicates the specific filter mode of the filter condition. Supported values include `INCLUDE`, `EXCLUDE`, `EXISTS`, and `RANGE`.
<table>
	<tr><th>Feature</th><th>grammarName</th><th>Example</th><th>Equivalent Search Statement</th></tr>
	<tr><td>Key-value search - INCLUDE</td><td>INCLUDE</td><td>[{"key":"action","grammarName":"INCLUDE","values":[{"values":["test1"]}]}]</td><td>action:"test1"</td></tr>
	<tr><td>Key-value search - EXCLUDE</td><td>EXCLUDE</td><td>[{"key":"action","grammarName":"EXCLUDE","values":[{"values":["test1","test2"]}]}]</td><td>NOT action:"test1" AND NOT action:"test2"</td></tr>
	<tr><td>Full-text search - INCLUDE</td><td>INCLUDE_WITHOUT_KEY</td><td>[{"key":"","grammarName":"INCLUDE_WITHOUT_KEY","values":[{"values":["test3"]}]}]</td><td>"test3"</td></tr>
	<tr><td>Full-text search - EXCLUDE</td><td>EXCLUDE_WITHOUT_KEY</td><td>[{"key":"","grammarName":"EXCLUDE_WITHOUT_KEY","values":[{"values":["test3"]}]}]</td><td>NOT "test3"</td></tr>
	<tr><td>The field exists</td><td>EXISTS</td><td>[{"key":"action","grammarName":"EXISTS","values":[]}]</td><td>_exists_:action</td></tr>
	<tr><td>The field does not exist</td><td>NOT_EXISTS</td><td>[{"key":"action","grammarName":"NOT_EXISTS","values":[]}]</td><td>NOT _exists_:action</td></tr>
	<tr><td>The numeric type field is in the specified range</td><td>RANGE</td><td>[{"key":"time","grammarName":"RANGE","values":[{"values":["1"]},{"values":["100"]}]}]</td><td>time:[1 TO 100]</td></tr>
	<tr><td>The numeric type field is outside the specified range</td><td>NOT_RANGE</td><td>[{"key":"time","grammarName":"NOT_RANGE","values":[{"values":["1"]},{"values":["100"]}]}]</td><td>NOT time:[1 TO 100]</td></tr>
	<tr><td>The numeric type field is greater than the specified value</td><td>MORE_THAN</td><td>[{"key":"time","grammarName":"MORE_THAN","values":[{"values":["1"]}]}]</td><td>time:>1</td></tr>
	<tr><td>The numeric type field is greater than or equal to the specified value</td><td>MORE_THAN_OR_EQUAL</td><td>[{"key":"time","grammarName":"MORE_THAN_OR_EQUAL","values":[{"values":["1"]}]}]</td><td>time:>=1</td></tr>
	<tr><td>The numeric type field is less than the specified value</td><td>LESS_THAN</td><td>[{"key":"time","grammarName":"LESS_THAN","values":[{"values":["1"]}]}]</td><td>time:<1</td></tr>
	<tr><td>The numeric type field is less than or equal to the specified value</td><td>LESS_THAN_OR_EQUAL</td><td>[{"key":"time","grammarName":"LESS_THAN_OR_EQUAL","values":[{"values":["1"]}]}]</td><td>time:<=1</td></tr>
</table>


>! Only base64Url-encoded filter parameters can be added to URLs.
>

