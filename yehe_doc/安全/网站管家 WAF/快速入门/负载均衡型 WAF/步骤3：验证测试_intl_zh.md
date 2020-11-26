1. WAF 通过域名和 CLB 对应监听器进行绑定，对经过 CLB 监听器的域名流量进行防护。验证负载均衡型 WAF 是否生效，请先确保本地电脑可以正常访问在负载均衡不同实例下添加的域名。
>?验证添加在负载均衡中域名型访问是否正常，IPv4 域名请求，请参见负载均衡快速入门的 [验证负载均衡服务](https://intl.cloud.tencent.com/document/product/214/8975)，IPv6 域名请求，请参见 IPv6 负载均衡快速入门的 [步骤4：测试 IPv6 负载均衡](https://intl.cloud.tencent.com/document/product/214/34560)。
2. 在浏览器中输入网址`http://wow.qcloudwaf.com/?test=alert(123)`并访问。
>!`wow.qcloudwaf.com` 为本案例中域名，此处需要将域名替换为实际添加的域名。
3. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/attack)，在左侧导航栏中，选择【Web 应用防火墙】>【攻击详情】，进入攻击日志查询页面，进行日志查询。
4. 选择添加防护的域名，单击【查询】，若看到攻击类型为 “XSS 攻击”，说明 WAF 配置已经生效。
