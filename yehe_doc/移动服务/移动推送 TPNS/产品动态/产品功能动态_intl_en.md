## November 2020


<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=44%>Description</th>
<th width=16%>Release Date</th>
<th width=20%>Document</th>
</tr>
</thead>
<tbody><tr>
<td>Emojis can be quickly inserted into push message body</td>
<td>When you create a push in the console, you can quickly insert emojis in the message input box on the right, which effectively increases the click rate</td>
<td>November 20, 2020</td>
<td>-</td>
</tr>
<tr>
<td>IP allowlist is available</td>
<td>After you configure an IP allowlist in the console, you can control the permissions of RESTful API requests, so that only IPs in the allowlist can request RESTful APIs, which helps improve the push security</td>
<td>November 20, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Test preview is available</td>
<td>You can save the tokens of commonly used test devices and directly select such devices to preview messages before officially pushing them, which enables you to quickly verify the push configuration</td>
<td>November 20, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Account package filename can be viewed in account push details</td>
<td>The account package filename can be displayed in account push details when the push is performed, so you can locate push targets quickly</td>
<td>November 20, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Huawei v2 protocol is upgraded</td>
<td>Huawei officially announced that <b>the v2 protocol will be disused starting September 30, 2021</b>. TPNS has upgraded the Huawei push protocol to v5, which does not support carrying custom parameters through the **extra parameter(s)` field. If you have integrated the Huawei vendor channel, we recommend you use <a href="https://intl.cloud.tencent.com/document/product/1024/32624">Intent</a> to carry custom parameters; otherwise, custom parameters cannot be delivered through the Huawei channel</td>
<td>November 9, 2020</td>
<td>-</td>
</tr>
<tr>
<td>A new personalized push feature is added</td>
<td>After binding user attributes such as nickname with tokens, you can push personalized messages with user attributes to different users easily, which can increase the average click rate by 40%</td>
<td>November 9, 2020</td>
<td><a href="https://cloud.tencent.com/document/product/548/49303">Personalized Notification</a></td>
</tr>
<tr>
<td>Account package files in <code>.txt</code> or <code>.csv</code> format can be uploaded directly</td>
<td>If an account package file in <code>.txt</code> or <code>.csv</code> format is below 100 MB in size, it can be uploaded directly without being compressed</td>
<td>November 9, 2020</td>
<td>-</td>
</tr>
<tr>
<td>iOS push supports channel policy</td>
<td>One device can receive up to 3 silent messages per hour through the APNs Channel. Both notification bar messages and silent messages on iOS support complementary delivery through the TPNS and APNs channels, and the delivery policy can be customized</td>
<td>November 2, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36151">Channel Policy</a></td>
</tr>
</tbody></table>

## October 2020
                                            

<table>
<thead>
<tr>
<th  width=20%>Update</th>
<th  width=44%>Description</th>
<th  width=16%>Release Date</th>
<th  width=20%>Document</th>
</tr>
</thead>
<tbody><tr>
<td>Statistics in the console are optimized</td>
<td>Push statistics and device statistics are separated</td>
<td>October 22, 2020</td>
<td><a href="https://console.cloud.tencent.com/tpns/overview">Statistics</a> module in the console</td>
</tr>
<tr>
<td>Quick integration with iOS is upgraded</td>
<td>You can use the quick integration tool to integrate the SDK for iOS to get complete push capabilities in 3 minutes</td>
<td>October 22, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35770">Quick Integration with iOS</a></td>
</tr>
<tr>
<td>Notifications will not be delivered to opt-out iOS devices</td>
<td>If notification bar is disabled on an iOS device, this device will not be included in the <b>Attempted</b> metric when a push message is delivered</td>
<td>October 22, 2020</td>
<td>-</td>
</tr>
</tbody></table>


## September 2020

<table>
<thead>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
</thead>
<tbody>
<tr>
<td>Troubleshooting tools support querying tokens by account</td>
<td>You can search for device tokens by account to locate issues more quickly and conveniently</td>
<td>September 28, 2020</td>
<td><a href="https://cloud.tencent.com/document/product/548/48774">Troubleshooting Tools</a></td>
</tr>
<tr>
<td>New, active, and inactive are added as user tags</td>
<td>New, active, and inactive are added as user tags, allowing you to reattract and reactivate inactive users in a more targeted manner and improve the user activity with ease</td>
<td>September 24, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35392">Tagging Feature</a></td>
</tr>

</tbody></table>



## August 2020

<table>
<thead>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
</thead>
<tbody>
<tr>
<td>The feature of <B>collapse by group</B> is added</td>
<td>The feature of <B>collapse by group</B> is added, which can determine whether to collapse a message in the notification center, and the collapse policy can be customized</td>
<td>August 11, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/37807">Message Collapse</a></td>
</tr>
<tr>
<td>The channel policy for Android is optimized</td>
<td>The custom channel policy for Android is optimized, so you can choose whether to deliver a push message preferably through the TPNS channel when a device is online</td>
<td>August 11, 2020</td>
<td>-</td>
</tr>

<tr>
<td>New data metrics are added on the data overview page</td>
<td>Opt-in devices and uninstalled/unavailable devices can be viewed by day on the data overview page in the console</td>
<td>August 11, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36384">Data Overview</td>
</tr>
</tbody></table>



## July 2020




<table>
<thead>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
</thead>
<tbody>
<tr>
<td>The <B>device statistics</B> page is added</td>
<td>The <B>device statistics</B> page is added in the console to help you stay on top of the distribution of all registered devices of the application in all dimensions and make informed operational decisions.</td>
<td>July 30, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Rich media notification is upgraded</td>
<td>The rich media notification feature is upgraded to support images in notifications for an improved click rate (for the Huawei and Mi channels).</td>
<td>July 30, 2020</td>
<td><a href="https://cloud.tencent.com/document/product/548/46964 ">Rich Media Notification</a></td>
</tr>

<tr>
<td>The pay-as-you-go (postpaid) billing mode is added</td>
<td>The daily pay-as-you-go billing mode is added, which is suitable for applications whose number of daily connected devices fluctuates greatly.</td>
<td>July 1, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36877">Pay-as-You-Go</a></td>
</tr>
</tbody></table>

## June 2020

<table>
<thead>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
</thead>
<tbody><tr>
<td>Bulletin board is added</td>
<td>A bulletin board module is added on the **Product Management** page in the console to display notifications for release notes and services changes</td>
<td>June 10, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Reminder for lengthy notification text is available</td>
<td>When you enter the notification title/content in the console, if the text cannot be fully displayed on some device models, the console will display the corresponding reminder, which does not affect the normal delivery of the push</td>
<td>June 10, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35286">Text Length Limit Description</a></td>
</tr>
<tr>
<td>The toolbox feature is updated</td>
<td>In the toolbox, you can query some basic attributes of a device by token</td>
<td>June 10, 2020</td>
<td>-</td>
</tr>
</tbody></table>

## May 2020

<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
<tr>
        <td>Push funnel data at the application level is available</td>
        <td>Data for daily and real-time trends in message delivery, arrival (PV/UV), click, and dismissal at the application level is provided and can be viewed by channel</td>
        <td>May 25, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/36384">Data Overview</a></td>
    </tr> 
    <tr>
        <td>Task-level channel selection is supported</td>
        <td>A push channel can now be specified for a single push to save the vendor channel quota</td>
        <td>May 7, 2020</td>
        <td>-</td>
    </tr>
</table>

## April 2020

<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
    <tr>
        <td>Quota reminder is available for the Mi channel</td>
        <td>After the quota of the Mi channel is used up, pushes will be automatically delivered through the TPNS channel, and reminders will be displayed in the console</td>
        <td>April 23, 2020</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Push records can be searched for in the console</td>
        <td>Pushes can now be searched for by `pushid`</td>
        <td>April 23, 2020</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Push progress is displayed</td>
				<td>Push progress is now displayed on the push details page in the <a href="https://console.cloud.tencent.com/tpns">console</a> for you to view the delivery status</td>
        <td>April 23, 2020</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Push time is displayed</td>
        <td>Push time analysis is added on the push details page for you to view push arrivals and clicks in real time</td>
        <td>April 23, 2020</td>
        <td>-</td>
    </tr>
    <tr>
        <td>The toolbox is updated</td>
        <td>"Notification bar status" is added in the toolbox, enabling you to query whether the notification bar is enabled on a device based on the token</td>
        <td>April 23, 2020</td>
        <td>-</td>
    </tr>
    <tr>
        <td>The tag combination logic is optimized</td>
        <td>"AND", "OR", and "NOT" operations are supported for tags for more precise user grouping</td>
        <td>April 9, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35392#.E6.8E.A7.E5.88.B6.E5.8F.B0.E4.BD.BF.E7.94.A8">Tagging Feature</a></td>
    </tr>
    <tr>
        <td>More metrics are available in data overview</td>
        <td>More metrics are added on the data overview page for you to view push data in more dimensions</td>
        <td>April 9, 2020</td>
        <td>-</td>
    </tr>
</table>

## March 2020

<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
    <tr>
        <td>Multi-package name push is fully supported for Android</td>
        <td>Multi-package name push is now supported for the TPNS channel and major vendor channels</td>
        <td>March 12, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35393">Multi-Package Name Push Feature</a></td>
    </tr>
</table>

## February 2020


<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
    <tr>
        <td>Interactions in the console are upgraded</td>
        <td>The functionality structure in the console is optimized</td>
        <td>February 24, 2020</td>
        <td>-</td>
    </tr>
      <tr>
        <td>The SDK can be quickly integrated</td>
        <td>Quick integration based on configuration file is supported for Android;<br>Codeless integration can be implemented for iOS based on local tools</td>
        <td>February 24, 2020</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/1024/35769">Quick Integration with Android</a><li><a href="https://intl.cloud.tencent.com/document/product/1024/35770">Quick Integration with iOS</a></li></td>
    </tr>
      <tr>
        <td>Resource-level permissions are supported</td>
        <td>You can now grant operation permissions of a specified application to a specified sub-account</td>
        <td>February 24, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35288">Authorizable TPNS Resource Types</a></td>
    </tr>
</table>


## January 2020

<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
    <tr>
        <td>Quota exceeding policy is supported for vendor channels</td>
        <td>After a vendor channel quota is used up, messages will be automatically delivered through the TPNS channel to ensure message arrival as mush as possible</td>
        <td>February 24, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35829">Vendor Channel Limit Description</a></td>
    </tr>
</table>

## December 2019

<table>
    <tr>
        <th width=20%>Update</th>
        <th width=44%>Description</th>
        <th width=16%>Release Date</th>
        <th width=20%>Document</th>
    </tr>
    <tr>
        <td>Push details are optimized</td>
        <td>Push details can now be displayed by channel, and push effect can now be analyzed at the channel level</td>
        <td>December 25, 2019</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/32606">Querying Push Records</a></td>
    </tr>
    <tr>
        <td>A trial mechanism is added</td>
        <td>The TPNS service can be used free of charge for 30 days for applications with less than 1,000 daily connected devices</td>
        <td>December 25, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>The toolbox is launched</td>
        <td>Troubleshooting tools are launched for querying device information by token, binding accounts and tags, and quickly identifying push issues in a self-service manner</td>
        <td>December 19, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Aggregate statistics are available</td>
        <td>Push funnel data of multiple pushes can be aggregated through the `groupld` field</td>
        <td>December 19, 2019</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/33775">Querying Aggregated Statistics for Multiple Tasks</a></td>
    </tr>
</table>
