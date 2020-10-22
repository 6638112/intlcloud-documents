## 内容介绍

如果您希望给某些房间加入进房的条件限制（例如有些房间需要是会员才能进入），而您又担心在客户端限制很容易遭遇破解问题，那么可以考虑**开启房间权限控制**。

## 支持的平台

|   iOS    | Android  |  Mac OS  | Windows  | Electron | 微信小程序 | Chrome 浏览器 |
| :------: | :------: | :------: | :------: | :------: | :--------: | :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;  |   &#10003;    |

## PrivateMapKey

### 作用介绍

privateMapKey 是 TRTCParamEnc 中的一个可选字段，它的作用是让腾讯云检查用户是否拥有进入指定房间的权限。

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)

### 与 UserSig 的区别

- [**UserSig**](https://intl.cloud.tencent.com/document/product/647/35166) 
  TRTCParamEnc 的必选项，作用是检查当前用户是否有权使用 TRTC 云服务，用于防止攻击者盗用您的 sdkappid 账号内的流量。

- **privateMapKey**
  TRTCParamEnc 的非必选项，作用是检查当前用户是否有权进入指定 roomid 的房间，当您的业务需要对用户进行身份区分的时候才有必要开启。

而且，您在 App 端直接判定当前用户是否有权进入指定房间也是可以的，privateMapKey 的作用仅仅是做的更安全，它可以避免客户端被破解后，出现“非会员也能进高等级房间”的破解版本。

## 如何开启

1. **在腾讯云 [实时音视频控制台](https://console.cloud.tencent.com/rav) 开启房间权限控制。**
    ![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)
2. **在您的服务器端计算 privateMapKey。**
   由于 privateMapKey 的价值就是为了防止客户端被逆向破解，从而出现“非会员也能进高等级房间”的破解版本，所以它只适合在您的后台服务器计算再返回客户端。
   我们提供了 privateMapKey 计算代码示例，您可以直接下载并集成到您的服务端：
<table>
<tr><th>语言版本</th><th>签名算法</th><th>关键函数</th><th>下载链接</th></tr>
<tr>
<td>Java</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-java">Github</a></td>
</tr><tr>
<td>GO</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go">GenPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-golang">Github</a></td>
</tr><tr>
<td>PHP</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-php">Github</a></td>
</tr><tr>
<td>Node.js</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-node">Github</a></td>
</tr><tr>
<td>Python</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-python">Github</a></td>
</tr><tr>
<td>C#</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-cs">Github</a></td>
</tr></table>
3. **将 privateMapKey 下发到您的 App 并用来设置 TRTCParams 的 privateMapKey 参数。**


## 常见问题

#### 线上的房间都进不去了？

 房间权限控制一旦开启后，当前 SDKAppID 下的房间就需要在 TRTCParams 中设置 privateMapKey 才能进入，所以如果您线上业务正在运营中，并且线上版本并没有加入 privateMapKey 的相关逻辑，请不要开启此开关。

#### 老版本算法如何计算 privateMapKey？

为了简化签名计算难度，方便客户更快速地使用腾讯云服务，实时音视频自2019年07月19日开始启用新的签名算法，从之前的 ECDSA-SHA256 升级为 HMAC-SHA256，也就是从2019年07月19日之后创建的 SDKAppID 均会采用新的 HMAC-SHA256 算法。

如果您的 SDKAppID 仍然需要继续使用老版本 ECDSA-SHA256 的签名算法，计算 PrivateMapKey 的源码下载链接如下：

| 语言版本 |   签名算法   |      关键函数      |                           下载链接                           |
| :------: | :----------: | :----------------: | :----------------------------------------------------------: |
|   Java   | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/java) |
|   PHP    | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/php) |
| Node.js  | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/nodejs) |

