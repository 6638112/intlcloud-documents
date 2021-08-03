云顾问的巡检项包含五个维度： 安全、可靠、服务限制、成本、性能

#### Security

通过建议您启用腾讯云安全功能以及检查权限，提高系统和业务的安全性。

<table>
   <tr>
      <td>产品</td>
      <td>巡检项</td>
      <td>巡检说明</td>
   </tr>
   <tr>
      <td rowspan="4">DDOS 防护（ANTIDDOS)</td>
      <td>DDOS 防护（ANTIDDOS）被封堵的公网 IP 检查</td>
      <td>检查是否有公网 IP（EIP）因 DDOS 攻击被封堵</td>
   </tr>
   <tr>
      <td>DDOS 防护（ANTIDDOS）可用 IP 黑洞解封次数检查</td>
      <td>检查黑洞解封次数使用占比是否过大</td>
   </tr>
   <tr>
      <td>DDOS 防护（ANTIDDOS）CC 防护状态检查</td>
      <td>检查类型为 CVM、CLB、NAT 的实例是否开启 CC 防护</td>
   </tr>
   <tr>
      <td>DDOS 防护（ANTIDDOS）DDOS 防护状态检查</td>
      <td>检查类型为 CVM、CLB、NAT 的实例是否开启 DDOS 防护</td>
   </tr>
   <tr>
      <td  rowspan=2>COS</td>
      <td>对象存储（COS）存储桶 CORS 配置</td>
      <td>检查存储桶 CORS 配置， 若未配置 CORS Allow-Headers/Expose-Headers 头部，则告警</td>
   </tr>
   <tr>
      <td>对象存储（COS）存储桶防盗链（Referer） 配置</td>
      <td>检查 COS 存储桶 Referer 配置，若未配置或者配置了空 Referer 访问规则，则告警</td>
   </tr>
   <tr>
      <td>对象存储（COS）存储桶防盗链（Referer） 配置</td>
      <td>检查 COS 存储桶 Referer 配置，若未配置或者配置了空 Referer 访问规则，则告警</td>
   </tr>
   <tr>
      <td>对象存储（COS）存储桶公有读写</td>
      <td>检查 COS 存储桶公有读写权限，若设置了公有读写权限，则会告警</td>
   </tr>
   <tr>
      <td>COS sub-account access permission not set</td>
      <td>检查 COS 存储桶账号配置，若未设置子账号访问权限，则告警</td>
   </tr>
   <tr>
      <td>COS sub-account access permission not restricted</td>
      <td>检查 COS 存储桶子账号权限范围，若具有完全控制（COS_ACL_FULL），则会告警</td>
   </tr>
   <tr>
      <td  rowspan=2>Elasticsearch Service</td>
      <td>Elasticsearch public access not restricted</td>
      <td>检查 ES 集群的 Elasticsearch 组件公网访问策略，若未配置任何限制，则告警</td>
   </tr>
   <tr>
      <td>ES 集群的 Kibana 组件公网访问策略</td>
      <td>检查 ES 集群的 Kibana 组件公网访问策略，若未配置任何限制，则告警</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>内容分发网络（内容分发网络（CDN)）IP 访问限频</td>
      <td>检测 内容分发网络（CDN) IP 访问限频配置，若业务经常出现恶意用户盗刷，建议开启</td>
   </tr>
   <tr>
      <td>云防火墙（CFW）</td>
      <td>云防火墙（CFW）资源防护检查</td>
      <td>检查云防火墙防护策略，若资源类型为 CVM/NAT/VPN/CLB 的实例未开启，则告警</td>
   </tr>
   <tr>
      <td rowspan=3>CVM</td>
      <td>CVM public login not restricted</td>
      <td>检查 CVM 公网访问安全策略，若 CVM 配置了公网 IP，且放通了登录端口访问权限，则会告警</td>
   </tr>
   <tr>
      <td>CVM public access not restricted</td>
      <td>检查 CVM 公网访问安全策略，若 CVM 配置了公网 IP，且安全组放通了对所有 IP 和 Port 的访问权限，则会告警</td>
   </tr>
   <tr>
      <td>CVM public network ports with high risks enabled</td>
      <td>检查 CVM 公网访问安全策略，若 CVM 配置了公网 IP，且放通了高危端口访问权限，则会告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MySQL</td>
      <td>云数据库（MySQL）非 root 账号高危命令限制</td>
      <td>检查 MySQL 非 root 账号权限范围，若拥有高危命令权限，则会告警</td>
   </tr>
   <tr>
      <td>云数据库（MySQL）公网安全策略检查</td>
      <td>检查 MySQL 公网安全策略，若开放公网访问且没有配置安全组规则，则告警</td>
   </tr>
   <tr>
      <td>Root account security of TencentDB for MySQL</td>
      <td>检查 MySQL 账号配置，若只存在 root 账号，则会告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for Redis</td>
      <td>High-risk commands of TencentDB for Redis not disabled</td>
      <td>检查 Redis 实例禁用命令配置，若高危命令未禁用，则告警</td>
   </tr>
   <tr>
      <td>Default account security of TencentDB for Redis</td>
      <td>检查 Redis 账号配置，若只存在默认账号，则告警</td>
   </tr>
