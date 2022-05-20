
## April 2022

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.3.3.3 release</td>
	<td>
		<li>Supported the Huawei push channel for a device with an EMUI system.</li>
		<li>Fixed the issue where the persistent connection retry interval was inaccurate.</li>
		</td>
        <td>April 25, 2022</td><td>
		<a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a>
</td>
    </tr>
<tr>
</table>

## February 2022

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.3.2.0 release</td>
	<td>
		<li>Upgraded the encapsulated SDK versions for Mi, Meizu, OPPO, and vivo push.</li>
		<li>Added an API to allow users to get the custom parameter `customContent` delivered with pushed messages on the push target page.</li>
		<li>Fixed other known issues.</li>
		</td>
        <td>February 23, 2022</td><td>
		<li><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></li>
		<li>For how to get `custom_content` delivered with pushed messages, see <a href="https://intl.cloud.tencent.com/document/product/1024/38354">Notification Tap-to-Redirect > Getting parameters on the client</a>.</li>
		<li><a href="https://intl.cloud.tencent.com/document/product/1024/40595">Android SDK Upgrade Guide</a></li>
</td>
    </tr>
<tr>
</table>

## January 2022

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.3.1.1 release</td>
	<td>
		<li>Added a new method for adapting to Honor device badges.</li>
		<li>Added the feature to regularly update notification status.</li>
		<li>Updated vendor channel policies.</li>
		<li>Optimized the registration and account binding processes.</li>
		<li>Removed some broadcast events that may cause applications to automatically start.</li>
		<li>Fixed the issue where the Android Service component automatically started.</li>
		</td>
        <td>January 18, 2022</td><td>
<a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a>
</td>
    </tr>
<tr>
</table>

## September 2021

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.2.7.1 release</td>
	<td>Fixed the issue of occasional cross-process storage inconsistency.</td>
        <td>September 1, 2021</td><td><li>When using the new in-app messaging feature, you need to pay attention to the compatibility between WebView and higher Android versions. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1024/30715">API Documentation</a></li>
<li><a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/1024/40595">Android SDK Upgrade Guide</a></li></td>
    </tr>
<tr>
</table>

## August 2021

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.2.7.0 release</td><td>
		<li> Added support for in-app message display.
		<li> Optimized the TPNS registration process
		<li> Fixed the issue when a user can obtain the device model before agreeing to the Privacy Agreement.</td>
        <td>August 27, 2021</td><td><li>When using the new in-app messaging feature, pay attention to the compatibility between WebView and higher Android versions. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1024/30715">API Documentation</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/1024/40595">Android SDK Upgrade Guide</a></li></td>
    </tr>
<tr>
</table>

## July 2021

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK 1.2.6.0 release</td><td><li> Added the feature of limiting API call frequency.
<li>  Supported configuring notification channels for FCM frontend notifications and TPNS local notifications.
<li>  Optimized persistent connection retry policies.
<li>  Optimized the logic for reporting the number of daily active users and SDK startup events.
<li>  Placed SDK logs in a hidden directory.
<li>  Disabled the session keep-alive feature by default. If you need to enable it, see the Android FAQs documentation.
		<li>  Fixed IPv6 request failures.</td>
        <td>July 6, 2021</td><td><li>
<a href="https://console.cloud.tencent.com/tpns/sdkdownload">SDK Download</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/1024/32624">Android FAQs</a></li></td>
    </tr>
<tr>
</table>

## May 2021

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.2.5.0 release</td><td><li>Added the API for tag query.
<li>Added the API for binding phone numbers to send ordinary and intelligent SMS messages.
<li>Supported SSL encrypted communication over persistent connection.
<li>Upgraded the API for binding accounts by adding multiple preset account types.
<li>Supported clearing notifications pushed through the Mi channel (devices of MIUI 11 or earlier) via the API for clearing all notifications.
<li>Supported badge display on HONOR mobile phones.</td>
        <td>May 26, 2021</td><td><li>Because JCenter has been deprecated, you may encounter issues when pulling SDK dependencies. See <a href="https://intl.cloud.tencent.com/document/product/1024/40595">Android SDK Upgrade Guide</a> to configure the dependency repository mirror source.</li>
