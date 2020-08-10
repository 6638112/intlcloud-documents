
CFS offers two types of file systems: standard and high-performance. Below are their features, benefits, and use cases.

<table>
<tr>
    <th>File System Type</th>
    <th>Features</th>
    <th>Benefits</th>
    <th>Use Cases</th>
  </tr>
<tr>
    <td>Standard</td>
    <td nowrap="nowrap">   
    <li>Elastic scaling of storage capacity based on the number of writes, up to 160 TB</li>
    <li>Linear scaling of throughput based on file system capacity, up to 300 MB/s</li>
    <li>Up to 4K IOPS (4 KB random read/write)</li>
    </td>
    <td nowrap="nowrap"><li>Low costs<br><li>High volume</td>
    <td>The most common file sharing scenarios that require high cost efficiency, such as data backup, OA, log storage, and small file sharing</td>
</tr>
<tr>
    <td>High-performance</td>
    <td>   
    <li>Elastic scaling of storage capacity based on the number of writes, up to 2 PB</li>
    <li>Linear scaling of throughput based on file system capacity, up to 40 GB/s</li>
    <li>Up to 60K IOPS (4 KB random read/write)</li>
    </td>
    <td nowrap="nowrap"><li>High throughput<br><li>High IOPS</td>
    <td>High-through, compute-intensive workloads mainly involving large files, such as high-performance computing, media asset rendering, and machine learning</td>
 </tr>
</table>



## Performance Formula

The relationship between the throughput of a single standard or high-performance file system and the amount of write storage is as follows:

<table>
   <tr>
      <th>File System Type</th>
      <th>Performance Formula</th>
   </tr>
   <tr>
      <td>Standard</td>
      <td>Throughput (MB/s) = storage usage (GB) * 0.1 + 100</td>
   </tr>
   <tr>
      <td>High-performance</td>
      <td>Throughput (MB/s) = storage usage (GB) * 0.2 + 200</td>
   </tr>
</table>

>?The above formulas show the capabilities a file system can provide. To reach the upper performance limit, you usually need to perform multi-threaded reads/writes by using multiple computing nodes.
