本文将为您介绍如何使用离线日志功能。

## 前提条件
已完成 [应用接入](https://intl.cloud.tencent.com/document/product/1131/44496)。

## 操作步骤
1. 首先需要开发者在初始化 SDK 的时候开启离线日志
<dx-codeblock>
:::  javascript
new Aegis({
	id: 'xxxxx',
	uin: '123456',
	offlineLog: true, // 开启离线日志（默认关闭）
})
:::
</dx-codeblock>
离线日志将用户数据存储于 localstorage 中，所以对用户业务性能略有影响，开发者可以酌情开启。
2. 登录 [前端性能监控控制台](https://console.cloud.tencent.com/rum)。
3. 在菜单栏左侧单击**离线日志**，进入离线日志页面。
4. 开发者需要对用户进行监听，当用户下次进入页面的时候，就会将存储在本地的离线日志批量上报到服务端。
![](https://qcloudimg.tencent-cloud.cn/raw/a518f485ae5b8ecb113df7ee90844f8f.png)
5. 获取用户的上报信息后，开发者就可以搜索相关的日志了。



### 字段
勾选离线日志列表需要展示的字段。
![](https://qcloudimg.tencent-cloud.cn/raw/ee973bf0d913847bb183771f11d4db60.png)

### 高级搜索
- 支持筛选项目、日志类型、时间等筛选。
- 支持根据用户唯一标识、sessionid、AID、关键词、屏蔽词进行日志筛选。
- 设置离线监听：设置离线日志后，系统会自动拉取 uin/aid 下的离线日志。

### 日志列表
折叠长日志：不折叠一行内将展示所有日志信息，折叠后最多展示8行长日志信息
