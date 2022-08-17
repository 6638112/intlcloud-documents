## Background
You can monitor the performance of ClickHouse clusters in the following two ways:
- Use the default monitoring page if you don't enable Grafana monitoring when purchasing a cluster.
- Use the advanced monitoring system with cluster alarm policies if you enable Grafana monitoring when purchasing a cluster.

## Grafana Monitoring Disabled 
Go to the [CDWCH console](https://console.cloud.tencent.com/cdwch), click a **Cluster ID/Name** in the **Cluster List** to enter the cluster details page, and switch to the **Cluster Monitoring** tab to view performance metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/6d8f62029b442b16dbf475a171730512.jpg)

| Metric                  | Description                                                 |
| ----------------------- | ---------------------------------------------------- |
| Network connections              | Total number of server connections                                     |
| SELECT queries            | Number of queries executed per unit of time                               |
| Total file opens       | Number of file opens                                       |
| Inserted rows              | Number of insertions executed per unit of time                               |
| Merges executed on backend | Number of threads being merged                                 |
| Total threads processing queries      | Number of threads to start query processing                               |
| CPU utilization               | CPU utilization of each node                                    |
| 1-min CPU load          | CPU load in 1 minute of each node                                |
| Disk space utilization          | Ratio of used disk space to the maximum available disk space * 100% |
| Memory utilization              | Memory utilization of each node                                   |
| Outbound network traffic rate          | Rate of data sent by the ENI                                     |
| Inbound network traffic rate          | Rate of data received by the ENI                                     |

## Granafa Monitoring Enabled
### Monitoring dashboard
ClickHouse is preconfigured with four monitoring dashboards (**ClickHouse cluster**, **Single-Node server**, **Multi-Node server**, and **Node overview**). You can also customize dashboards as needed. The following describes the metrics and formulas for each dashboard.

**Clickhouse cluster dashboard**: See [Metric Description](#jump) for details. Click **ClickHouse Monitoring** in the top-right corner to switch to other dashboards.
![](https://qcloudimg.tencent-cloud.cn/raw/261ff6f8db9452239c457cce9d6dcf7a.jpg)
**Single-node server dashboard**: Details server metrics by IP.
![](https://qcloudimg.tencent-cloud.cn/raw/a8d9339c5a62a31daa2aa18e89ca1f31.jpg)
**Multi-node server dashboard**: Horizontally compares 8 basic server metrics by IP.
![](https://qcloudimg.tencent-cloud.cn/raw/bceca0ed8c620a5cf5d2e723756c3afd.jpg)
**Node overview dashboard**: Summarizes the basic server conditions of all nodes to offer a holistic picture of the entire cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/7ca6d1d8b44a0254acd4ce06f1661126.jpg)

### Metric calculation formula
Click a dashboard name and select **Explore** in the drop-down list to learn the details of a metric.
![](https://qcloudimg.tencent-cloud.cn/raw/1ccf1fe1e7c42ba1b3a0262cc3b575f4.jpg)
In a specific calculation, `node_cppu_seconds_total` is the metric. For more metrics, see [metrics](https://clickhouse.tech/docs/en/operations/system-tables/metrics/).
![](https://main.qcloudimg.com/raw/48e230b468108fd6d639b446bd8a3081.png)


### Custom panel configuration
You can personalize a panel to fit your usage habits.
1. Click **+** on the left sidebar and select **Dashboard** in the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/4ca2892b94280df1ce1d05c421d3e7d5.jpg)
2. Click **+ Add new panel**.
![](https://main.qcloudimg.com/raw/6203ab9604542e0007cf4d1138ef96b9.png)
3. Enter a metric or click **Metrics** to view the calculated metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/e6ce321e705dd7a6806ac8b391649831.jpg)
4. You can select a display style on the right. For more information, see [About Grafana panels](https://grafana.com/docs/grafana/latest/panels/).
![](https://main.qcloudimg.com/raw/6155e7249b8e20b3d02007301eafee03.png)
5. Click **Apply** in the top-right corner and click **Save**.

[](id:jump)
### Metrics
<table>
<thead>
<tr>
<th>Metric</th>
<th>Description</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>Total Query</td>
<td>Number of CRUD statements executed per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Query</td>
<td>Number of queries executed per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Replication</td>
<td>Sending, acquisition, and checking conditions of a single replica</td>
<td>-</td>
</tr>
<tr>
<td>Insert Query</td>
<td>Number of insertions executed per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Connections</td>
<td>Number of connections of each node</td>
<td>-</td>
</tr>
<tr>
<td>Read/Write Syscalls</td>
<td>Number of read/write system calls of each node</td>
<td>-</td>
</tr>
<tr>
<td>Number of Read/Write with a File Descriptor</td>
<td>Number of handles for file reads/writes and failed reads/writes per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Bytes of Read/Write with a File Descriptor</td>
<td>Size of files read and written per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Cache Rate</td>
<td>Cache hit rate and miss rate</td>
<td>Indicates repeated queries of the business</td>
</tr>
<tr>
<td>Selected Ranges</td>
<td>Number of index hits for a query, matching the amount of query data for a particular SQL hit</td>
<td>-</td>
</tr>
<tr>
<td>Selected Marks</td>
<td>Number of index hits for a query, matching the amount of query data for a particular SQL with a finer granularity</td>
<td>-</td>
</tr>
<tr>
<td>Merge1</td>
<td>Number of threads being merged</td>
<td>The number of merges should not be set too large. A high merge rate means that the amount of data imported per batch is too small, and the data is relatively concentrated and proportional to the part file directories</td>
</tr>
<tr>
<td>Merge2</td>
<td>Number of rows being merged</td>
<td>-</td>
</tr>
<tr>
<td>Merges Time</td>
<td>Compression and consumption time (rate)</td>
<td>It is related to the amount of compressed data</td>
</tr>
<tr>
<td>Parts of ReplicatedMergeTree Merged</td>
<td>Number of replicated parts merged per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Mutations</td>
<td>Number of replicated part mutations per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Pool Tasks</td>
<td>Number of tasks performed on the backend</td>
<td>-</td>
</tr>
<tr>
<td>Open Files</td>
<td>Number of file opens per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Compressed Read Buffer</td>
<td>Size of compressed read cache used per unit of time</td>
<td>-</td>
</tr>
<tr>
<td>Memory</td>
<td>Memory usage of each node</td>
<td>-</td>
</tr>
</tbody></table>
