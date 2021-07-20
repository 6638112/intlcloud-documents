## Overview
CI’s Image Watermarking feature is implemented using the **watermark** API. Currently, only image watermarks stored in CI are supported. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, its total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

An image can be processed:

- Upon download
- Upon upload
- In cloud


>? 
> - You can overlay up to 10 image watermarks over a single image.
> - An animated image cannot be used as a watermark.
> 

## API Format

#### 1. Processing upon download

```shell
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

> ? Spaces and line breaks above are for readability only and can be ignored.

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
      "rule": "watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>"
  }]
}
```

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
      "rule": "watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>"
  }]
}
```

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use **Processing upon upload** or **Processing in-cloud data**.

## Parameters

In the code above, `watermark` is the operation name and the number `1` indicates that the watermark is an image.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /image/      | [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430) URL of the image watermark. For example, if the image watermark URL is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, you should set this parameter to `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc`.  |
| /gravity/    | Position of the image watermark, which is a square in a [3x3 grid](#1). Default value: `southeast` |
| /dx/  | Horizontal offset in pixels. Default value: `0` |
| /dy/  | Vertical offset in pixels. Default value: `0` |
| /blogo/      | Adaptation mode for an image watermark that is larger than the input image. Valid values: <br><li>`1`: scales the image watermark to the size of the input image. <br><li>`2`: crops the image watermark to the size of the input image. |
| /scatype/    | Scaling mode for the image watermark (relative to the input image). This parameter must be used together with `/spcent/`. Valid values: <br><li>`1`: scales by width.<br><li>`2`: scales by height.<br><li>`3`: scales by area. </li> |
| /spcent/     | Scale ratio of the image watermark (relative to the input image), in permillage. This parameter must be used together with `/scatype/`. Value range: [1,1000]. By default, the image watermark is not scaled. |

>! An image watermark must:  
> - Be stored in the same bucket as the input image.
> - Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible (if the image watermark is set to private-read, it must carry a signature).
> - Have a URL starting with `http://`. Note that “http://” cannot be omitted or changed to “https://”. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.
> 

<span id="1"></span>
## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter to position your watermark, the corresponding red dot becomes the reference point of the square, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>?
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid and the watermark will be centered horizontally.
> - If `gravity` is set to `west` or `east`, `dy` is invalid and the watermark will be centered vertically.
> 

## Examples

#### Adding an image watermark

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

After an image watermark is added:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)

#### Adding an image watermark with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>


