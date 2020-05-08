## 简介
本文档提供腾讯移动推送 Android 应用快速接入指引。只需四步，即可在您的 Android 应用上面使用腾讯移动推送服务。
## 接入前准备
1. 接入 SDK 之前，需要您前往腾讯移动推送 [控制台](https://console.cloud.tencent.com/tpns) 创建产品和 Android 应用，详细操作可参考 [创建产品和应用](https://intl.cloud.tencent.com/document/product/1024/32603) 文档。
 
2. 应用创建完成后，您可以参考 [申请试用](https://intl.cloud.tencent.com/document/product/1024/32603#.E7.94.B3.E8.AF.B7.E8.AF.95.E7.94.A8) ，为当前应用申请试用权限。
3. 完成以上步骤后，进入应用的【配置管理】页面，准备接入。

## 开始接入
1.在【配置管理】页面中， 单击【快速接入】按钮。
2.按照接入指引的操作顺序完成配置，然后点击验证按钮。
3.若出现以下提示，则表示SDK接入成功 。

- 若出现以下提示，请确认该应用是否开通试用或购买了推送服务。

可在[产品管理](https://console.cloud.tencent.com/tpns)页面查看当前应用服务状态，在您申请试用或购买后30分钟内可开通服务。

- 若出现以下提示，请确认App是否成功注册推送服务，可参考[接入结果验证](#jierujieguo)。

<span id="jierujieguo"></span>
## 接入结果验证
1. 运行 App，过滤"TPush"关键字，查看相关日志：
![](https://main.qcloudimg.com/raw/3534e6c05ab9f6959e6e19d4272dc48b.png)
如出现有类似上图日志，则表明 TPNS-SDK 的插件集成方式已经成功。

2. 推送服务注册成功的日志如下：
```
XG register push success with token:6ed8af8d7b18049d9fed116a9db9c71ab44d5565
```
若未搜索到 Token，请查看注册接口返回的错误码，根据 [错误码对照表](https://intl.cloud.tencent.com/document/product/1024/30722) 排查。

## 厂商通道快速接入
1.在配置管理页面打开厂商推送通道开关并配置好应用的 AppId、SecretKey 等信息，申请方式可单击查看各厂商通道的说明文档。
2.厂商通道信息配置完成后，单击页面上方【配置文件下载】按钮，下载包含厂商通道配置信息的配置文件，然后用该配置文件替换工程文件中旧的配置文件即可。
![](https://main.qcloudimg.com/raw/4dfa37ac471c1c3b18cc559d5780a6be.png)

## 问题排查指引
1. 插件日志
如果集成出现异常，则将 tpns-configs.json 文件中的 "debug" 字段置为 true，运行命令： 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
并通过 "TpnsPlugin" 关键字进行分析。
2. sync projects。
![](https://main.qcloudimg.com/raw/30368ed3cb4a25f3c33be46e3c1f2f5d.png)
3. 在项目的 External Libraries 中查看是否有相关依赖。
![](https://main.qcloudimg.com/raw/1de82d05f351939883e1870ae7300c44.png)
