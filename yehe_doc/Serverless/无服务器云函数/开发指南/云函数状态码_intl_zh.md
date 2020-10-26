对于函数运行后抛出的错误信息，您可以检索错误内容找到对应的问题产生原因和解决方案。



<table>
<thead>
<tr>
<th>状态码及状态消息</th>
<th>说明</th>
<th>解决方法</th>
</tr>
</thead>
<tbody>

<tr>
<td>200<br>Success</td>
<td>成功。</td>
<td>-</td>
</tr>

<tr>
<td>400<br>BadRequest</td>
<td>当函数执行传入参数错误时，会有该返回信息。</td>
<td><ul class="params"><li>检查函数调用传入参数是否正确，可以根据错误信息提示进行检查。</li>
<li>参数不符合规范，请参考<a href="https://intl.cloud.tencent.com/document/product/583/17234" target="_blank" rel="noopener noreferrer"> API 文档 </a>修改参数后重试。。</li></ul></td>
</tr>

<tr>
<td>401<br>InvalidCredentials</td>
<td>认证失败。</td>
<td>-</td>
</tr>

<tr>
<td>403<br>ResourceUnavailable</td>
<td>资源不可用。</td>
<td>-</td>
</tr>

<tr>
<td>404<br>InvalidSubnetID</td>
<td>当函数执行执调用时子网 ID 错误时，会有该返回信息。</td>
<td>检查函数的 <a href="https://intl.cloud.tencent.com/document/product/583/38377" target="_blank" rel="noopener noreferrer">网络配置</a> 信息是否正确以及子网 id 是否有效。</td>
</tr>

<tr>
<td>406<br>RequestTooLarge</td>
<td>函数调用请求参数体太大时，会有该返回信息。</td>
<td><ul class="params"><li>可以根据产品文档，缩小请求参数大小。</li>
<li>此处判断参数过大是针对用户请求体大小，同步6M以内，异步128k（检查传入 req body）。</li></ul></td>
</tr>

<tr>
<td>430<br>UserFunctionExecError</td>
<td>当用户代码执行出现错误时，会有该返回信息。</td>
<td>可以根据控制台的错误日志，查看代码错误堆栈信息，检查代码是否能正常执行。</td>
</tr>

<tr>
<td>432<br>ResourceLimitReached</td>
<td>当并发超出限制时，会有该返回信息。</td>
<td>可 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">提交工单</a> 申请提升并发限制。</td>
</tr>

<tr>
<td>433<br>TimeLimitReached</td>
<td>当函数执行时间超出超时配置，会有该返回信息。</td>
<td><ul class="params"><li>检查业务代码是否有大量耗时处理操作。</li>
<li>配置更长的超时时间，如果当前已是最大时间设置，可 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">提交工单</a> 申请提升超时限制。</li></ul></td>
</tr>

<tr>
<td>434<br>MemoryLimitReached </td>
<td>当函数执行使用内存超过配置内存时，会有该返回信息。</td>
<td><ul class="params"><li>在函数配置页面将内存配置调大，如果当前设置已经是最大内存配置，可 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">提交工单</a> 申请提升内存限制。</li>
<li>检查代码逻辑，是否存在内存泄露。</li></ul></td>
</tr>

<tr>
<td>435<br>FunctionNotFound</td>
<td>当用户函数不存在时，会有该返回信息。</td>
<td>查看用户函数是否被删除，或者查看传入参数中的函数信息是否正确。</td>
</tr>

<tr>
<td>436<br>InvalidParameterValue</td>
<td>参数不合法。</td>
<td>-</td>
</tr>

<tr>
<td>437<br>HandlerNotFound</td>
<td>当函数包加载错误时，会有该返回信息。</td>
<td>检查函数是否未正确配置执行方法 handler，详情请参见 <a href="#handler">执行方法</a>。</td>
</tr>

<tr>
<td>438<br>FunctionStatusError</td>
<td>腾讯云账户欠费导致函数服务停止。</td>
<td>-</td>
</tr>

<tr>
<td>439<br>UserProcExitError</td>
<td>当函数执行时用户进程意外退出时，会有该返回信息。</td>
<td>用户可以根据返回错误信息中查询进程退出原因修复函数代码。</td>
</tr>

<tr>
<td>441<br>UnauthorizedOperation</td>
<td>当函数执行时，用户 CAM 鉴权不通过，会有该返回信息。</td>
<td>请求未授权。请参考 <a href="https://intl.cloud.tencent.com/document/product/598" target="_blank"> CAM文档 </a>对鉴权的说明。</td>
</tr>

<tr>
<td>442<br>QualifierNotFound</td>
<td>当函数指定版本调用时，未找到对应版本，会有该返回信息。</td>
<td>函数版本不存在，请检查函数版本后重试。</td>
</tr>

<tr>
<td>500<br>InternalError</td>
<td>内部错误。</td>
<td>-</td>
</tr>

<tr>
<td>532<br>ResourceExhausted</td>
<td>计算资源不足。</td>
<td>-</td>
</tr>

</tbody>
</table>

<style>
.params{margin:0px !important}
</style>


## 相关概念
#### 执行方法<div id="handler"></div>
执行方法表明了调用云函数时需要从哪个文件中的哪个函数开始执行。如下图所示：
![](https://main.qcloudimg.com/raw/48172f9407d4002f79ad0355e609aff2.png)
- 一段式格式为【文件名】，Golang 环境时使用。例如 `main`。
- 两段式格式为【文件名.函数名】，Python、Node.js 及 PHP 环境时使用。例如 `index.main_handler`。
	- 此执行方法**前一段指向代码包中不包含后缀的文件名，后一段指向文件中的入口函数名**。需要确保代码包中的文件名后缀与语言环境匹配，如 Python 环境为 `.py` 文件，Node.js 环境为 `.js` 文件。 更多执行方法相关说明，请参见 [执行方法详情说明](https://intl.cloud.tencent.com/document/product/583/9210)。 
- 三段式格式为【package.class::method】，JAVA 环境时使用。例如 `example.Hello::mainHandler`。
- 非固定段式格式，只针对 Custom Runtime 运行环境开放使用，根据自定义语言实现来设定执行方法。

         
