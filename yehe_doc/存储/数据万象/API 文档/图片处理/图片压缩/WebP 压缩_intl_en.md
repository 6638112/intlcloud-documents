## Feature Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the WebP compression feature to convert images into WebP format, a format that outperforms JPG in terms of compression. WebP offers over 25% smaller file sizes at the same quality compared with JPG, making it suitable for more clients.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, TPG, HEIF, AVIF, or other formats can be converted into WebP.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.

## Use Directions

CI uses the **imageMogr2** API to provide the WebP compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? 
>- WebP compression is billed at the basic image processing ratio. For detailed pricing, see Image Processing Fees.
>- If an image is converted into WebP, some browsers may not be able to read its EXIF data. As a result, the image cannot be rotated. You can add the `auto-orient` parameter to rotate the input image first (see [Rotation](https://intl.cloud.tencent.com/document/product/1045/33715)) before compressing it.
>- WebP compression inherits the quality parameters of the input image by default. You can adjust the compression ratio by modifying the image quality as instructed in [Quality Change](https://intl.cloud.tencent.com/document/product/1045/33717).
>


## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/webp
```

#### 2. Processing upon upload

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/webp"
}]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
>

#### 3. Processing in-cloud data

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/webp"
}]
}
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format> | Compression format, which is `webp`     |

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **Processing upon upload** or **Processing in-cloud data** instead.
>

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image into WebP format by using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp
```

Output image:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp)

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :------------------- |
| PNG (input image) | 1,335.2 KB |
| WebP | 65 KB (compression ratio: 95.13%) |
