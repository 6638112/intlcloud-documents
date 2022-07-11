## Overview

The request body sent to service backend by the Client contains many fields. If you want to modify the content of the request body, you can do so via custom request body plugin.

The custom request body plugin is based on Serverless Cloud Function (SCF) and applies during request process. The API Gateway will forward the request content to the specified function after receiving it from the Client. SCF will send the modified content of request body to the API Gateway after modifying it. Then, the API Gateway will forward the modified request body to service backend.
<img  src="https://qcloudimg.tencent-cloud.cn/raw/d08dee5fddf27985ffc89b23836060b7.png" width="600px">

## Prerequisites

- You have activated [SCF](https://console.cloud.tencent.com/scf/list).

## Directions

### Step 1. Create a function to modify the request body

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list).
2. Click **Function Service** on the left sidebar to open the function list page.
3. Click **Create** in the top-left corner of the page to create a function that is used to modify the request body.

>?You need to write the function that is used to modify the request body. For more information, see [How to Write Custom Request Body Function](#scfdemo).

### Step 2. Create a custom request body plugin[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin - Custom Plugin** to open the custom plugin list page.
3. Create **Create** in the top-left corner of the page to create a custom request body plugin. You need to enter the following parameters:

| Parameter | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ |
| Function | Required | You need to select the namespace, name and version of the function that is used to modify the request body. |
| Backend timeout    | Required | This sets the backend timeout that the API Gateway forwards the request to the function that is used to modify the request body. The maximum time limit is 30 minutes. When no response is returned before the timeout after the API Gateway calls the function, the API Gateway will end the call and returns an error message. |
| Custom content | Required | It sets the request content sent to the function by the API Gateway. You can select Header, Body and Query. The request content not selected will not be modified and forwarded to service backend as is. |
| Base64 encoding | Required | It specifies whether to forward the request content to the function after applying Base64 encoding. Generally, it is applicable to binary content. |

![](https://qcloudimg.tencent-cloud.cn/raw/19cefb5320773a3a1a09bbaba0cc3c7d.png)

4. Click **Save** to complete the process.

### Step 3. Bind the API

1. Select the plugin created in [step 2](#step2) from the list. Click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e9e674392e0070e320d38c1c00fc1ba2.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## How to Write Custom Request Body Function[](id:scfdemo)
### Returned value definition
The custom request body plugin of API Gateway needs to receive the response in a certain format returned by the custom request body function. The specific format is as follows:
```
{
  "replace_headers":{
    "header1":"header1-value",
    "header2":"header2-value"
  },
  "remove_headers":[
    "header3",
    "header4"
  ],
  "replace_body":"hello",
  "replace_querys":{
    "query1":"query1-value",
    "query2":"query2-value"
  },
  "remove_querys":[
    "query3",
    "query4"
  ]
}
```

### Demo for Python
>?For more information on how to write the function that is used to modify the request body in Python, see [Custom Request Body Demo for Python](https://github.com/tencentyun/serverless-demo/blob/master/Python3.6-APIGWCustomRequest/src/index.py).

### Demo for Java
```
package com.example.demo;

import com.google.gson.JsonArray;
import com.google.gson.JsonObject;
import com.qcloud.services.scf.runtime.events.APIGatewayProxyRequestEvent;

public class Demo {

	public String mainHandler(APIGatewayProxyRequestEvent request) {
		System.out.println("helloworld");
		System.out.println(request.getHttpMethod());
		JsonObject resp = new JsonObject();
		headerHandler(request, resp);
		headerQuery(request, resp);
		headerBody(request, resp);
		return resp.toString();
	}

	private void headerHandler(APIGatewayProxyRequestEvent request, JsonObject resp) {
		JsonObject replace_headers = new JsonObject();
		JsonArray remove_headers = new JsonArray();
		// Sample: Replace or add `header1` and `header2`
		replace_headers.addProperty("header1", "header1-value");
		replace_headers.addProperty("header2", "header2-value");

		// Sample: Delete `header3`
		remove_headers.add("header3");
		resp.add("replace_headers", replace_headers);
		resp.add("remove_headers", remove_headers);
	}

	private void headerQuery(APIGatewayProxyRequestEvent request, JsonObject resp) {
		JsonObject replace_querys = new JsonObject();
		JsonArray remove_querys = new JsonArray();

		// Sample: Replace or add `query1` and `query2`
		replace_querys.addProperty("query1", "query1-value");
		replace_querys.addProperty("query2", "query2-value");

		// Sample: delete `query3`
		remove_querys.add("query3");
		resp.add("replace_querys", replace_querys);
		resp.add("remove_querys", remove_querys);
	}

	private void headerBody(APIGatewayProxyRequestEvent request, JsonObject resp) {
		resp.addProperty("replace_body", "{'name':'Yagr'}");
	}
}
```

## PluginData

```json
{
    "endpoint_timeout":15, // Backend timeout period in seconds. Value range: 0–60
    "func_name":"test_name", // Custom function name
    "func_namespace":"test_namespace", // Custom function namespace
    "func_qualifier":"$LATEST", // Custom function version
    "is_base64_encoded":true, // Whether to forward the request content to the function after applying Base64 encoding
    "is_send_req_body":true, // Whether to send the request Body content to the function
    "is_send_req_headers":true, // Whether to send the request Header content to the function
    "is_send_req_querys":true, // Whether to send the request Query content to the function
    "user_id":1253970226 // appid
}
```

## Notes

- Binding a custom plugin to the API means creating a trigger for the function to trigger the API. Deleting the trigger on the SCF side means unbinding the plugin from the API.
- For now, the custom request body plugin only supports event-triggered function and does not support HTTP-triggered function.