</table>

## Reliability

通过多方位监控，维护实例的运行稳定性。

<table>
   <tr>
      <td>产品</td>
      <td>巡检项</td>
      <td>巡检说明</td>
   </tr>
   <tr>
      <td rowspan="2">Access Management</td>
      <td>访问管理（CAM）账号是否绑定MFA设备</td>
      <td>判断账号是否绑定MFA</td>
   </tr>
   <tr>
      <td>访问管理（CAM）是否开启账号保护功能</td>
      <td>判断登录操作保护、敏感操作保护、异地登录保护等功能是否开启</td>
   </tr>
   <tr>
      <td rowspan="2">云硬盘（CBS）</td>
      <td>CBS storage capacity</td>
      <td>检查云硬盘（CBS）的存储容量使用情况，若已使用容量占总容量比率过高，则发出警告</td>
   </tr>
   <tr>
      <td>CBS storage capacity</td>
      <td>检查云硬盘（CBS）的存储容量使用情况，若已使用容量占总容量比率过高，则发出警告</td>
   </tr>
   <tr>
      <td  rowspan=2>COS</td>
      <td>COS bucket versioning</td>
      <td>检查 COS 存储桶的版本控制配置，若未启用，则告警</td>
   </tr>
   <tr>
      <td>对象存储（COS）存储桶日志管理配置</td>
      <td>检查 COS 存储桶日志管理功能，若未配置，则告警</td>
   </tr>
   <tr>
      <td rowspan=3>CVM</td>
      <td>System disk snapshot of CVM</td>
      <td>检查 CVM 系统盘快照，若未创建快照，则告警</td>
   </tr>
   <tr>
      <td>云服务器（CVM）实例磁盘空间使用率过高</td>
      <td>检查 CVM 实例磁盘使用情况，若使用率过高，则告警</td>
   </tr>
   <tr>
      <td>云服务器（CVM）实例本地盘类型检查</td>
      <td>检查 CVM 实例使用本地盘的情况，若实例为非 IO 或大数据类型，且使用了本地盘，则告警</td>
   </tr>
   <tr>
      <td>云服务器（CVM）带宽利用率过高</td>
      <td>检查 CVM 实例带宽利用率情况，若带宽利用率过高，则告警</td>
   </tr>
   <tr>
      <td>Anti-DDoS</td>
      <td>DDOS 防护（ANTIDDOS）L7 转发规则健康检查</td>
      <td>检查当前7层转发规则健康检查是否存在异常</td>
   </tr>
   <tr>
      <td>Elasticseach Service</td>
      <td>Automatic snapshot backup of ES cluster</td>
      <td>检查 Elasticsearch Service 集群自动快照备份配置，若未配置，则告警</td>
   </tr>
   <tr>
      <td>TencentDB for MongoDB instance expired</td>
      <td>云数据库（MongoDB）oplog 保存时间</td>
      <td>检查 MongoDB oplog 保存时间，若保存时间过短，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MySQL</td>
      <td>Automatic backup of TencentDB for MySQL</td>
      <td>检查 MySQL 实例自动备份配置，若未开启，则告警</td>
   </tr>
   <tr>
      <td>Cross-region disaster recovery of TencentDB for MySQL</td>
      <td>检查 MySQL 灾备实例的配置，若未配置，则告警</td>
   </tr>
   <tr>
      <td>Automatic backup of TencentDB for MySQL</td>
      <td>检查 MySQL 主从延迟情况，若延迟过高，则告警</td>
   </tr>
   <tr>
      <td>云数据库（MySQL）跨可用区部署</td>
      <td>检查 MySQL 是否跨可用区部署，如果实例没有跨可用区部署，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for Redis</td>
      <td>Automatic backup of TencentDB for Redis</td>
      <td>检查 Redis 实例自动备份配置，若未开启自动备份，则告警</td>
   </tr>
   <tr>
      <td>云数据库（Redis）跨可用区部署</td>
      <td>检查 Redis 实例是否跨可用区部署，如果实例未跨可用区部署，则告警</td>
   </tr>
   <tr>
      <td rowspan="3">消息队列（TDMQ）</td>
      <td>消息队列（TDMQ）集群健康状态检查</td>
      <td>检查 TDMQ 集群的健康状态</td>
   </tr>
   <tr>
      <td>消息队列（TDMQ）备份消费者检查</td>
      <td>检查 TDMQ 订阅是否有备份消费者</td>
   </tr>
   <tr>
      <td>消息队列（TDMQ）死信队列检查</td>
      <td>检查 TDMQ 命名空间下是否有死信队列</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MySQL</td>
      <td>云数据库（TDSQL）主从延迟</td>
      <td>检查 TDSQL 主从延迟情况，若主从延迟过高，则告警</td>
   </tr>
   <tr>
      <td>云数据库（TDSQL）主从延迟</td>
      <td>检查 TDSQL 主从延迟情况，若主从延迟过高，则告警</td>
   </tr>
   <tr>
      <td rowspan="3">容器服务（容器服务（TKE））</td>
      <td>容器服务（容器服务（TKE））集群 Pod 分配率</td>
      <td>检查 容器服务（TKE） 集群可创建最大 Pod 数量是否过低</td>
   </tr>
   <tr>
      <td>容器服务（容器服务（TKE））集群节点跨可用区</td>
      <td>检查 容器服务（TKE） 节点跨可用区情况</td>
   </tr>
   <tr>
      <td>容器服务（容器服务（TKE））节点状态</td>
      <td>检查 容器服务（TKE） 节点状态，若节点状态为 NotReady，则告警</td>
   </tr>
