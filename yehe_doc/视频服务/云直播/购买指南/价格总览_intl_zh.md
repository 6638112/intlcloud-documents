>? 您可通过 [云直播价格计算器](https://buy.cloud.tencent.com/price/css/calculator) 预估您的标准直播和快直播相关费用。

云直播计费项包含基础服务费用、增值服务费用。结合腾讯云其他产品一起提供的增值功能会产生拓展服务费用。费用组成如下图：

![](https://main.qcloudimg.com/raw/a71760b6e95440f8cd3a8fa053a50708.png)


- [基础服务费用](#base)：使用直播（包括标准直播和快直播）后产生的直播消耗费用，标准直播和快直播支持流量或峰值带宽两种计费方式切换。
- [增值服务费用](#appreciation)：使用直播转码、录制、截图、鉴黄、云导播台等增值功能，此类功能默认关闭，使用才收费。
- [拓展服务费用](#extensions)：结合腾讯云其他产品一起提供的增值功能，由其他云产品根据各自的计费规则分别收取相关费用。

<span id="base"></span>

## 基础服务费用

基础服务费用根据直播服务分为标准直播服务费用和快直播服务费用。

<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>标准直播流量<br>（默认）</td>
<td>
<li/>标准直播观看产生的下行流量消耗，按日结后付费计费。
<li/>中国内地（大陆）、中国港澳台及海外加速计费标准各异。
</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818">后付费-日结</a></li>
</td>
</tr><tr>
<td>标准直播带宽峰值</td>
<td>
<li/>标准直播观看产生的下行带宽峰值，按日结后付费计费。
<li/>中国内地（大陆）、中国港澳台及海外加速计费标准各异。
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818">后付费-日结</a></td>
</tr><tr>
<td>快直播流量<br>（默认）</td>
<td>快直播观看产生的中国内地（大陆）下行流量消耗，按日结后付费计费。</td>
<td><a href="https://cloud.tencent.com/document/product/267/39136#flow">后付费-日结</a></td>
</tr><tr>
<td>快直播宽带峰值</td>
<td>快直播观看产生的中国内地（大陆）下行带宽峰值，按日结后付费计费。</td>
<td><a href="https://cloud.tencent.com/document/product/267/39136#bandwidth">后付费-日结</a></td>
</tr></table>

>! 
>- 由于快直播采用超低延迟链路，流量/带宽费用略高于标准直播。
>- 若您需要重新选择计费方式，请参见 [计费变更](https://intl.cloud.tencent.com/document/product/267/30411)。  


<span id="appreciation"></span>

## 增值服务费用

<table>
<tr><th colspan=2 width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td rowspan=3>直播转码</td>
<td>标准转码</td>
<td><ul style="margin:0">
<li/>使用直播标准转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31064">直播水印</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071">标准转码</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">直播混流</a> 等功能时，均会产生标准转码费用。
<li/>产生的费用按<b>转码时长计费</b>，以您输出的直播流画面尺寸的范围区间价格为计费单价。
</ul></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li></ul>
</td>
</tr><tr>
<td>极速高清转码</td>
<td><ul style="margin:0">
<li/>使用直播极速高清转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">极速高清转码</a> 功能时，将产生极速高清转码费用。
<li/>产生的费用按<b>转码时长计费</b>，以您输出的直播流画面尺寸的范围区间价格为计费单价。
</ul><td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li></td>
</tr><tr>
<td>音频转码</td>
<td>
<li/>使用直播音频转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">音频转码</a>、音频混流、音视频分离等功能时，均会产生音频转码费用。
<li/>产生的费用按<b>音频转码时长计费</b>。
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li></td>
</tr><tr>
  <td colspan=2>直播录制</td>
  <td>
    <li>直播录制为根据录制模板生成的录制文件并存储到云点播。</li>
    <li>录制产生的服务费用<b>按标准直播录制并发峰值路数计费</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">后付费-月结</a></td>
</tr><tr>
<td colspan=2>直播截图</td>
<td>
  <li>直播截图为根据模板定时对直播流进行截图，图片存储到 COS。</li>
  <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">后付费-月结</a></td>
</tr><tr>
  <td colspan=2>智能鉴黄</td>
  <td>截图鉴黄会产生鉴黄和截图两笔费用。
    <li>鉴黄产生的服务费用<b>按鉴黄张数计费</b>，每月前1000张免费。</li>
    <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">后付费-月结</a></td>
</tr>
</table>


<span id="extensions"></span>

## 拓展服务费用

<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>录制存储</td>
<td>直播录制文件需存储到云点播，产生的服务费用<b>按数据的实际存储时间和存储量计费</b>，需额外支付点播存储费用。</td>
<td><a href="https://cloud.tencent.com/document/product/266/14667#storage_page">云点播-按量计费</a></td>
</tr><tr>
<td>截图存储</td>
<td>直播截图和鉴黄生成的截图文件需存储到 COS，产生的服务费用<strong>按数据的实际存储时间和存储量计费</strong>，需额外支付 COS 存储费用。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-按量计费</a></td>
</tr></table>

