## ECDN 接入云监控系统说明

ECDN 已正式接入腾讯云监控系统，当前版本支持的告警指标包括：

<table style="display:table;">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center;width: 100px;"> 指标类别 </th>
			<th colspan="1" style="text-align: center"> 详细指标 </th>
			<th colspan="1" style="text-align: center"> 1分钟告警粒度 </th>
			<th colspan="1" style="text-align: center"> 5分钟告警粒度 </th>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> 访问流量相关指标 </td>
			<td colspan="1" style="text-align: center"> 总请求次数 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 访问带宽 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 访问流量（上行） </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 访问流量（下行） </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> 回源流量相关指标 </td>
			<td colspan="1" style="text-align: center"> 总回源次数 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 回源失败次数 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 回源失败率 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 回源带宽 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center;width: 100px;"> 访问性能相关指标 </td>
			<td colspan="1" style="text-align: center"> 平均响应时间 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> 状态码相关指标 </td>
			<td colspan="1" style="text-align: center"> 200，206，2XX 等状态码次数及占比 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 302，304，3XX 等状态码次数及占比 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 401，403，404，416，4XX 等状态码次数及占比 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 500，502，5XX 等状态码次数及占比 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
			<td colspan="1" style="text-align: center"> 支持 </td>
		</tr>
	</tbody>
</table>

> 
- 您可以免费开通和使用腾讯云监控服务。
- 系统免费通过邮件、微信和回调接口发送告警信息，并且您每月还享有免费的短信告警配额。
- 当超出当月免费告警短信额度后，需要购买短信配额才可以继续通过短信接收告警信息。
- 告警数据实时采集上报，具有一定数据偏差，数据延迟时长约5分钟。
- 监控告警数据仅可用于辅助运营，不可作为计费或 SLA 依据。



## 监控配置入口
登录 [云监控控制台](https://console.cloud.tencent.com/monitor/policylist)，在左侧目录中，单击【告警策略】，进入管理页面。
![](https://main.qcloudimg.com/raw/02656ec03060812cd5f6267856ff779f.png)

## 新增告警配置
新增告警策略配置步骤如下图所示。
1. 填写策略名称、备注提示并选择 ECDN 动态加速告警策略类型。
![](https://main.qcloudimg.com/raw/66f0a21eef4f94a5ec9f515e67e73463.png)
2. 选择告警对象。
![](https://main.qcloudimg.com/raw/a979482d128fc858621a7ba4b658867e.png)
3. 设置告警触发条件，您可以同时设置多条触发条件。
![](https://main.qcloudimg.com/raw/a4582abf188e52c1d10a3b9c44525c29.png)
4. 设置告警接收对象、告警时间段和告警方式。
![](https://main.qcloudimg.com/raw/2224745dd2e051f2ec0e174c1d16a20d.png)
5. 设置告警回调接口。
![](https://main.qcloudimg.com/raw/153f990bd1cd08087c68254ac9ddb253.png)
6. 单击【完成】，确认提交。


## 查看告警
在云监控告警历史页面，您可以查看详细告警信息列表。
![](https://main.qcloudimg.com/raw/03155da8d30984811d6c820428c79aac.png)

## 其他告警策略
告警策略更多配置说明，请参见 [创建告警策略](https://intl.cloud.tencent.com/document/product/248/6215) 文档。