</table>


Service limit

通过监控可提供的服务资源的最大数量。 提醒您按照建议删除资源或请求增加配额。

<table>
   <tr>
      <td>产品</td>
      <td>巡检项</td>
      <td>巡检说明</td>
   </tr>
   <tr>
      <td>云防火墙（CFW）</td>
      <td>云防火墙（CFW）规则配额检查</td>
      <td>检查云防火墙规则列表配额，若配额不足，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MongoDB</td>
      <td>TencentDB for MongoDB instance expired</td>
      <td>检查 MongoDB 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，则告警</td>
   </tr>
   <tr>
      <td>Storage capacity of TencentDB for MongoDB</td>
      <td>检查 MongoDB 存储容量的使用情况，若容量使用率较高，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MySQL</td>
      <td>TencentDB for MySQL instance expired</td>
      <td>检查 MySQL 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，则告警</td>
   </tr>
   <tr>
      <td>Automatic backup of TencentDB for MySQL</td>
      <td>检查 MySQL 实例连接使用率情况，若连接使用率过高，则告警</td>
   </tr>
   <tr>
      <td>Disk capacity of TencentDB for MySQL</td>
      <td>检查 MySQL 实例磁盘使用率情况，若磁盘使用率过高，则告警</td>
   </tr>
   <tr>
      <td>Automatic backup of TencentDB for Redis</td>
      <td>TencentDB for Redis instance expired</td>
      <td>检查 Redis 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MySQL</td>
      <td>云数据库（TDSQL）连接使用率</td>
      <td>检查 TDSQL 连接使用情况，若使用率较高，则告警</td>
   </tr>
   <tr>
      <td>云数据库（TDSQL）数据盘使用率</td>
      <td>检查 TDSQL 数据盘使用情况，若使用率较高，则告警</td>
   </tr>
