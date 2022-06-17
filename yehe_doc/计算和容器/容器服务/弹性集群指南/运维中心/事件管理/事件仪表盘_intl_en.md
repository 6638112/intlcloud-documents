
## Overview

EKS provides out-of-the-box event dashboards and can automatically configure the event overview dashboard and aggregated exception search dashboard for the cluster with event storage enabled. With user-defined filters and built-in CLS global event search, EKS makes it convenient for you to comprehensively observe, find, analyze, and locate problems in the EKS console.


## Feature Description

Three dashboards are configured in **Event Search**, namely **Event Overview**, **Aggregated Exception Search**, and **Global Search**. Follow the steps below to enter the **Event Search** page and use the features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable **Event Storage**. For more information, see [Event Storage](https://intl.cloud.tencent.com/document/product/457/39121).
3. On the left sidebar, select **Cluster Ops** > **Event Search**.


### Event overview

On the **Event Overview** tab, you can filter events based on dimensions such as time, namespace, level, reason, resource type, and resource object, view the aggregated statistics of the core event, and display data comparison within a period. Specifically, you can view dashboards of the total number of events and distribution, node exceptions, Pod OOM errors, and important event trends as well as the top exception list.
You can customize up to ten filters as needed as shown below:
![](https://main.qcloudimg.com/raw/f370277ce76c6a2ef240a344169fc08f.png)

You can modify the custom fields of the filters as shown below:
<img src="https://main.qcloudimg.com/raw/df8ee926969df26811bf59507ba7c6ac.png" data-nonescope="true">



You can view more statistics on this page as shown below:
- The total number of events, level distribution, causes of exceptions, and object distribution are as shown below:
![](https://main.qcloudimg.com/raw/c7ca857ff9f54e5c8dd30cb5206acb3c.png)
- The aggregated information of common events is as shown below:
![](https://main.qcloudimg.com/raw/4374439d538e7385fbae59f901342212.png)
- Event trends and the top exception list are as shown below:
![](https://main.qcloudimg.com/raw/986479a0ff4770ba17a9cc9733cf74ee.png)



### Aggregated exception search
On the **Aggregated Exception Search** tab, you can set filters to view the cause and object distribution trends of exceptions over a specified period of time. You can also search for exceptions in the list below the trend diagrams to quickly locate problems as shown below:
![](https://main.qcloudimg.com/raw/c38f9871647f9c39e6f4da600f9018df.png)

### Global search
The global search dashboard with the built-in CLS search and analysis page makes it convenient for you to quickly search for all events in the TKE console as shown below:
![](https://main.qcloudimg.com/raw/8dca297b58a5ce58c55077979c84fb6e.png)

### Configuring alarm by dashboard
You can configure alarms based on the preset dashboards as instructed below, so that alarms will be triggered when the configured conditions are reached:


1. Click **<img src="https://main.qcloudimg.com/raw/77e0007d25c9724e5b2f05ab3ff8f95a.png" width="2.5%">** on the right of the target dashboard and select **Quickly Add Alarm** from the drop-down list as shown below:
![](https://main.qcloudimg.com/raw/e4615f3bf641d0e7c869a8ef8b12d775.png)
2. For more information on how to configure alarm policies, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/614/39574).


