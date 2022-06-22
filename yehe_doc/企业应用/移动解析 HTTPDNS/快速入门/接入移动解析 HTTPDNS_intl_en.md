# Connecting to HTTPDNS

>!
> 
> - If you don't use the SDK, you need to **retain the local DNS as a backup** during connection. For more information, see [Best Practice of API Connection](https://intl.cloud.tencent.com/doc/product/379/%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5?from_cn_redirect=1).
> - **Currently, only the DES encryption method is available (service IP: `43.132.55.55`). HTTPS and AES encryption methods are not available.**

## **1. Register an account**

First, you need to activate HTTPDNS in the [HTTPDNS console](https://console.cloud.intl.tencent.com/httpdns) as instructed in [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).

## **2. Add a domain**

After activating HTTPDNS, you need to add a domain to be resolved in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465) before you can use it.

## **3. Get the configuration information**

After activating the service, you will be assigned the configuration information such as authorization ID, AES and DES encryption keys, and HTTPS token, which can be viewed in the [HTTPDNS console](https://console.cloud.tencent.com/httpdns/configure). For more information, see [Configuration Information Description](https://intl.cloud.tencent.com/document/product/1130/44467).

## **4. Resolve the domain with the HTTPDNS API**

After getting the authorization ID, encryption key, and HTTPS token, you can request DNS query in the following ways:

>?
> 
> - DNS query encrypted with DES, which is fast
> - DNS query encrypted with AES, which delivers balanced effect and speed
> - DNS query encrypted with HTTPS, which delivers the best effect but is slightly slow

### **Single query**

- DES/AES encryption: `http://43.132.55.55/d?dn=[encrypted domain string]&id=[authorization ID]&ttl=1`. For the request format, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470).
- HTTPS encryption: `https://43.132.55.56/d?dn=[domain]&token=[HTTPS Token]&ttl=1`. For the request format, see [Querying with HTTP Request Methods](https://intl.cloud.tencent.com/document/product/1130/44468).

### **Batch query**

HTTPDNS supports batch querying domains. You can enter multiple domains separated by commas. The query results will be separated by `\n`. For example, you can query `cloud.tencent.com,www.qq.com,www.dnspod.cn` at the same time.

- DES/AES encryption: For the request format, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470).
- HTTPS encryption: For the request format, see [Querying with HTTPS Request Methods](https://intl.cloud.tencent.com/document/product/1130/44469).

**Limits:**

- Up to 8 domains are supported at a time, and the returned value will not exceed `8 * 1024` bytes.

## **5. Modify the client**

Change the client DNS to HTTPDNS. Note that you need to **retain the local DNS as a backup** during connection. For more information, see [Best Practice of API Connection](https://intl.cloud.tencent.com/document/product/1130/44471).

## **6. Apply for use with SDK (optional)**

You can [connect to HTTPDNS with the SDK](https://intl.cloud.tencent.com/document/product/1130/44474). Tencent Cloud's proprietary **HTTPDNS SDKs** are highly customizable and can be directly embedded in applications. With mature and stable features, they have been widely used on Tencent's various types of game clients.

>!
> 
> - `dnsId` in the SDK parameters is the authorization ID.
> - `dnsKey` in the SDK parameters is the AES/DES encryption key (i.e., key for the authorization ID), which can be selected based on your encryption method.
> - `token` in the SDK parameters is the HTTPS token.
> - `appkey` in the SDK parameters is the `AppID`. If you need to get the `AppID` information, see [SDK Activation Process](https://intl.cloud.tencent.com/document/product/1130/44474).

For more information, see the following documents:

[SDK for iOS >>](https://intl.cloud.tencent.com/document/product/1130/44472)

[SDK for Android >>](https://intl.cloud.tencent.com/document/product/1130/44473)