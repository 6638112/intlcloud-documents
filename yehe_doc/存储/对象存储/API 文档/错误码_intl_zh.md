## 概述

本文将为您介绍请求出错时返回的错误码和对应错误信息。

## 错误响应

Content-Type：application/xml

对应 HTTP 状态码：3XX，4XX，5XX。对于 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 接口，即使 HTTP 状态码为200也有可能在响应体中包含错误。

#### 响应体

```xml
<?xml version='1.0' encoding='utf-8' ?>
<Error>
			<Code>string</Code>
			<Message>string</Message>
			<Resource>string</Resource>
			<RequestId>string</RequestId>
			<TraceId>string</TraceId>
</Error>

```

具体的节点描述如下：

| 节点名称（关键字） | 父节点 | 描述 | 类型 |
| ------------------ | ------ | ------------------ | --------- |
| Error | 无 | 包含所有的错误信息 | Container |

**Container 节点 Error 的内容：**

| 节点名称（关键字） | 父节点 | 描述 | 类型 |
| ------------------ | ------ | ------------------------------------------------------------ | ------ |
| Code | Error | 错误码，用来定位唯一的错误条件和确定错误场景，具体错误码见下文 | string |
| Message | Error | 具体的错误信息 | string |
| Resource | Error | 请求的资源，存储桶地址或对象地址 | string |
| RequestId | Error | 每次请求发送时，服务端将会自动为请求生成一个 ID，遇到问题时，该 ID 能更快地协助 COS 定位问题 | string |
| TraceId | Error | 每次请求出错时，服务端将会自动为这个错误生成一个 ID，遇到问题时，该 ID 能更快地协助 COS 定位问题 | string |

## 错误码列表

### 4XX 类型错误

