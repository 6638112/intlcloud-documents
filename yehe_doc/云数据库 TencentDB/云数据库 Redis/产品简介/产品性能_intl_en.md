## Specifications
### Memory edition
<table>
<thead>
<tr>
<th align="center">Feature</th>
<th colspan="2" >Standard Architecture</th>
<th align="center">Cluster Architecture</th>
</tr>
</thead>
<tbody><tr>
<td align="center">Compatible Redis version</td>
<td align="center">2.8</td>
<td align="center">4.0, 5.0</td>
<td align="center">4.0, 5.0</td>
</tr>
<tr>
<td align="center">Memory</td>
<td align="center">256 MB-60 GB</td>
<td align="center">1-60 GB</td>
<td align="center">12 GB-4 TB</td>
</tr>
<tr>
<td align="center">Number of shards</td>
<td align="center">Unsupported</td>
<td align="center">Unsupported</td>
<td align="center">3-128</td>
</tr>
<tr>
<td align="center">QPS</td>
<td align="center">80,000-100,000</td>
<td align="center">80,000-100,000</td>
<td align="center">80,000-100,000 per shard</td>
</tr>
<tr>
<td align="center">Max connections</td>
<td align="center">10,000</td>
<td align="center">10,000</td>
<td align="center">10,000 per shard</td>
</tr>
<tr>
<td align="center">Traffic limit</td>
<td align="center">10-64 MB/s</td>
<td align="center">10-64 MB/s</td>
<td align="center">72 MB/s-5 GB/s</td>
</tr>
<tr>
<td align="center">Multi-database</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Mget, Mset</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Lua</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Supported (cross-slot access not supported)</td>
</tr>
<tr>
<td align="center">Horizontal scaling</td>
<td align="center">Unsupported</td>
<td align="center">Unsupported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Replica scaling</td>
<td align="center">Unsupported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Read/Write separation</td>
<td align="center">Unsupported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">GEO</td>
<td align="center">Unsupported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Number of replicas</td>
<td align="center">0-1</td>
<td align="center">1-5</td>
<td align="center">1-5</td>
</tr>
</tbody></table>

>The 256 MB specification is a limited introductory version. It is only suitable for functionality verification in test environments but not recommended for production environments. Other specifications currently cannot be scaled down to the 256 MB specification.


### CKV edition
<table>
<thead>
<tr>
<th width=20%>Feature</th>
<th width=30%>Standard Architecture</th>
<th width=50%>Cluster Architecture</th>
</tr>
</thead>
<tbody><tr>
<td>Compatible Redis version</td>
<td>3.2</td>
<td>3.2</td>
</tr>
<tr>
<td>Memory</td>
<td>4-384 GB</td>
<td>12 GB-48 TB</td>
</tr>
<tr>
<td>Number of shards</td>
<td>-</td>
<td>3-128</td>
</tr>
<tr>
<td>QPS</td>
<td>80,000–120,000</td>
<td>Tens of millions</td>
</tr>
<tr>
<td>Max connections</td>
<td>12,000-24,000</td>
<td>12,000–24,000 per shard</td>
</tr>
<tr>
<td>Traffic limit</td>
<td>16-256 MB/s</td>
<td>72 MB/s-32 GB/s</td>
</tr>
<tr>
<td>Multi-database</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Mget, Mset</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Lua</td>
<td>Supported</td>
<td>Limited support (to use Lua in the cluster edition, you need to make sure that the keys accessed in the Lua script are in the same slot, and the `key` field must be included in the command parameters)</td>
</tr>
<tr>
<td>Horizontal scaling</td>
<td>Unsupported</td>
<td>Supported</td>
</tr>
<tr>
<td>Replica scaling</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Read/write separation</td>
<td>Unsupported</td>
<td>Unsupported</td>
</tr>
<tr>
<td>GEO</td>
<td>Supported</td>
<td>Supported</td>
</tr>
</tbody></table>

### Traffic and Connections
**Memory edition**

| Specification (GB) | Max Connections | Max Throughput (MB/s) |
|  :----------: |  :----------: |  :-------------------: |
| 0.25          | 3,000       | 10                  |
| 1          | 10,000       | 16                  |
| 2          | 10,000       | 24                  | 
| 4          | 10,000       | 24                  |
| 8          | 10,000       | 24                  |
| 12         | 10,000       | 32                  | 
| 16         | 10,000       | 32                  | 
| 20         | 10,000       | 48                  |
| 24         | 10,000       | 48                  | 
| 32         | 10,000       | 48                  | 
| 40         | 10,000       | 64                  | 
| 48         | 10,000       | 64                  | 
| 60         | 10,000       | 64                  | 

**CKV edition**

| Specification (GB) | Max Connections | Max Throughput (MB/s) | 
|  :----------: |  :----------: |  :-------------------: |
| 4          | 10,000       | 24                  |
| 8          | 10,000       | 24                  |
| 16         | 10,000       | 32                  | 
| 24         | 10,000       | 32                  | 
| 32         | 10,000       | 32                  | 
| 48         | 18,000      | 64                  | 
| 64         | 18,000      | 64                  | 
| 80         | 18,000      | 64                  |
| 96         | 18,000      | 64                  | 
| 128        | 24,000      | 128                 | 
| 160        | 24,000      | 128                 | 
| 192        | 24,000      | 128                 | 
| 256        | 24,000      | 256                 | 
| 320        | 24,000      | 256                 | 
| 384        | 24,000      | 256                 | 

Cluster edition connections = number of connections per shard * number of shards;
Cluster edition throughput = shard throughput * number of shards
>! After scaling, legacy instances capable of up to 9,000 connections will be capable of 10,000 connections.

## Performance Data
### Performance references
The time needed to execute Redis commands varies. Businesses use different database commands in their production environments; therefore, the corresponding performance values will also vary. The test results listed here are obtained with specified parameters and are for your reference only. Please conduct tests in your actual business environment for more accurate results.

- Single-node test performance
  
|  Redis Instance Specification | Connections | QPS |
|:---------:|:---------:|:--------:|
| Memory edition (standard architecture), 8 GB | 10,000 | 80,000-100,000 |
| Memory edition (cluster architecture), 8 GB (per shard) | 10,000 | 80,000-100,000 |
| CKV edition (standard architecture), 8 GB|  12,000    |   80,000-120,000  |

 
- Cluster architecture test performance
   Memory edition (cluster architecture) performance = memory edition (standard architecture) performance * number of shards
   CKV edition (cluster architecture) performance = CKV edition (standard architecture) performance * number of shards


### Test method

 - Test environment
 
| Number of CVMs in the Pressure Test Client | CVM Cores | CVM MEM | Region | Redis Instance Specification |
|:---------:|:---------:|:---------:|:---------:|:---------:|
| 3 | 2 |8 GB | Guangzhou Zone 2 | Memory edition (standard architecture), 8 GB | 
| 3 | 2 |8 GB | Guangzhou Zone 2 | CKV edition (standard architecture), 8 GB |


 - Test parameters
 ```
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1znib6aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1z5536aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-090rjlih:1234567 -t set -c 3500 -d 128 -n 25000000 -r 5000000
```
 - QPS calculation
Sum of the QPS values of 3 pressure test clients (tested by redis-benchmark).


