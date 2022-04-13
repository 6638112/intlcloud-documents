TDSQL-C for MySQL is a new-generation cloud native relational database developed by Tencent Cloud. It combines the strengths of traditional databases, cloud computing, and cutting-edge hardware technologies to provide elastic scalable database services featuring high performance, availability, reliability, and security, as well as full MySQL compatibility. It can deliver a high throughput of over one million QPS, a massive distributed smart storage capacity at the petabyte level, and serverless scaling within seconds, helping you accelerate your digital transformation.

TDSQL-C for MySQL simplifies your IT Ops and allows you to focus more on business development with its various features such as backup, restoration, monitoring, fast scaling, and data transfer.

Continuously tested and optimized by a professional team, TDSQL-C for MySQL offers many MySQL Enterprise Edition features and can flexibly and efficiently process transactions. Its engine kernel has also been deeply optimized to deliver advanced and complete security protection capabilities, massive instance capacity, and superior performance.

This document compares the performance of TDSQL-C for MySQL and TencentDB for MySQL under the dataset characteristics of full cache, big dataset, and 1 TB single table in write, read, and read-write scenarios respectively to show TDSQL-C for MySQL's overall performance. The specific test scenarios are as described below:

<table>
<tr><th>Dataset Characteristics</th><th>Test Scenario</th><th>Read Type</th></tr>
<tr><td rowspan = "5"  width="33%">Full cache</td><td>Write</td><td>-</td></tr>
<tr><td>Read</td><td>POINT SELECT</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td></tr>
<tr><td rowspan = "5"  width="33%">Big dataset</td><td>Write</td><td>-</td></tr>
<tr><td>Read</td><td>POINT SELECT</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td></tr>
<tr><td rowspan = "5"  width="33%">1 TB single table</td><td>Write</td><td>-</td></tr>
<tr><td>Read</td><td>POINT SELECT</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td></tr>
<table>