| HTTP 状态码 | 错误码 | 描述 |
| --------------- | -------------------------- | ----------------- |
| 400 Bad Request | ActionAccelerateNotSupported | 加速域名不支持该操作 |
| 400 Bad Request | AttachmentFull | ACL 和 Policy 数量到达上限。详情请参见 [规格与限制](https://intl.cloud.tencent.com/document/product/436/14518) |
| 400 Bad Request | BadDigest | 提供的 [Content-MD5](https://intl.cloud.tencent.com/document/product/436/7728) 值与服务端收到的请求体的 MD5 哈希值不一致 |
| 400 Bad Request | BadRquest | 参数错误 |
| 400 Bad Request | BucketAccelerateNotEnabled | 该存储桶未启用加速域名 |
| 400 Bad Request | BucketNameTooLong | 存储桶名称过长。详情请参见 [存储桶命名规范](https://intl.cloud.tencent.com/document/product/436/13312) |
| 400 Bad Request | BucketVersionNotOpen | 存储桶未启用版本控制 |
| 400 Bad Request | DNSRecordVerifyFailed | DNS 记录验证失败，请添加 CNAME 或 TXT 记录。DNS 记录可能需要最多10分钟生效 |
| 400 Bad Request | EntitySizeNotMatch | 请求体大小与 [Content-Length](https://intl.cloud.tencent.com/document/product/436/7728) 请求头不符 |
| 400 Bad Request | EntityTooLarge | 上传的对象大小超过规定的最大值。详情请参见 [规格与限制](https://intl.cloud.tencent.com/document/product/436/14518) |
| 400 Bad Request | EntityTooSmall | 上传的对象大小不足规定的最小值，常见于分块上传。详情请参见 [规格与限制](https://intl.cloud.tencent.com/document/product/436/14518) |
| 400 Bad Request | ExpiredToken | 临时密钥 Token 已过期 |
| 400 Bad Request | ImageResolutionExceed | 图片分辨率超出限制或动图帧数过多 |
| 400 Bad Request | ImageTooLarge | 图片超过限制大小 |
| 400 Bad Request | IncompleteBody | 请求体大小小于 [Content-Length](https://intl.cloud.tencent.com/document/product/436/7728) 请求头 |
| 400 Bad Request | IncorrectNumberOfFilesInPostRequest | POST Object 请求每次只允许上传一个对象 |
| 400 Bad Request | InvalidArgument | 请求参数不合法，请确认是否允许携带该请求参数 |
| 400 Bad Request | InvalidBucketName | 存储桶名称不合法。详情请参见存储桶 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) |
| 400 Bad Request | InvalidCopySource | 复制对象源不合法 |
| 400 Bad Request | InvalidDelimiter | 分隔符（delimiter）参数不合法，分隔符只能为一个字符 |
| 400 Bad Request | InvalidDigest | 给定的 [Content-MD5](https://intl.cloud.tencent.com/document/product/436/7728) 值不合法 |
| 400 Bad Request | InvalidImageFormat | 图片格式不合法 |
| 400 Bad Request | InvalidImageSource | 图片源不合法 |
| 400 Bad Request | InvalidLocationConstraint | 指定的 location 不合法 |
| 400 Bad Request | InvalidObjectName | 对象名称不合法。详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) |
| 400 Bad Request | InvalidPart | 分块缺失 |
| 400 Bad Request | InvalidPartOrder | 分块的编号不连续 |
| 400 Bad Request | InvalidPicOperations | Pic-Operations 请求头不合法 |
| 400 Bad Request | InvalidPolicyDocument | POST Object 请求中的策略（Policy）不合法 |
| 400 Bad Request | InvalidRegionName | 不合法的地域名。详情请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) |
| 400 Bad Request | InvalidRequest | 请求不合法 |
| 400 Bad Request | InvalidSHA1Digest | 请求内容 SHA1 校验不合法 |
| 400 Bad Request | InvalidTag | 存储桶标签不合法。详情请参见 [存储桶标签概述 ](https://intl.cloud.tencent.com/document/product/436/31509) |
| 400 Bad Request | InvalidTargetBucketForLogging | 用于存放日志的目标存储桶不合法，目标存储桶必须与当前存储桶在同一个地域 |
| 400 Bad Request | InvalidUploadStatus | 当启用版本控制时不能使用 JSON API 上传对象，请使用 XML API |
| 400 Bad Request | InvalidURI | URI 不合法 |
| 400 Bad Request | InventoryFull | 清单任务数量已达到限制。清单任务上限1000条 |
| 400 Bad Request | JsonAPINotSupportOnMAZBucket | JSON API 不支持操作多 AZ 存储桶，请使用 XML API |
| 400 Bad Request | KeyTooLong | 对象键过长。详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) |
| 400 Bad Request | KmsException | 密钥管理服务异常 |
| 400 Bad Request | KmsKeyDisabled | 提供的密钥已被禁用 |
| 400 Bad Request | KmsKeyNotExist | 提供的密钥不存在 |
| 400 Bad Request | ListPartUploadIdIsEmpty | UploadId 为空 |
| 400 Bad Request | LoggingConfExists | 日志配置已存在 |
| 400 Bad Request | LoggingPrefixInvalid | 日志前缀参数不合法 |
| 400 Bad Request | MalformedPolicy | 策略格式不合法 |
| 400 Bad Request | MalformedPOSTRequest | 该 POST 请求的请求体内容不合法 |
| 400 Bad Request | MalformedXML | 请求体的 XML 格式不符合 XML 语法 |
| 400 Bad Request | MAZOperationNotSupportOnOAZBucket | 单可用区（单 AZ）存储桶不支持多可用区（多 AZ）操作。关于多 AZ 特性及使用限制的说明请参见 [多 AZ 特性概述](https://intl.cloud.tencent.com/document/product/436/35208) </br>The multiple availability zones operation is not supported by single availability zone bucket |
| 400 Bad Request | MissingRequestBodyError | 请求体缺失 |
| 400 Bad Request | MultiAZFeatureNotSupport | 当前地域不支持多可用区 |
| 400 Bad Request | MultiBucketNotSupport | 跨地域复制只能设置一个目的存储桶 |
| 400 Bad Request | NotifyRuleEventConflict | 通知规则 Event 冲突 |
| 400 Bad Request | NotifyRulePrefixConflict | 通知规则 Prefix 冲突 |
| 400 Bad Request | NotifyRuleSuffixConflict | 通知规则 Suffix 冲突 |
| 400 Bad Request | NotSupportedStorageClass | 指定的 [存储类型](https://intl.cloud.tencent.com/document/product/436/30925) 不支持 |
| 400 Bad Request | OAZOperationNotSupportOnMAZBucket | 多可用区存储桶不支持单可用区操作。关于多 AZ 特性及使用限制的说明请参见 [多 AZ 特性概述](https://intl.cloud.tencent.com/document/product/436/35208) </br> The single availability zone operation is not supported by multiple availability zones bucket |
| 400 Bad Request | PolicyFull | ACL 和 Policy 数量到达上限。详情请参见 [规格与限制](https://intl.cloud.tencent.com/document/product/436/14518) |
| 400 Bad Request | PolicyVersionFull | Policy 版本数量到达上限 |
| 400 Bad Request | RequestTimeout | 请求超时 |
| 400 Bad Request | SsecDecryptHeaderInvalid | 源文件使用 SSE-C 加密，需要在请求头中提供相同的密钥 |
| 400 Bad Request | SSEContentNotSupported | 加密方式不支持 |
| 400 Bad Request | SSEHeaderNotAllowed | 该操作不支持指定的服务端加密头部 |
| 400 Bad Request | TargetBucketNameInvalid | 目标存储桶名称不合法。详情请参见存储桶 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) |
| 400 Bad Request | TooManyBuckets | 存储桶数目达到上限200 |
| 400 Bad Request | UnexpectedContent | 请求不支持相关内容 |
| 400 Bad Request | UserCnameInvalid | 用户指定的 CNAME 不存在或不合法 |
| 400 Bad Request | UserNetworkTooSlow | 用户的网络速度过慢 |
| 400 Bad Request | VerifyAlgorithmNotSupported | 校验算法不支持 |
| 400 Bad Request | WebsiteURLInvalid | 自定义域名 URL 不合法 |
| 400 Bad Request | XMLSizeLimit | XML 长度超过限制 |
| 402 Payment Required | PaymentRequired | 超出费用配额限制 |
| 403 Forbidden | AccessDenied | 签名或者权限不正确，拒绝访问。请参考 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 和 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) |
| 403 Forbidden | AccessForbidden | 跨域资源共享（CORS）请求被拒绝，请检查请求方法或请求头部中的 Origin、Access-Control-Request-Method、Access-Control-Request-Headers 是否在配置的 CORS 白名单中 |
| 403 Forbidden | InvalidAccessKeyId | SecretID 不存在 |
| 403 Forbidden | InvalidObjectState | 对象存储类型与操作请求冲突 |
| 403 Forbidden | NoProcessAuthority | 没有处理图片的权限 |
| 403 Forbidden | RequestTimeTooSkewed | 本地时间与服务器时间相差过大，超过15分钟 |
| 403 Forbidden | Request has expired | 发起请求的时间超过了签名的有效时间，或者本地系统时间和所在时区的时间不一致。详情请参见 [常见问题](https://intl.cloud.tencent.com/document/product/436/10687) |
| 403 Forbidden | SignatureDoesNotMatch | 客户端计算的签名与 COS 服务端计算的签名不一致。请参阅 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档并借助COS 请求签名工具 检查自行实现的签名过程 |
| 403 Forbidden | UserNotSourceBucketOwner | 当前用户不是源存储桶的拥有者 |
| 403 Forbidden | UserNotTargetBucketOwner | 当前用户不是目标存储桶的拥有者 |
| 404 Not Found | InventoryConfigurationNotFoundError | 清单配置未找到 |
| 404 Not Found | NoBucketQuotaPolicy | 存储桶配额策略不存在 |
| 404 Not Found | NoSuchBucket | 指定的存储桶不存在 |
| 404 Not Found | NoSuchCopySource | 复制对象源不存在 |
| 404 Not Found | NoSuchCORSConfiguration | 指定的跨域资源共享配置不存在 |
| 404 Not Found | NoSuchEncryptionConfiguration | 指定的存储桶加密配置不存在 |
| 404 Not Found | NoSuchJob | 指定的批量处理任务不存在 |
| 404 Not Found | NoSuchKey | 指定的对象键不存在。检查对象是否存在请使用 [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) 接口 |
| 404 Not Found | NoSuchLifecycleConfiguration | 指定的生命周期配置不存在 |
| 404 Not Found | NoSuchObjectLockConfiguration | 指定的对象锁定配置不存在 |
| 404 Not Found | NoSuchPolicyVersion | 指定的策略版本不存在 |
| 404 Not Found | NoSuchTagSet | 指定的标签集合不存在 |
| 404 Not Found | NoSuchUpload | 分块上传时指定的 UploadId 不存在 |
| 404 Not Found | NoSuchVersion | 指定版本不存在 |
| 404 Not Found | NoSuchWebsiteConfiguration | 指定的静态网站配置不存在 |
| 404 Not Found | OriginConfigurationNotFoundError | 回源配置未找到 |
| 404 Not Found | ReplicationConfigurationNotFoundError | 跨地域复制配置未找到 |
| 405 Method Not Allowed | MethodNotAllowed | 此资源不支持该 HTTP 方法 |
| 405 Method Not Allowed | RestoreNonArchiveObject | 不允许对非归档对象进行回热（恢复） |
| 405 Method Not Allowed | UploadIdNotSupported | 指定的 UploadId 由 JSON API 生成，不能使用 XML API 操作 |
| 409 Conflict | AppendPositionErr | Append 操作时，对象长度和 Position 不一致 |
| 409 Conflict | BucketAlreadyExists | 指定的存储桶已存在 |
| 409 Conflict | BucketAlreadyOwnedByYou | 指定的存储桶已存在且由当前帐户创建 |
| 409 Conflict | BucketLocked | 存储桶已锁定，不能操作跨地域复制或生命周期 |
| 409 Conflict | BucketNotEmpty | 存储桶不为空 |
| 409 Conflict | DomainConfigConflict | 域名配置冲突，请删除冲突的记录 |
| 409 Conflict | InvalidBucketState | 存储桶状态与操作请求冲突，例如版本控制管理与跨地域复制的冲突 |
| 409 Conflict | InvalidLockedTime | 对象锁定时间无效 |
| 409 Conflict | ObjectLocked | 对象已锁定，不允许覆盖上传或删除该对象，也不允许通过复制修改该对象的元数据 |
| 409 Conflict | InvalidObjectState | 对象状态与操作请求冲突 |
| 409 Conflict | PathConflict | 存在同名对象的毫秒级并发冲突 |
| 409 Conflict | QuotaConflict | 配额冲突 |
| 409 Conflict | QuotaOperationConflict | 该存储桶的状态不适用于该操作 |
| 409 Conflict | RecordAlreadyExist | DNS 记录冲突，请删除冲突的记录，或添加 CNAME/TXT 记录 |
| 409 Conflict | RestoreAlreadyInProgress | 该对象正在回热（恢复）中 |
| 409 Conflict | UploadConflict | 同一个对象键频繁上传会导致冲突 |
| 409 ObjectNotAppendale | ObjectNotAppendable | 指定的对象不能追加 |
| 411 Length Required | MissingContentLength | [Content-Length](https://intl.cloud.tencent.com/document/product/436/7728) 请求头部缺失 |
| 412 Precondition Failed | PreconditionFailed | 前置条件不匹配 |
| 416 Requested Range Not Satisfiable | InvalidRange | 请求的对象范围不合法 |
| 451 Unavailable For Legal Reasons | DomainAuditFailed | 域名未备案 |
| 451 Unavailable For Legal Reasons | UnavailableForLegalReasons | 当前服务不可用，请检查账号是否欠费，若无欠费可通过 [内容合规](https://console.cloud.tencent.com/cos5/compliance) 查看是否存在违规内容 |


### 5XX 类型错误

| HTTP 状态码 | 错误码 | 描述 |
| --------------- | -------------------------- | ----------------- |
| 500 Internal Server Error | InternalError | 服务端内部错误 |
| 500 Internal Server Error | KmsInternalException | 查询密钥管理服务时发生服务端内部错误 |
| 501 Not Implemented | NotImplemented | 请求尚未实现 |
| 503 Service Unavailable | KmsFreqControl | 请降低使用密钥管理服务的请求的访问频率 |
| 503 Service Unavailable | ServiceUnavailable | 服务暂不可用，请重试 |
| 503 Service Unavailable | SlowDown | 请降低访问频率 |

### 数据处理相关错误码


#### 图片下载时处理错误码

| 错误码 | 说明 | 处理措施 |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -103 | 无效的请求；请求报文无法识别。 | 请检查请求内容。 |
| -104 | 无效的 APPID，URL 中包含的 APPID 无效，或者域名没有和 APPID 绑定。 | 请检查 APPID 是否正确。|
| -105 | 无效的样式名，URL 中指定的样式名或者别名没有配置。 | 请检查样式配置或样式名内容。|
| -106 | 无效的 URL，URL 格式不符合格式要求。 | 请检查 URL 格式。 |
| -107 | 无效的 Host 头域。 | 请检查 Host 是否正确。 |
| -108 | 无效的 Referer。 | 请检查相关 Referer 配置。 |
| -109 | 无效的样式名 ID。没有找到该样式名对应的图片。可能是上传该图片后，新增的样式名， 因此图片上传时不能生成该样式名对应的数据。 | - |
| -110 | 该图片在黑名单中。 | - |
|-113 | 该文档的类型不支持 | 文档预览目前所支持的输入文件类型，请参见 [规则与限制](https://intl.cloud.tencent.com/document/product/1045/33425) |
| -120 | 回源到源站获取数据时，源站返回的数据有异常，无法正常获取到图片数据。 | 请检查源站数据。 |
| -124 | 下载偏移错误。HTTP 请求的 Range 断点续传偏移量可能设置错误。 | 请检查断点续传偏移量的相关配置。|
| -154 | 原图保护机制禁止该 URL 下载。 | 请使用样式访问。 |
| -156 | 强制执行302流程。 | - |
| -162 | 业务配置为欠费，禁止下载图片。 | 请及时充值。 |
| -163 | 业务配置不存在。 | 请检查相关配置项。 |
| -164 | 热图下载，限制。 | 请降低请求频率，或 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。 | -
| -165 | 攻击性下载请求，限制。 | - |
| -166 | 消息格式错误。 | - |
| -167 | 文件太大，无法支持图片下载。 | 请降低图片大小。 |
| -168 | 文件太大，无法支持图片下载。 | 请降低图片大小。 |
| -441 | 图片格式不符，无法进行压缩。 | 请使用数据万象支持的图片格式进行图片处理操作。具体支持格式为 jpg、bmp、gif、png、webp。 | -
| -442 | 图片超过限制大小。 | 请将图片长宽限制在9999像素以内。 |
| -443 | 图片格式不满足处理限制。 | 请使用支持的图片格式进行处理，详情请参见 [规则与限制](https://intl.cloud.tencent.com/document/product/1045/33425) |
| -447 | 图片分辨率超出限制或动图帧数过多。 | 请将图片长宽限制在9999像素以内（动图请限制帧数）。 |
| -901 | 压缩超时。 | - |
| -902 | 回源超时，镜像存储功能把请求转发到开发商源站，但没有收到响应，超时了。 | 请检查源站数据或回源配置。|
| -3006 | 该文档被加密，无法解析。 | - |
| -3008 | 该文件为空文件，无法解析。 | - |
| -3011 | 该文档的类型不支持。 | 文档预览目前所支持的输入文件类型，请参见 [规则与限制](https://intl.cloud.tencent.com/document/product/1045/33425) |
| -3015 | 请求的页码不存在。 | - |
| -3075 | 该文档超过100MB，无法解析。 | 输入文件大小需限制在100MB之内 |
| -5062 | 图片涉嫌违禁。 | 请检查图片内容是否违规。 |
| -6101 | 图片不存在、图片没有上传或者图片已经删除。 | 请检查请求源数据。 |
| -29033 | 下载请求无有效的 range。 | - |
| -29034 | 下载的 offset 大于文件 size。 | - |
| -29214 | 触发频控。 | 请降低请求频率，或 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。 |
| -40168 | 原图为空数据。 | 请检查请求源数据。 |
| -46152 | 非法的 bucketName。 | 请检查存储桶名称是否正确。 |
| -46154 | 非法的 APPID。 | 请检查 APPID 是否正确。 |
| -46614 | 文件尚未上传完成，禁止下载。 | 请等待文件上传成功后请求。 |
| -46617 | 命中黑名单。 | 请检查图片内容是否违规。 |
| -46618 | 签名校验失败。 | 请检查签名是否准确。 |
| -46619 | 签名过期。 | 请更新签名。 |
| -46620 | Bucket 被封禁。 | 您的 Bucket 已被封禁，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。 | -
| -46621 | 文件被封禁。 | 您的资源已被封禁，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。 |
| -46627 | 用户目前在黑名单中。 | 您的账号已被封禁，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。 |
| -46628 | 文件不存在。 | 请确认请求下载的文件是否真实存在。 |
| -46642 | APPID 不存在。 | 请检查 APPID 是否正确。 |
| -46646 | 文件已封禁。 | 文件已被封禁，请检查文件内容是否违规。 |
| -46661 | 无权访问 | 请联系资源所有者授予权限。 |


#### 图片持久化处理错误码

| 错误码 | 说明 | 处理措施 |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|-60998|图片处理参数无效。|请检查图片处理规则是否正确。|
|-60997|图片处理规则过多。|持久化处理当前最多支持五条规则，请控制在五条以内。|
|-60996|文件太大，无法处理。|请将文件控制在32MB以内。|
|-60987|图片获取失败。|请检查图片 URL。|
|-60983|无效的 Host。|请检查 Host。|
|-60972|无效地域。|请检查请求地域是否支持数据万象服务。数据万象现有地域详见 [地域与域名](https://intl.cloud.tencent.com/document/product/1045/33423)。|
|-60967|图片样式不存在。|请检查图片样式。|
|-60957|样式数量超过上限。|当前样式数量上限为100条，如需更多样式请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们。|
|-60955|无效的 URL。|请检查 URL 是否正确。|
|-60950|未指定文件。|请在请求中指定需要处理的文件。|
|-60949|请求频率过高。|请放缓请求频率。如有需要请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们提升频率限制。|
|-60948|账号涉嫌违规。|您的 APPID 已被封禁，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。|
|-60938|签名信息不完整。|请检查签名信息中的必选项。|
|-60936|请求被拒绝。|AccessDenied。|
|-60932|签名错误。|签名无效，请检查签名信息是否匹配。|
|-62999|无效的图片格式。|请检查图片格式是否正确。|

#### 文档预览错误码


| 错误码 | 说明 | 处理措施 |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|-3006 | 文档为加密文件 | 建议使用已解密的文档。 |
|-3008 | 文档长度为0 | 请确认文档是否正常。 |
|-3011 | 文档类型不支持 | 请确认文档是否在支持范围内，支持的文档类型详情请参见 [规则与限制](https://intl.cloud.tencent.com/document/product/1045/33425)。 |
|-3015 | 请求的页数超过了文档总页数 | 请检查请求页数是否正确。 |


#### 内容审核错误码

| 错误码 | 说明 | 处理措施 |
| :----- | :----------------------------------------------------------- | :----------------------------------------------- |
| -61011 | 文件不存在。 | 请检查文件是否存在。 |
| -65007 | 文件内容错误，解码失败。 | 请检查文件格式是否正确。 |
| -65010 | 下载文件失败。 | 请检查文件链接是否正确，私有读文件需要携带签名。 |
| -65011 | 文件过大，无法处理。 | 当前不支持审核过大的文件。 |
| -65012 | 图片分辨率过小，无法处理。 | 当前不支持分辨率过小的图片。 |
| -65013 | 不符合要求（例如不支持识别的文件后缀、文件过大等），未进行处理。 | 请检查文件是否符合规则。 |
| -65014 | 没有数据万象角色 CI_QCSRole。 | 请绑定数据万象角色。 |
| -65015 | 未启用审核场景。 | 请使用至少一种审核场景进行审核。 |
| -65016 | 使用的 BizType 不存在。 | 请填写正确的 BizType。 |
| 其他 | 内部错误 | 无。 |