<li> When using the new API for tag query, you need to add the implementation method <code>onQueryTagsResult</code> in the implementation class that inherits <code>XGPushBaseReceiver</code>. </li></td>
    </tr>
<tr>
</table>

## February 2021

<table>
	<tr>
		<th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
	</tr>
	<tr>
        <td>SDK v1.2.3.1 release</td><td>Fixed a logic error of the Huawei disable component.</td>
        <td>February 4, 2021</td><td>-</td>
    </tr>
<tr>
</table>

## January 2021
   <table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <td>SDK v1.2.3.0 release</td>
<td><li>Optimized the network communication protocol to support secondary message encryption.
<li>Simplified APIs for client account, tag, and attribute settings.
<li>Added the `traceId` and `templateId` fields to notification callback.
<li>Supported the badge logic for new Honor phones.
<li>Fixed the ANR issue that occasionally occurred during network connection checks.</td>
        <td>January 27, 2021</td>
        <td>-</td>
    </tr>
<tr>
        <td>SDK v1.2.2.4 release</td>
<td><li>Fixed the special character handling issue in Intent strings of FCM notifications.<li>Fixed other known issues.</td>
        <td>January 18, 2021</td>
        <td>-</a></td>
    </tr>
</table>



## November 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.2.0 release</td>
       <td><li> Unified the naming convention for account and tag operation APIs.<li> Optimized SDK error code reporting.<li> Upgraded the FCM channel protocol to enable the FCM system to take over the display of notifications sent through the FCM channel.<li> Added the support for badge coloring for messages sent through the TPNS channel.<li> Added the support for Gzip compression during network communication.<li>Fixed the exception of service unbinding that might occur in multi-thread environments.</td>
        <td>November 26, 2020</td>
        <td>-</td>
    </tr>
        <tr>
        <td>SDK v1.2.1.3 release</td>
       <td><li>Optimized the internal logic.<li>Officially added the support for Huawei Push SDK v5 staring this version. Update the integration configuration as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/37176">Huawei Channel v5 Integration</a>.</td>
        <td>November 11, 2020</td>
        <td>-</td>
    </tr>
</table>


## October 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <tr>
        <td>SDK v1.2.1.1 release</td>
				<td><li>Added <b>user attribute</b> APIs for personalized push.</li> <li>Added the <b>in-app message</b> feature and several in-app message templates.</li><li>Optimized and updated the SO files.</li><li>Optimized the SDK internally.</li></td>
        <td>October 12, 2020</td>
        <td>-</td>
    </tr>
</table>




## July 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
        <tr>
        <td>SDK v1.2.0.3 release</td>
       <td>Fixed known issues. </td>
        <td>July 30, 2020</td>
        <td>-</a></td>
    </tr>
<tr>
        <td>SDK v1.2.0.2 release</td>
       <td>Optimized the internal logic. </td>
        <td>2020-07-01</td>
        <td>-</td>
    </tr>
</table>

## June 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
<tr>
        <td>SDK v1.2.0.1 release</td>
       <td><li> Supported collecting statistics on vendor channel notification click events. </li> <li> Added more custom notification styles.</li> <li> Upgraded the SDK for OPPO PUSH to v2.1.0.</li> </td>
        <td>June 23, 2020</td>
        <td>This version involves package name changes. Modify relevant configurations as instructed in <a href="https://intl.cloud.tencent.com/document/product/1024/30713">SDK Integration</a>:
