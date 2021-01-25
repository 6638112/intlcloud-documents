
## Overview
This document describes the signature authentication methods of TPNS.

The HMAC-SHA256 algorithm is used to generate signing information according to `SecretKey`. The authentication is performed by verifying the signature, which ensures higher security and is recommended.


#### Parameter description

| Parameter | Description |
| --- | --- |
| AccessId | Application ID assigned by the TPNS backend, which can be obtained in **Configuration Management** > **Basic Configuration** in the [TPNS console](https://console.cloud.tencent.com/tpns) |
| SecretKey | `SecretKey` assigned by the TPNS backend, which corresponds to `AccessId` and can be obtained in **Configuration Management** > **Basic Configuration** in the [TPNS console](https://console.cloud.tencent.com/tpns) |
| Sign | API signature method |
| timeStamp |      Request timestamp |


## Signature Generation Method

1. Splice the request timestamp + `accessId` + request body to get the original string to be signed:
`String to be signed = ${timeStamp} + ${accessId} + ${request body}`
2. Use `secretKey` as the key to sign the original string to be signed to generate a signature:
`sign = Base64(HMAC_SHA256(string to be signed, secretKey))`

## HTTP Protocol Assembly Method

In addition to the general header protocol, the HTTP protocol header also needs to carry the current request timestamp, `AccessId`, and signature's `Sign` information. The specific parameters are as follows:

| Parameter Key in Header | Description | Required |
| --- | --- | --- |
| Sign | Request signature | Yes |
| AccessId | Application ID | Yes |
| TimeStamp | Request timestamp | Yes |

The specific HTTP request packet is as follows:
```xml
POST /v3/push/app HTTP/1.1
Host: api.tpns.tencent.com
Content-Type: application/json
AccessId: 1500001048
TimeStamp: 1565314789
Sign: Y2QyMDc3NDY4MmJmNzhiZmRiNDNlMTdkMWQ1ZDU2YjNlNWI3ODlhMTY3MGZjMTUyN2VmNTRjNjVkMmQ3Yjc2ZA==
{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }
```

## Signature Generation Sample

1. The generated string to be signed is as follows:
```
String to be encrypted =15653147891500001048{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }
```
2. Generate a hexadecimal hash based on the key through the HMAC-SHA256 algorithm, i.e., `secretKey =1452fcebae9f3115ba794fb0fff2fd73` in the sample.
```
hashcode= hmac-sha256(string to be signed, secretKey)
Get hashcode="cd20774682bf78bfdb43e17d1d5d56b3e5b789a1670fc1527ef54c65d2d7b76d"
```
3. Base64-encode the hashcode to get the following signature string:
```
Get Sign=Base64(hashcode)
Sign="Y2QyMDc3NDY4MmJmNzhiZmRiNDNlMTdkMWQ1ZDU2YjNlNWI3ODlhMTY3MGZjMTUyN2VmNTRjNjVkMmQ3Yjc2ZA=="
```




## Signature Code Samples in Various Languages

<dx-codeblock>
::: Python2 python
#!/usr/bin/env python
import hmac
import base64
from hashlib import sha256

s = '15653147891500001048{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }'
key = '1452fcebae9f3115ba794fb0fff2fd73'
hashcode = hmac.new(key, s, digestmod=sha256).hexdigest()
print base64.b64encode(hashcode)
:::
::: Python3 python
import hmac
import base64
from hashlib import sha256

s = '15653147891500001048{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }'
key = '1452fcebae9f3115ba794fb0fff2fd73'
hashcode = hmac.new(bytes(key, "utf-8"), bytes(s, "utf-8"),
                        digestmod=sha256).hexdigest()
print(base64.b64encode(bytes(hashcode, "utf-8")))
:::
::: Java java
package com.tencent.xg;

import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;
import org.apache.commons.codec.binary.Hex;

public class SignTest {
    public static void main(String[] args) {
        try {
            String stringToSign = "15653147891500001048{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }";
            String appSecret = "1452fcebae9f3115ba794fb0fff2fd73";

            Mac mac;
            mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(appSecret.getBytes("UTF-8"), "HmacSHA256"));
            byte[] signatureBytes = mac.doFinal(stringToSign.getBytes("UTF-8"));

            String hexStr = Hex.encodeHexString(signatureBytes);
            String signature = Base64.encodeBase64String(hexStr.getBytes());

            System.out.println(signature);
        } catch (NoSuchAlgorithmException | InvalidKeyException | UnsupportedEncodingException e) {
            e.printStackTrace();
        }
    }
}
:::
::: Golang go
import (
   "crypto/hmac"
   "crypto/sha256"
   "encoding/base64"
   "encoding/hex"
   "testing"
)

func TestSign(t *testing.T) {
   requestBody := "15653147891500001048{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }"
   secretKey := "1452fcebae9f3115ba794fb0fff2fd73"

   h := hmac.New(sha256.New, []byte(secretKey))
   h.Write([]byte(requestBody))
   sha := hex.EncodeToString(h.Sum(nil))
   sign := base64.StdEncoding.EncodeToString([]byte(sha))
   println(sign)
}
:::
::: C# c#
using System;
using System.Security.Cryptography;
using System.Text;

namespace tpns_server_sdk_cs
{
    class GenSign { 
  
        // Main Method 
        // static public void Main(String[] args)
        // {
        //     string reqBody =
        //         "{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }";
        //     string genSign = GenSign.genSign("1565314789", "1500001048", "reqBody", "1452fcebae9f3115ba794fb0fff2fd73");
        //     Console.WriteLine(genSign);
        // } 
        public static string HmacSHA256(string key, string data)
        {
            string hash;
            ASCIIEncoding encoder = new ASCIIEncoding();
            Byte[] code = encoder.GetBytes(key);
            using (HMACSHA256 hmac = new HMACSHA256(code))
            {
                Byte[] hmBytes = hmac.ComputeHash(encoder.GetBytes(data));
                hash = ToHexString(hmBytes);
            }
            return hash;
        }

        public static string ToHexString(byte[] array)
        {
            StringBuilder hex = new StringBuilder(array.Length * 2);
            foreach (byte b in array)
            {
                hex.AppendFormat("{0:x2}", b);
            }
            return hex.ToString();
        }
        
        public static string genSign(string timeStampStr, string accessId, string requestBody, string keySecret)
        {
            string data = timeStampStr + accessId + requestBody;
            string hash = HmacSHA256(keySecret, data);
            string sign = Base64Encode(hash);
            Console.WriteLine("timeStampStr: "  + timeStampStr + " accessId:" + accessId + " requestBody" + requestBody + " keySecret:" + keySecret);
            return sign;
        }
        
        public static string Base64Encode(string plainText) {
            var plainTextBytes = System.Text.Encoding.UTF8.GetBytes(plainText);
            return System.Convert.ToBase64String(plainTextBytes);
        }
    }
}
:::
::: PHP php
```
<?php
$accessId = "1500001048";
$secretKey = "1452fcebae9f3115ba794fb0fff2fd73";
$timeStamp = "1565314789";
$requestBody = "{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }";
$hashData = "{$timeStamp}{$accessId}{$requestBody}";
echo "reqBody: " . $hashData . "\n";
//Get the SHA256 and hex results
$hashRes = hash_hmac("sha256", $hashData, $secretKey, false);
//Conduct Base64 encoding
$sign = base64_encode($hashRes);
echo $sign . "\n";
?>
```
:::
</dx-codeblock>

