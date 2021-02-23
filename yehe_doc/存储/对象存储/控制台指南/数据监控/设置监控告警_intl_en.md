## Overview

You can leverage the alarm policy feature of Cloud Monitor to set threshold-reaching alarms for COS monitoring metrics. An alarm policy must include the policy name, policy type, trigger condition, alarm object, and alarm notification template. You can create an alarm policy for COS as instructed below.

>?Tencent Cloud’s Cloud Monitor enables users to monitor cloud resources in real time and provides alarm services. Users can set alarm policies for COS monitoring metrics to query the alarm history and receive alarm notifications.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Overview** in the left sidebar. Alternatively, you can click the name of the bucket in **Bucket List**, click the **Overview** tab, and click **Configure Alarm Policy** in the **Alarm Configuration** area.

2. Click **Create** and configure the alarm policy. The configurations are described as follows:
![](https://main.qcloudimg.com/raw/6f0634875354dc41ea5f541d2b9f8c4f.png)

<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="5"> Basic info</td>
    <td>Policy name</td>
    <td>User-defined policy name</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>User-defined remarks for the policy</td>
  </tr>
  <tr>
    <td>Monitor type</td>
    <td>Choose <b>Cloud Product Monitoring</b>.</td>
  </tr>
  <tr>
    <td>Policy type</td>
    <td>Choose <b>COS</b>.</td>
  </tr>
  <tr>
    <td>Project</td>
    <td>Setting the policy project allows you to:<br>   
         <ul>
             <li>Manage alarm policies. Alarm policies of a project can be quickly located in the alarm policy list.</li>
             <li>Manage instances. You can choose the project as needed. Instances of the project can be quickly located in <b>Alarm Object</b>. You can distribute Tencent Cloud services to the desired project according to your business types. To create a project, please see <a href="https://intl.cloud.tencent.com/document/product/378/34726"> Project Management</a>. After the project is created, you can distribute resources to projects in the console of each Tencent Cloud service. Some Tencent Cloud services cannot be distributed to a project. If you do not have project permission, please see <a href="https://intl.cloud.tencent.com/document/product/248/36744"> Cloud Access Management (CAM) </a> for authorization.   
  </tr>
  <tr>
    <td rowspan="4">Configure alarm rule</td>
    <td>Alarm object</td>
    <td>
      <ul>
			         <li>If you choose <b>Instance ID</b> in the drop-down list, select the bucket you want to add an alarm to. </li>
               <li>If you choose <b>Instance Group</b> in the drop-down list, the alarm policy is bound to the selected instance group. If there is no instance group, you can click <b>Create Instance Group<b/> on the right to create a group for the bucket first.</li>
		            <li>If you choose <b>All Objects</b> in the drop-down list, the alarm policy is bound to all buckets the current account has permission on.</li>
           </ul>
        </td>
				<tr>
    <td>Trigger condition<br>(choosing <b>Manual Configuration</b>)</td>
    <td>
      <ul>
        <li><b>Trigger condition</b>: consists of metric, comparison, threshold, statistical period, and the number of consecutive periods.<br>For example, if the metric is set to `STANDARD storage read requests`, comparison to `>`, threshold to `80` times, statistical period to `5` minutes, and the number of consecutive periods to `Last 2 periods`, <br>STANDARD storage read requests are collected every 5 minutes, and if the number of STANDARD storage read requests in a bucket is greater than 80 in 2 consecutive periods, the alarm will be triggered.
				<br><li>Alarm frequency: you can set a repeated notification policy for each alarm rule. In this way, an alarm notification will be sent repeatedly at a specified frequency when an alarm is triggered.<br>Frequency options: do not repeat, once every 5 minutes, once every 10 minutes, at an exponentially increasing interval, and other frequency options.<br><ul><li type="square">An exponentially increasing interval means that a notification is sent when an alarm is triggered the 1st time, 2nd time, 4th time, 8th time, and so on. In other words, the alarm notification will be sent less and less frequently as time goes on to reduce the disturbance caused by repeated notifications.</li>
      <li>Default logic for repeated alarm notifications: the alarm notification will be sent to you at the configured frequency within 24 hours after the alarm is triggered. After 24 hours, the alarm notification will be sent once a day by default.</li></ul></li>
      </ul></td>
  </tr>
  <tr>
  </tr>
  <tr>
    <td>Trigger condition (choosing <b>Select template</b>)</td>
    <td>Select a configured template in the drop-down list. For more information about the configurations, please see <a href="https://intl.cloud.tencent.com/document/product/248/32817">Configuring trigger condition templates</a>. If the newly created template is not displayed, click the Refresh icon on the right.</td>
  </tr>
   <tr>
        <td >Configure alarm notification</td>
        <td>Notification template</td>
        <td>You can select a preset notification template or customize one. Up to 3 notification templates can be bound to each alarm policy.</td>
    </tr>
		<tr>
      <td>Advanced configuration</td>
      <td >Auto scaling</td>
      <td>If enabled, the auto scaling policy can be triggered when the alarm condition is met.</td>
     </tr>
</table>

3. Click **Complete**.