<li>Automatic integration: pay attention to the obfuscation configuration.</li>
<li>Manual integration: Pay attention to the SO files, manifest file, and obfuscation configuration.</li></td>
    </tr>
    <tr>
        <td>SDK v1.1.6.3 release</td>
        <td>Optimized third-party vendor channel integration.</td>
        <td>June 4, 2020</td>
        <td><a href="https://console.cloud.tencent.com/tpns/sdkdownload">-</a></td>
    </tr>
</table>

## April 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.6.1 release</td>
        <td>Fixed the vulnerability with HTTPS certificate verification.</td>
        <td>April 28, 2020</td>
        <td>-</a></td>
    </tr>
    <tr>
        <td>SDK v1.1.6.0 release</td>
        <td><li>Optimized the encryption protocol. </li> <li>Optimized network connection.</li> <li>Supported badge configuration for the Huawei channel.</li> <li>Upgraded the SDK for Mi Push to v3.7.5 and SDK for Meizu Push to v3.9.0.</li><li>Supported Realme and Black Shark channels.</li><li>Removed the call of Beacon to get QIMEI information.</li></td>
        <td>April 21, 2020</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35828">Badge Adaptation Guide</a></td>
    </tr>
    <tr>
        <td>SDK v1.1.5.5 release</td>
        <td>Fixed the issue where DCL violation occurred when an application was released in Google Play.</li></td>
        <td>April 2, 2020</td>
        <td>-</td>
    </tr>
</table>

## March 2020
<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.4 release</td>
        <td><li>Optimized network connection.</li> <li>Added account types. </li> <li> Fixed issues with security alarming. </li> <li> Added the compatibility with XG Platform version upgrade. </li><li> Added the feature of getting QIMEI information.</li><li>Added the feature of disabling session keep-alive.</li></td>
        <td>March 6, 2020</td>
        <td>-</td>
    </tr>
</table>

## January 2020

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.3 release</td>
        <td><li> Optimized the network.</li> <li> Optimized security alarming.</li></td>
        <td>January 14, 2020</td>
        <td>-</td>
    </tr>
</table>

## December 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.5.2 release</td>
        <td>Optimized error monitoring.</td>
        <td>December 19, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.5.1 release</td>
        <td>Optimized crash monitoring.</td>
        <td>December 12, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.5.0 release</td>
        <td><li> Optimized the TPNS SDK support for Huawei push.</li> <li> Upgraded the OPPO PUSH SDK to v2.0.2.</li></td>
        <td>December 4, 2019</td>
        <td>-</td>
    </tr>
</table>

## November 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.4.0 release</td>
        <td><li> Added internal error reporting.</li> <li> Added the compatibility with Huawei PUSH v3.</li> <li> Added the compatibility with OnePlus devices.</li></td>
        <td>November 21, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.3.2 release</td>
        <td>Optimized statistics collection.</td>
        <td>November 13, 2019</td>
        <td>-</td>
    </tr>
    <tr>
        <td>SDK v1.1.3.1 release</td>
        <td>Optimized the network.</td>
        <td>November 11, 2019</td>
        <td>-</td>
    </tr>
</table>

## October 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.3.0 release</td>
        <td><li> Optimized data reporting.</li> <li> Optimized logging to add the local log reporting feature.</li> <li> Added API call chaining.</li> <li> Optimized the system internally to improve resource release.</li></td>
        <td>October 31, 2019</td>
        <td>-</td>
    </tr>
</table>

## September 2019

<table>
<tr>
    <th width=20%>Update</th>
    <th width=44%>Description</th>
    <th width=16%>Release Date</th>
    <th width=20%>Documentation</th>
</tr>
    <tr>
        <td>SDK v1.1.2.1 release</td>
        <td><li> Optimized the notification bar display.</li> <li> Optimized some APIs.</li> <li> Added the support for audio rich media.</li> <li> Optimized the SDK internally.</li></td>
        <td>September 27, 2019</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/30713#.E9.9B.86.E6.88.90.E6.96.B9.E6.B3.95">Usage of audiovisual rich media</a></td>
    </tr>
</table>

