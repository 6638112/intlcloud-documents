[](id:senderConfig)
## Sender Configuration Options
Simple Email Service (SES) provides three ways to send emails: SES console, SES API, and SES SMTP. You can send emails by calling APIs with SES command line interface (SES CLI) or [SES SDK] (https://intl.cloud.tencent.com/document/product/1084/39387) or by calling SMTP APIs.

To send an email, see [**Console Guide** > **Email Sending**](https://intl.cloud.tencent.com/document/product/1084/40178).
## Flexible Deployment Options
### Shared IP Addresses
Generally, SES sends emails from shared IP addresses in the shared IP pool by default. Shared addresses are a fast and easy-to-use option for users who want to start sending with established IPs immediately. Tencent Cloud helps ensure the quality of shared IPs and a high delivery rate.
### Dedicated IP Addresses
A dedicated IP is an IP specially assigned to you by Tencent Cloud for sending emails. Generally, it has never been used for email sending or has enjoyed a good reputation all along, ensuring that it will not be marked as a spam IP by anti-spam organizations. You can apply for a dedicated IP subject to your sending volume. If you need to send a large number of emails, contact your sales rep to apply for a dedicated IP.


## Sender Identity Management and Security
When receiving an email, an internet service provider (ISP) will check whether it is authenticated before delivering it to the recipient. Authentication proves to the ISP that you are the owner of the email address you are sending from. SES supports all industry-standard authentication mechanisms, including Sender Policy Framework (SPF), Domain Keys Identified Mail (DKIM), and Domain-Based Message Authentication, Reporting and Conformance (DMARC). It can ensure that your emails pass the ISP checks and are delivered to recipients successfully.
## Sending Statistics
SES provides a variety of methods to monitor email sending activities. For example, it can capture the information about the entire email response funnel (including the numbers of deliveries, opens, clicks, and bounces), and provide accurate data analysis. In addition, you can check the sending status of a specific email by calling [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502) to help you adjust your email sending policy.

[](id:warmUp)

## Automatic Warm-up 
### Features
The email delivery process can be extremely complicated. The reputation of an IP/domain is vital to improving deliverability. Warm-up is a process of building up your sending reputation. The sending volume must be increased gradually day by day, and cannot be lifted to the desired level at a stroke. A good warm-up helps establish a good reputation with your ISP.
>? Automatic warm-up refers to automatically warming up your IP addresses or sender domains without manual intervention throughout the process.
### Description
Automatic warm-up is divided into two categories: [Standard Rules (Default)](#default) and [Upgraded Rules](#upgrade).

#### Default rules:
Standard warm-up rules apply by default under the batch sending mode. The backend will determine the warm-up progress based on a series of policies and automatically assign the daily sending quota. The entire process is completely automatic. When the maximum number of sent emails allowed per day is reached, email sending will stop and extra emails will enter the cache queue and be sent 24 hours later. The standard warm-up plan is shown here: [](id:default)

<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Day</td>
      <th width="0px" style="text-align:center">Sending Volume/Day</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">500</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >1,000</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >2,000</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >5,000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >10,000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >20,000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10000" >40,000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20000" >60,000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >80,000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >100,000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >150,000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >200,000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >300,000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >400,000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >500,000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >600,000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >700,000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >800,000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >900,000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1,000,000</td>
	</tr>
</table>

[](id:customize)
#### Custom rules:
If the standard warm-up plan cannot satisfy your needs, you can pursue a upgraded warm-up plan for high-quality emails. For details, contact your sales rep to apply for.
[](id:batch)
## Batch Feature Set
This is suitable for batch sending of marketing or notification emails. To send trigger-based emails (such as authentication and transactional emails), we recommend you call the `SendEmail` API.
### Features
You can use the SES batch sending feature in either of the following ways:
• Console: A template is required, the email size must not exceed 10 MB, and attachments are not supported.
• API: A template is required, the email size must not exceed 10 MB, and attachments are supported.

### Description
You can manage sender addresses on the **Email Sending** > **Recipient Groups** page in the console.

The batch sending feature is set to use the standard warm-up plan. The backend will automatically identify the reputation of the IP/domain and assign the daily sending quota. Later, the backend will automatically determine whether the total sending volume exceeds the maximum number allowed per day, and if it does, email sending will stop, and extra emails will enter the cache queue and be sent 24 hours later.

## Batch
To send emails in batches, create a sending task in the console, select **Batch** for **Task Type**, and set all required fields for the task.
## Scheduled
Emails can be sent at a scheduled time. If you select **Start Time** for the task, the emails will be sent automatically at the specified time.
## Recurring
To send recurring emails, specify fields such as**Start Time** and **Recurrence** in the console. The console will automatically send emails based on the specified recurrence.
## Mailbox Simulator
The SES mailbox simulator can help you easily test your application responses in various scenarios (such as bounces) without affecting sender reputation. You can send test emails to simulate successful delivery, bounce, unsubscription, and other scenarios with the mailbox simulator.
- Emails sent to the mailbox simulator are not real ones but simulated ones only.
- You can simulate email sending free of charge in the console.
- Each simulated scenario corresponds to a specific email address.
