
## 操作场景
物联网通信平台支持设备级密钥认证，在该模式下，用户需要每个设备烧录不同的配置固件，平台将根据用户选择的具体认证方式（证书认证/密钥认证）进行鉴权验证，成功通过后即可与平台建立连接，进行数据通信。


## 流程图
设备级密钥需要为每个设备烧录不同的固件，在产线应用中有一定实现成本，但安全性更高，推荐使用。



## 操作步骤
1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)，创建产品与设备。具体创建步骤请参考 [设备接入准备](https://intl.cloud.tencent.com/document/product/1105/41476)。
2. 在产品详情页获取产品信息，在设备详情页获取设备名称、设备证书/密钥。
 - 产品信息
![](https://main.qcloudimg.com/raw/aca400b6f81833f551e2dd9b428cc210.png)
 - 设备信息
![](https://main.qcloudimg.com/raw/64862bbc5a5aface8f45a6de0d4c2dd7.png)
3. 设备固件烧录，具体步骤如下：
 1. 下载 [设备端 SDK](https://intl.cloud.tencent.com/document/product/1105/41840)。
 2. 实现 SDK 中关于产品、设备信息读写的 HAL 层函数，包括 ProductID、Devicename 与设备证书或密钥，具体可参考 [设备接入](https://intl.cloud.tencent.com/document/product/1105/41842)。
 3. 根据实际业务需求基于 SDK 开发设备端固件，实现设备唯一标识的读取、设备动态注册、鉴权接入、通信及 OTA 等功能。
 4. 在生产环节，将开发测试完成的设备端固件批量烧录至设备中。
4. 设备使用烧录的设备级证书/密钥与平台发起连接，鉴权通过后完成设备激活上线，即可与云端进行数据交互，实现业务需求。



