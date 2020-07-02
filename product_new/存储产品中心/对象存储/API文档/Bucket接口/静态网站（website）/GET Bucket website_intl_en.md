## Feature

This API is used to obtain the configuration of the static website associated with the bucket.

## Request

#### Request samples

```plaintext
GET /?website HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request parameters

This API does not use any request parameter.

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query will return **application/xml** data which includes all information about the static website configuration on the bucket.

```xml
<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>string</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>string</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>string</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>integer</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>string</Protocol>
				<ReplaceKeyWith>string</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>string</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>string</Protocol>
				<ReplaceKeyPrefixWith>string</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| WebsiteConfiguration | None | Saves all information in the response to GET Bucket website | Container |

**Content of the Container node `WebsiteConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| IndexDocument | WebsiteConfiguration | Index document | Container |
| RedirectAllRequestsTo | WebsiteConfiguration | Redirects all requests | Container |
| ErrorDocument | WebsiteConfiguration | Error document | Container |
| RoutingRules | WebsiteConfiguration | Sets redirect rules | Container |

**Content of the Container node `IndexDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Suffix | WebsiteConfiguration.IndexDocument | Specifies the object key suffix for index documents. For example, if it is specified as `index.html`, the request automatically returns `index.html` when you access the root directory of the bucket, or `article/index.html` when you access the directory `article/`. | string |

**Content of the Container node `RedirectAllRequestsTo`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RedirectAllRequestsTo | Specifies the destination protocol for all redirect requests | string |

**Content of the Container node `ErrorDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | WebsiteConfiguration.ErrorDocument | Specifies the object key of the general error document | string |

**Content of the Container node `RoutingRules`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| RoutingRule | WebsiteConfiguration.RoutingRules | Sets a single redirect rule | Container |

**Content of the Container node `RoutingRules.RoutingRule`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Condition | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the condition for the redirect rule | Container |
| Redirect | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the redirect destination for the redirect rule | Container |

**Content of the Container node `RoutingRules.RoutingRule.Condition`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| HttpErrorCodeReturnedEquals | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Condition | Specifies the error code as match condition for the redirect rule | integer |
| KeyPrefixEquals | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Condition | Specifies the object key prefix as match condition for the redirect rule | string |

**Content of the Container node `RoutingRules.RoutingRule.Redirect`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Specifies the destination protocol for the redirect rule | string |
| ReplaceKeyWith | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key of redirect destination in the redirect rule to replace the entire object key included in the original request | string |
| ReplaceKeyPrefixWith | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key of redirect destination in the redirect rule to replace the prefix which the original request used for match | string |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

#### Request

```plaintext
GET /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 20 May 2020 09:33:49 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1589967229;1589974429&q-key-time=1589967229;1589974429&q-header-list=date;host&q-url-param-list=website&q-signature=50a22a30b02b59e5da4a0820d15a36805ea7****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1163
Connection: close
Date: Wed, 20 May 2020 09:33:49 GMT
Server: tencent-cos
x-cos-request-id: NWVjNGY5N2RfYTdjMjJhMDlfNjZkY18yYWUx****

<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>pages/error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>403</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>pages/403.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<ReplaceKeyWith>pages/404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>assets/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<ReplaceKeyWith>index.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>article/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>archived/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```
