## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

## 设置存储桶 Referer

#### 功能说明

设置指定存储桶的 Referer 白名单或者黑名单（PUT Bucket referer）。

#### 方法原型

```go
func (s *BucketService) PutReferer(ctx context.Context, opt *BucketPutRefererOptions) (*Response, error)
```

#### 请求示例

```go
opt := &cos.BucketPutRefererOptions{
	Status:      "Enabled",
	RefererType: "White-List",
	DomainList: []string{
		"*.qq.com",
		"*.qcloud.com",
	},
	EmptyReferConfiguration: "Allow",
}
  
_, err := c.Bucket.PutReferer(context.Background(), opt)
```

#### 参数说明

```go
type BucketPutRefererOptions struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status                         | 是否开启防盗链，枚举值：Enabled、Disabled | String                                   |
| RefererType | 防盗链类型，枚举值：Black-List、White-List                | String |
| DomainList | 生效域名，支持带端口和 IP、支持通配符\*, 支持多条 | Array |
| EmptyReferConfiguration | 是否允许空 Refer 访问，枚举值： Allow、Deny | String |

## 查询存储桶 Referer

#### 功能说明

查询指定存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

#### 方法原型

```go
func (s *BucketService) GetReferer(ctx context.Context) (*BucketGetRefererResult, *Response, error)
```

#### 请求示例

```go
res, _, err := c.Bucket.GetReferer(context.Background())
```

#### 返回结果说明

```go
type BucketGetRefererResult struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status                         | 是否开启防盗链，枚举值：Enabled、Disabled | String                                   |
| RefererType | 防盗链类型，枚举值：Black-List、White-List                | String |
| DomainList | 生效域名，支持带端口和 IP、支持通配符\*, 支持多条 | Array |
| EmptyReferConfiguration | 是否允许空 Refer 访问，枚举值： Allow、Deny | String |
