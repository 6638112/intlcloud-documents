## Overview
CLS allows you to export the collected log data, so you can download the data to view it locally.
The log download feature is as described below:
- Up to 10 billion logs can be exported.
- Search conditions and search time range can be specified.
- JSON and CSV export formats are supported.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to enter the search and analysis management page.
3. Click the drop-down lists of **Logset** and **Log Topic** to select the content to be searched.
4. Click **Log Time** and select a log time for search.
You can select **Recent Time** or **Relative Time** or customize the time range.
5. Click **Search and Analysis**.
6. After the log data is returned, click <img src="https://main.qcloudimg.com/raw/53b7030f85123fe5658e7cce23b730c8.png"></img> to download logs.
>? If no log data is returned, you cannot download logs.
>
7. In the pop-up window, confirm the time range of the logs to be downloaded and the search statement and download log data according to the following settings:
<ul>
	<li>Data format: "CSV format" or "JSON format" can be selected as needed.</li>
	<li>Log sorting: logs can be sorted in "ascending" or "descending" (default) order by time.</li>
	<li>Log quantity: "All logs" are exported by default. You can also select a "custom log quantity".</li>
</ul>
8. Click **Export** to switch to the **Export Record** page.
9. After the **Filename/Task ID** status changes to **File generated**, click **Download** to export the logs.
>! 
> - The exported log file is retained for only 3 days.
> - A single log topic can be exported for up to 5 times.
> 
