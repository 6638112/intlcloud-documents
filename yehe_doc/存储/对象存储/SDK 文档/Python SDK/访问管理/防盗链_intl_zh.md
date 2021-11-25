## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。

>! 需要 COS PYTHON SDK v5.1.9.7 及以上版本。
>

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

## 设置存储桶 Referer

#### 功能说明

设置指定存储桶的 Referer 白名单或者黑名单（PUT Bucket referer）。

#### 方法原型

```python
put_bucket_referer(Bucket, RefererConfiguration, **kwargs)
```

#### 请求示例

```python
# 设置用户属性, 包括 secret_id, secret_key, region等。Appid 已在CosConfig中移除，请在参数 Bucket 中带上 Appid。Bucket 由 BucketName-Appid 组成
secret_id = 'SecretId'     # 替换为用户的 SecretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'   # 替换为用户的 SecretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
                           # COS支持的所有region列表参见https://www.qcloud.com/document/product/436/6224
token = None               # 如果使用永久密钥不需要填入token，如果使用临时密钥需要填入，临时密钥生成和使用指引参见https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  
client = CosS3Client(config)
referer_config = {
    'Status': 'Enabled',
    'RefererType': 'White-List',
    'EmptyReferConfiguration': 'Allow',
    'DomainList': {
        'Domain': [
            '*.qq.com',
            '*.qcloud.com'
        ]
    }
}
response = client.put_bucket_referer(
    Bucket='examplebucket-1250000000',
    RefererConfiguration=referer_config
)
```

#### 参数说明

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |
| RefererConfiguration | 存储桶 Referer 配置                                               | Dict |

RefererConfiguration 说明：

| 参数名          | 参数描述                                         | 类型    | 是否必填 |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Status         | 是否开启防盗链，枚举值：Enabled、Disabled           | String | 是   |
| RefererType    | 防盗链类型，枚举值：Black-List、White-List          | String | 是   |
| DomainList         | 生效域名的列表                                 | Dict | 是   |
| Domain         | 生效域名，支持带端口和 IP、支持通配符\*, 支持多条        | List | 是   |
| EmptyReferConfiguration | 是否允许空 Refer 访问，枚举值： Allow、Deny | String | 否  |

#### 返回结果说明
该方法返回值为 None。

## 查询存储桶 Referer

#### 功能说明

查询指定存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

#### 方法原型

```python
get_bucket_referer(Bucket, **kwargs)
```

#### 请求示例

```python
response = client.get_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### 参数说明

| 参数名       | 参数描述  | 类型  |
| ----------- | -------- | ---- |
| bucketName  | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |

#### 返回结果说明
返回存储桶的 Referer 配置，参见 RefererConfiguration 说明。

## 删除存储桶 Referer

#### 功能说明

删除指定存储桶 Referer 白名单或者黑名单（DELETE Bucket referer）。

#### 方法原型

```python
delete_bucket_referer(Bucket, **kwargs)
```

#### 请求示例

```python
response = client.delete_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### 参数说明

| 参数名       | 参数描述  | 类型  |
| ----------- | -------- | ---- |
| bucketName  | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |

#### 返回结果说明
该方法返回值为 None。
