
CI provides multiple basic image processing features that facilitate various scenarios. For the supported basic image processing features, please see [Overview](https://intl.cloud.tencent.com/document/product/1045/33424).

>?
>- You can use APIs to process images during download. In addition, CI’s [Pipeline Operator](https://intl.cloud.tencent.com/document/product/1045/33727) allows you to perform multiple processing on images in sequence.
>- Currently, CI offers a 10 TB/month free tier for basic image processing. Exceeded usage will be charged at regular rates. For more information, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).





## Directions

#### Using CI console

You can process images using the CI console. For more information, please see [Setting Styles](https://intl.cloud.tencent.com/document/product/1045/33443).

### Using RESTful APIs

You can process images using the APIs provided by CI. For more information, please see the API Documentation of [Basic Image Processing](https://intl.cloud.tencent.com/zh/document/product/1045/33694).

## Restrictions

- Format: Currently, processing JPG, BMP, GIF, PNG, and WebP, as well as decoding and processing HEIF are supported.
- Size: The size of an original image cannot be larger than 20 MB, its width and height cannot exceed 30,000 pixels, and the total number of pixels cannot exceed 250 million. The width and height of the destination image cannot exceed 9,999 pixels. For a source animated image, Width x Height x Number of frames cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.
