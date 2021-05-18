## Overview

A log with full text in multi lines spans multiple lines (such as a Java program log). In this mode, the line break `\n` cannot be used to mark the end of a log. To help CLS system distinguish between the logs, a first-line regular expression is used for match. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log.

In the "full text in multi lines" mode, a default key `__CONTENT__` is also set, but the log data itself is not structured, and no log fields are extracted. The time attribute of a log is determined by the collection time.

## Prerequisites

Assume the raw data of a multi-line log is:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
CLS outputs it into:
```plaintext
__CONTENT__:10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 \nMozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0  0.310 0.310
```

## Directions

### Logging in to the console

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Logset** to go to the logset management page.

### Creating a log topic

1. Select the logset for which to create a log topic and click the logset ID/name to go to the logset information page.
2. Click **Create Log Topic**.
3. In the pop-up dialog box, enter `test-mtext` as the **Log Topic Name** and click **OK**.


### Server group management

1. After the log topic is created successfully, go to the log topic management page.
2. Select the **Collection Configuration** tab, click the format in which you need to collect logs.
3. On the **Machine Group Management** page, select the server group to which to bind the current log topic and click **Next** to proceed to collection configuration.
For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


### Collection configuration

#### Configuring log file collection path

On the **Collection Configuration** page, enter a **Collection Path** according to the log collection path format as shown below:
Log collection path format: `[directory prefix expression]/**/[filename expression]`.

After the log collection path is entered, LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen for all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | Directory structure of the log file prefix. Only wildcards `\*` and `?` are supported.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |
| /\*\*/     | Current directory and all its subdirectories                                  |
| Filename   | Log filename. Only wildcards `\*`  and `?` are supported.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |

Common configuration modes are as follows:
- [Common directory prefix]/\*\*/[common filename prefix]\*
- [Common directory prefix]/\*\*/\*[common filename suffix]
- [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
- [Common directory prefix]/\*\*/\*[Common string]\*

Below is an example:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| :--- | :------------- | :----------- | :----------------------------------------------------------- |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen for log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 2.   | /var/log/nginx | *.log        | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen for log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 3.   | /var/log/nginx | error*       | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen for log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path. |

>!
> - Only LogListener 2.3.9 or above allows adding multiple collection paths.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, please add a soft link to the source file and add it to another collection configuration.
> 

#### Configuring the "full text in multi lines" mode

1. In the **Collection Configuration** page, select **Full text in multi lines** as the **Extraction Mode**.

2. Define a regular expression according to the following rules.
You can choose **Auto-Generate** or **Enter Manually** to define a first-line regular expression, and the system will verify the regular expression based on the sample content.
 - **Auto-Generate**: enter the sample log in the text box, click **Auto-Generate**, and the system will automatically generate the first-line regular expression in the grayed-out text box as shown below:

 - **Enter Manually**: enter the sample log and first-line regular expression in the text box, click **Verify**, and the system will determine whether the expression has passed verification as shown below:

  

#### Filter rules

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be a hit rule; in other words, only logs that match the regular expression will be collected and reported.

In the "full text in multi lines" mode, `__CONTENT__` is used as the key name of a log by default. For example, below is a sample log with full text in multi lines:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
If you want to collect all logs of the server `10.20.20.10`, enter `__CONTENT__` in **Key** and `10.20.20.10.*` in **Filter Rule**.

>! The relationship logic between multiple filter rules is "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

### Index configuration

1. Click **Next** to go to the **Index Configuration** page.
2. On the **Index Configuration** page, set the following information.

 - **Index Status**: select whether to enable it.
 - **Full-Text Index**: select whether to set it to case-sensitive.
 - **Full-Text Delimiter**: they are `@&()='",;:<>[]{}/ \n\t\r` by default and can be modified as needed.
 - **Key-Value Index**: disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, you can set <img src="https://main.qcloudimg.com/raw/bd22396a4acfbf6d96def87060207a46.png" /> to <img src="https://main.qcloudimg.com/raw/d7ba8412e263386b627369741b457f2e.png" />.
 >! Index configuration must be enabled before you can perform searches.
>
3. Click **Submit** to finish collection configuration.

## Operations
### Log search
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Select the region, logset, and log topic as needed and click **Search and Analysis** to search for logs according to the set query criteria.
