## 2021年09月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tbody>
<tr>
<td>支持 Percona/MariaDB/MySQL 之间的异构迁移</td>
<td>支持 Percona/MariaDB/MySQL 之间的异构迁移。</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42644" target="_blank">MariaDB 或 Percona 到 MySQL 的迁移</a></td></tr><tr>
<tr>
<td>数据订阅支持 TDSQL MySQL</td>
<td>DTS 支持对 TDSQL MySQL 数据库的订阅。</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42663" target="_blank">数据订阅支持的数据库</a></td></tr>
</tbody></table>


## 2021年08月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tbody>
<tr>
<td>支持自定义路由策略</td>
<td>MySQL 订阅支持自定义数据字段路由到 Kafka 分区。 </td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42664" target="_blank">创建数据订阅任务</a></td></tr><tr>
<td>支持 TDSQL-C 数据同步</td>
<td>支持 TDSQL-C 数据同步至 TDSQL-C。 </td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42621" target="_blank">TDSQL-C 数据同步至 TDSQL-C</a></td></tr>
</tbody></table>


## 2021年07月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tbody>
<td>支持默认告警策略</td>
<td>支持对数据迁移、数据同步、数据订阅中的重要事件监控进行默认配置，事件触发后及时通知用户。 </td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42611" target="_blank">支持的事件和指标</a></td></tr>
<tr>
<td>支持数据迁移重试</td>
<td>支持在数据迁移任务中，由于部分异常导致任务中断，处理异常后再次启动任务。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42634" target="_blank">重试任务</a></td></tr>
<tr>
<td>支持 MySQL 数据同步至 TDSQL PostgreSQL版</td>
<td>支持 MySQL 向 TDSQL PostgreSQL版的数据同步功能。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42622" target="_blank">云数据库 MySQL 数据同步至 TDSQL PostgreSQL版 及TDSQL-A PostgreSQL版</a></td></tr>
<tr>
<td>支持库表映射</td>
<td>支持对迁移到目标库中的库表进行重命名。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42629" target="_blank">库表映射</a></td></tr>
<tr>
<td>支持查看迁移进度详情</td>
<td>支持查看迁移的详细进度，迁移进度页签显示源库表，目标库表，预估行数，已完成行数，迁移状态等信息。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42637" target="_blank">查看任务</a></td></tr>
<tr>
<td>修改视图导出功能</td>
<td><li>修改前：在导出视图时，只允许迁移和目标 user@host 相同的 definer。<li>修改后：在导出视图时，DTS 会检查源库中 `DEFINER` 对应的 user1（ [DEFINER = user1]）和迁移目标的 user2 是否一致，如果不一致，则会修改 user1 在目标库中的 `SQL SECURITY` 属性，由 `DEFINER` 转换为 `INVOKER`（ [INVOKER = user1]），同时设置目标库中 `DEFINER` 为迁移目标的 user2（[DEFINER = 迁移目标user2]）。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42561" target="_blank">视图检查</a></td></tr>
</tbody></table>


## 2021年05月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tbody>
<tr>
<td>支持数据同步指标监控</td>
<td>支持对数据同步任务中的指标进行监控。</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42579" target="_blank">支持的事件和指标</a></td></tr>
<tr>
<td>支持 MySQL 数据同步</td>
<td>腾讯云数据同步服务支持 MySQL 数据库之间的数据实时同步，可应用于云上云下多活、异地多活、数据异地多活、跨境数据同步，及实时数据仓库等多种业务场景，助您构建安全、可扩展、高可用的数据架构。</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42624" target="_blank">MySQL 数据同步至 MySQL</a></td></tr>
</tbody></table>



## 2021年04月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tbody>
<tr>
<td>支持跨账号迁移</td>
<td>数据迁移（NewDTS）支持跨账号的用户实例迁移。</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42646" target="_blank">云数据库跨账号实例间迁移</a></td></tr>
<tr>
<td>数据迁移支持 MySQL 8.0</td>
<td>数据迁移（NewDTS）支持 MySQL 8.0，支持从低版本迁移到8.0。</td>
<td>2021-04</td><td>-</td></tr>
</tbody></table>

