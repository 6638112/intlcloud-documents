直播截图是指以固定的时间间隔截取实时直播流的图像，并生成图片。您可以通过回调通知获取截图信息，截图数据可应用于直播鉴黄、直播房间封面等多种场景。

## 注意事项

- 阅读本文之前，希望您已经了解腾讯云直播是如何配置回调功能、您是如何接收回调消息的，具体请参见 [如何接收事件通知](https://intl.cloud.tencent.com/zh/document/product/267/38080)。
- 截图回调事件触发后获取的截图信息可应用于直播鉴黄、直播房间封面等多种场景。

## 截图事件参数说明

### 事件类型参数

| 事件类型 | 字段取值说明           |
| :------- | :------------- |
| 直播截图 | event_type = 200 |

### 回调公共参数
<table>
<tr><th>字段名称</th><th>类型</th><th>说明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>过期时间，事件通知签名过期 UNIX 时间戳。<ul style="margin:0"><li>来自腾讯云的消息通知默认过期时间是10分钟，如果一条消息通知中的 t 值所指定的时间已经过期，则可以判定这条通知无效，进而可以防止网络重放攻击。<li>t 的格式为十进制 UNIX 时间戳，即从1970年01月01日（UTC/GMT 的午夜）开始所经过的秒数。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>事件通知安全签名 sign = MD5（key + t）。<br>说明：腾讯云把加密 <a href="#key">key</a> 和 t 进行字符串拼接后通过 MD5 计算得出 sign 值，并将其放在通知消息里，您的后台服务器在收到通知消息后可以根据同样的算法确认 sign 是否正确，进而确认消息是否确实来自腾讯云后台。</td>
</tr></table>

>? <span id="key"></span>key 为【功能模板】>[【回调配置】](https://console.cloud.tencent.com/live/config/callback)中的回调密钥，主要用于鉴权。为了保护您的数据信息安全，建议您填写。
>![](https://main.qcloudimg.com/raw/34b21b2d50d2aca00dd2dfa19816e8e3.png)

### 回调消息参数


| 字段名称     | 类型   | 说明                        |
| :----------- | :----- | :-------------------------- |
| stream_id    | string | 直播流名称                  |
| channel_id   | string | 同直播流名称                |
| create_time  | int64  | 截图生成 UNIX 时间戳        |
| file_size    | int    | 截图文件大小，单位为字节    |
| width        | int    | 截图宽，单位为像素          |
| height       | int    | 截图高，单位为像素          |
| pic_url      | string | 截图文件路径 `/path/name.jpg`  |
| pic_full_url | string | 截图下载 URL                |

### 回调消息示例

```
{
"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```








