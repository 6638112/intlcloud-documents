### What should I do if my signature application is rejected?

You need to provide corresponding qualification certificates to apply for an SMS signature. Please enter the signature content again and upload correct and authentic certificates according to the SMS signature review standards.

### Why is the rejection reason "neutral signature"?

A neutral signature is a signature in which the relevant organizational or individual identity cannot be identified. For example, you cannot use `test`, `aabb`, `verification code`, or `notification` as a signature. You are recommended to use the name of your organization, application name, WeChat Official Account, or WeChat Mini Program as the signature.

### Is there a limit on the number of SMS signatures?
You can apply for up to 200 SMS signatures. To apply for multiple signatures, you need to provide corresponding qualification certificates for each signature.

### Can I modify an SMS signature?
Approved signatures cannot be modified. You can create multiple signatures and select an appropriate one when sending messages.

### How do I apply for a signature when my product is in beta test and cannot be released?
If your product has not been released, please use your organization name to apply for a signature for product testing. After it is released, you can apply for a signature containing your product name.

### Why can't my SMS signature application pass the review?

There are many possible reasons; for example, the signature does not meet the submitted certificates or relevant certificates have not been uploaded.

### What should I enter as signature remarks?
You need to enter **application remarks** only when the signature type is one of the following:
- Application: enter a link to the display page of the application on any application store/market.
- Website: enter the website domain name that has an ICP filing.
- WeChat Official Account (or WeChat Mini Program): enter the full name of the WeChat Official Account (or WeChat Mini Program).

<span id="Q8"></span>
### How do I specify a signature when calling an API to send a message if I have multiple signatures?
When calling the [SendSms](https://intl.cloud.tencent.com/document/product/382/34859) API to send messages, you can set the `sign` field to select the needed SMS signature.
 For example, if you have two signatures `Tencent Technology` and `Tencent Cloud` and need to send SMS messages with the latter, you only need to set the `sign` field to `Tencent Cloud` and call the corresponding API to send messages.
