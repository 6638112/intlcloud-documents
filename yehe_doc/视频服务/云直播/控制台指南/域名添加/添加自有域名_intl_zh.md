使用云直播服务，至少需要**2个**域名，一个作为推流域名，一个作为播放域名，且推流和播放不能使用相同的域名。

## 前提条件
已开通 [腾讯云直播服务](https://intl.cloud.tencent.com/product/css)。


## 操作步骤
[](id:step1)
### 步骤1：添加自有域名
1. 登录  [云直播控制台](https://console.cloud.tencent.com/live)，选择 **域名管理** 。
2. 单击 **添加域名**，进入域名添加页进行如下配置：
    1. 若您需添加**推流域名**：输入域名，选择域名类型为 **推流域名**，单击 **确定** 即可。
    2. 若您需添加**播放域名**：输入域名，选择域名类型为 **播放域名**，选择加速区域，默认为 **中国大陆** 。 单击 **确定** 即可。

![](https://qcloudimg.tencent-cloud.cn/raw/bde55a20b40da9d2d0fe2eda9613b63b.png)

>! 
>- 域名的位数限制为45位，暂不支持大写的域名，请输入不超过**45位**的小写域名地址。
>- 每个账户默认限制可管理100个域名，如果业务量级较大，可 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请增加域名数量上限。
>- 自有域名添加成功后，您可通过域名管理列表，单击需要修改的域名或右侧 **管理** 进入域名详情页，选择 **高级配置** 查看 **区域配置** 标签，单击选择 **编辑**，即可进入区域配置修改页，重新选择加速区域，单击 **保存** 即可。

[](id:step2)
### 步骤2：完成域名 CNAME
域名添加成功后，系统会为您自动分配一个 CNAME 域名（以`.tlivecdn.com`为后缀）。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后，即可享受云直播服务。具体操作请参见 [CNAME 配置](https://intl.cloud.tencent.com/document/product/267/31057)。

>? 若您需要对已添加成功的域名进行管理，请参见 [域名管理](https://intl.cloud.tencent.com/document/product/267/31056)。

## 常见问题
- [云直播播放域名有什么要求？](https://intl.cloud.tencent.com/document/product/267/7968)
- [直播域名接入播放域名和推流域名可以是同一个吗？能使用二级域名吗？](https://intl.cloud.tencent.com/document/product/267/7968)
