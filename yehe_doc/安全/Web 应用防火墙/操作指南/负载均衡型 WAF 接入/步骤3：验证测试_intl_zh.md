本文档将指导您如何验证负载均衡型 WAF 是否生效。

## 操作步骤

1. WAF 通过域名和 CLB 对应监听器进行绑定，对经过 CLB 监听器的域名流量进行防护。验证负载均衡型 WAF 是否生效，请先确保本地电脑可以正常访问在负载均衡不同实例下添加的域名。
>?验证添加在负载均衡中域名型访问是否正常，IPv4 域名请求，请参见负载均衡快速入门的 [验证负载均衡服务](https://intl.cloud.tencent.com/document/product/214/8975)，IPv6 域名请求，请参见 IPv6 负载均衡快速入门的 [步骤4：测试 IPv6 负载均衡](https://intl.cloud.tencent.com/document/product/214/34560)。
2. 在浏览器中输入网址`http://wow.qcloudwaf.com/?test=alert(123)`并访问，浏览器返回阻断页面，说明 Web 应用防火墙防护功能正常。

>!`wow.qcloudwaf.com` 为本案例中域名，此处需要将域名替换为实际添加的域名。

![](https://qcloudimg.tencent-cloud.cn/raw/e45acf63d1c5bd6497b8b8b59e94bd97.png)