</table>


Low cost

根据运行情况，给出性价比更高的配置建议，降低用户成本花费。

<table>
   <tr>
      <td>产品</td>
      <td>巡检项</td>
      <td>巡检说明</td>
   </tr>
   <tr>
      <td>CBS</td>
      <td>云硬盘（CBS）未充分利用</td>
      <td>检查云硬盘（CBS）的挂载状态及 IO 读写情况</td>
   </tr>
   <tr>
      <td  rowspan=2>COS</td>
      <td>对象存储（COS）存储桶生命周期配置</td>
      <td>检查 COS 存储桶生命周期规则，若未配置，则告警</td>
   </tr>
   <tr>
      <td>对象存储（COS）存储桶碎片检查</td>
      <td>检查 COS 存储桶清理碎片规则，若未配置，则告警</td>
   </tr>
   <tr>
      <td>CVM</td>
      <td>云服务器（CVM）计费模式检查</td>
      <td>检查 CVM 实例是否长期（超过2个月）处于按量计费模式</td>
   </tr>
   <tr>
      <td>弹性公网 IP（EIP）</td>
      <td>弹性公网 IP（EIP）被闲置</td>
      <td>检查 EIP 绑定情况，若 EIP 未绑定云资源（CVM 实例、NAT 网关、弹性网卡、高可用虚拟 IP 等），则告警</td>
   </tr>
</table>

### Performance

根据监控实例运行中的资源使用情况和最佳实践，为您提供改善性能的建议。

<table>
   <tr>
      <td>产品</td>
      <td>巡检项</td>
      <td>巡检说明</td>
   </tr>
   <tr>
      <td rowspan="7">内容分发网络（CDN)</td>
      <td>内容分发网络（内容分发网络（CDN)）单链接下行限速配置</td>
      <td>检测内容分发网络（CDN) 单链接下行限速配置配置</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）源站特殊头部缓存配置</td>
      <td>检测内容分发网络（CDN) 源站头部缓存配置</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）带宽封顶配置</td>
      <td>检查带宽封顶配置，若未关闭，则告警</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）域名绑定证书到期</td>
      <td>检查证书有效期，若小于一个月内，则告警</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）缓存命中率</td>
      <td>检查缓存命中率，若命中率过低，则告警</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）错误状态码占比</td>
      <td>检查错误状态码占比，若占比过高，则告警</td>
   </tr>
   <tr>
      <td>内容分发网络（内容分发网络（CDN)）备用源站</td>
      <td>主源站不为 COS 的前提下，建议配置备用源站</td>
   </tr>
   <tr>
      <td>COS</td>
      <td>对象存储（COS）5XX 错误率</td>
      <td>检查 COS 状态码， 若 5XX 状态码出现次数过多、且出现频率占比过大，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for MongoDB</td>
      <td>云数据库（MongoDB）Cache 脏数据</td>
      <td>检查 MongoDB Cache 脏数据情况，若 Cache 脏数据百分比较高，则告警</td>
   </tr>
   <tr>
      <td>云数据库（MongoDB）CPU 使用率</td>
      <td>检查 MongoDB CPU 使用率，若使用率较高，则告警</td>
   </tr>
   <tr>
      <td>Automatic backup of TencentDB for MySQL</td>
      <td>云数据库（MySQL）CPU 使用率</td>
      <td>检查 MySQL 实例 CPU 使用率情况，若使用率过高，则告警</td>
   </tr>
   <tr>
      <td  rowspan=2>TencentDB for Redis</td>
      <td>云数据库（Redis）Proxy 节点出流量限流触发情况</td>
      <td>检查 Redis 实例 Proxy节点出流量限流触发次数，若限流次数过高，则告警</td>
   </tr>
   <tr>
      <td>云数据库（Redis）节点CPU使用率</td>
      <td>检查数据库（Redis）实例节点CPU使用率</td>
   </tr>
   <tr>
      <td>云数据库（TDSQL）</td>
      <td>云数据库（TDSQL）CPU 使用率</td>
      <td>检查 TDSQL CPU 使用情况，若使用率较高，则告警</td>
   </tr>
</table>
