### What should I do if the client cannot consume messages?

**Error description**

The consumer cannot pull messages.

**Possible causes**

Check whether the consumer group has a heap. If there is no heap, an empty message will be returned after the `fetch.max.wait` time elapses. This parameter is configured by the consumer client and 500 ms by default as shown below:

```
# Fetch request wait time
fetch.max.wait.ms=500
```

![](https://main.qcloudimg.com/raw/05c88d97f36784e5f83c08b24e229265.png)



**Solution**

- If messages heap up, but no messages are pulled, we recommend you check the client SDK version. If the SDK version is low, please upgrade it as instructed in [SDK Overview](https://intl.cloud.tencent.com/document/product/597/41028).
- You can also [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
