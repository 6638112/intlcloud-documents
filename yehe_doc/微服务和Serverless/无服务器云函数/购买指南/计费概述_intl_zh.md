
## 免费额度

自2021年11月01日起，所有开通使用云函数 SCF 服务的用户，每月可享受一定量的免费调用次数、免费资源使用量和外网出流量。免费额度如下表所示：

<table>
  <tr>
    <th class="align-left">发放时间</th>
    <th class="align-left">计费项</th>
    <th class="align-left">免费额度</th>
  </tr>
  <tr>
    <td rowspan="3">前三个月（包含开通当月）每月</td>
    <td>调用次数</td>
    <td>200万次（事件函数和 Web 函数各100万次）</td>
  </tr>
  <tr>
    <td>资源使用量</td>
    <td>40万GBs</td>
  </tr>
  <tr>
    <td>外网出流量</td>
    <td>1GB</td>
  </tr>
  <tr>
    <td rowspan="3">开通三个月后每月</td>
    <td>调用次数</td>
    <td>10万次（事件函数和 Web 函数各5万次）</td>
  </tr>
  <tr>
    <td>资源使用量</td>
    <td>2万GBs</td>
  </tr>
  <tr>
    <td>外网出流量</td>
    <td>0.5 GB</td>
  </tr>
</table>


详情请参阅 [免费额度说明](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/12282)。

## 计费方式及计费项
云函数计费方式主要为按量计费（后付费）一种方式。

云函数的费用由四部分组成，每部分根据自身统计结果和计算方式进行费用计算，结果以**美元**为单位，并保留小数点后两位：

- **资源使用费用**：由函数配置内存，乘以函数运行时长得出资源使用量，单位为 GBs。
- **调用次数费用**：函数的每次触发执行均记为一次调用，单位为次。
- **外网出流量费用**：在函数代码中访问外网时产生的出流量记录为外网出流量，单位为 GB。
- **预置并发闲置费用**：由已启动的预置实例数，减去实际运行的并发数得到闲置实例数，闲置实例数乘以配置内存，再乘以闲置时长得出闲置资源量，单位为 GBs。
<<<<<<< HEAD

Web 函数与事件型函数计费方式相同，详情请参阅 [计费方式说明](https://cloud.tencent.com/document/product/583/61678)。
=======
>>>>>>> ddc813913d543596bac38096f9829a3a4e8bf914

## 产品定价

针对组成云函数费用的四部分，定价如下：

- 资源使用费用：0.0000167美元/GBs
- 调用次数费用：0.002美元/万次
- 外网出流量费用：各地域均有不同定价，中国大陆为0.12美元/GB
- 预置并发闲置费用：0.00000847美元/GBs

Web 函数与事件型函数计费价格相同，详情请参阅 [产品定价说明](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/12281)。

## 支持地域
下表为云函数目前所支持的地域信息：
<table>
<tr>
<th width="50%">地域</th><th width="50%">取值</th>
</tr>
<tr>
<td>华南地区（广州）</td><td>ap-guangzhou</td>
</tr>
<tr>
<td>华东地区（上海）</td><td>ap-shanghai</td>
</tr>
<tr>
<td>华北地区（北京）</td><td>ap-beijing</td>
</tr>
<tr>
<td>西南地区（成都）</td><td>ap-chengdu</td>
</tr>
<tr>
<td>港澳台地区（中国香港）</td><td>ap-hongkong</td>
</tr>
<tr>
<td>亚太南部（孟买）</td><td>ap-mumbai</td>
</tr>
<tr>
<td>亚太东南（新加坡）</td><td>ap-singapore</td>
</tr>
<tr>
<td>亚太东北（首尔）</td><td>ap-seoul</td>
</tr>
<tr>
<td>北美地区（多伦多）</td><td>na-toronto</td>
</tr>
<tr>
<td>美国西部（硅谷）</td><td>na-siliconvalley</td>
</tr>
<tr>
<td>欧洲地区（法兰克福）</td><td>eu-frankfurt</td>
</tr>
</table>



## 计费详情

具体的计费详情，请参考以下文档：

<table>
<thead>
<tr>
<th width="50%">文档名称</th>
<th width="50%">文档链接</th>
</tr>
</thead>
<tbody><tr>
<td>免费额度</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12282" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>产品定价</td>
<td><a href="https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/12281" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>欠费说明</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12283" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>计费示例</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12285" target="_blank">查看文档</a></td>
</tr>
</tbody></table>
