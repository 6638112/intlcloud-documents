## Feature Description
This API (`CreateMediaTemplate`) is used to create a top speed codec transcoding template.

## Request

#### Sample request

```shell
POST /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
    <Tag>HighSpeedHd</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Crf></Crf>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
        <Gop></Gop>
        <Preset>medium</Preset>
        <ScanMode></ScanMode>
        <Bufsize>0</Bufsize>
        <Maxrate>0</Maxrate>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| -----------------  | ------ | -------------  | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Template type: HighSpeedHd                                | String    | Yes   | None |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                                 | Container | Yes   | None   |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                                 | Container | Yes   | None   |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |

<br/>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| -------------------| ------- | ------------------------------------| --------- | ---- |
| Format             | Request.Container | Container format. Valid values: mp4, flv, hls | String | Yes       |

Audio/Video formats supported by different container formats are as follows:

| Container                  | Audio Codecs  | Video Codecs          |
| -------------------------- | ------------- | --------------------- |
| mp4/hls                    | AAC, MP3      | H.264, H.265          |
| flv                        | AAC, MP3      | H.264                 |


`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | Codec format             | String | No   |   H.264 | H.264, H.265  |
| Width              | Request.Video | Width                 | String | No       | Original video width | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3.If only `Width` is set, `Height` is calculated according to the original video aspect ratio.<br/>4.This parameter must be an even number. |
| Height             | Request.Video | Height                 | String | No   | Original video height | 1. Value range: [128, 4096]<br/>2.Unit: px<br/>3. If only `Height` is set, `Width` is calculated according to the original video aspect ratio.<br/>4. This parameter must be an even number. |
| Fps                        | Request.Video | Frame rate                  | String | No   | None           | 1. Value range: (0, 60]<br>2. Unit: fps |
| Profile                    | Request.Video | Encoding level              | String | No   | high         | 1. Valid values: baseline, main, high <br/>2. baseline: Suitable for mobile devices<br/>3. main: Suitable for standard resolution devices <br/>4. high: Suitable for high resolution devices <br/>5. Only H.264 supports this parameter. |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps                  |
| Crf                | Request.Video | Bitrate, which is a quality control factor  | String | No       | None           | 1. Value range: (0, 51]<br/>2. If `Crf` is set, the setting of `Bitrate` becomes invalid.<br/>3. If `Bitrate` is empty, `25` is used for this parameter by default. |
| Gop                | Request.Video | Maximum number of frames between two keyframes   | String | No       | None           | Value range: [0, 100000]                                       |
| Preset                     | Request.Video | Video algorithm preset        | String | No   | medium       |  1. Only H.264 supports this parameter.<br/>2. Valid values: veryfast, fast, medium, slow, slower |
| Bufsize                    | Request.Video | Buffer size            | String | No   | None           | 1. Value range: [1000, 128000]<br/>2. Unit: Kb<br/> |
| Maxrate                    | Request.Video | Peak video bitrate          | String | No   | None           | 1. Value range: [10, 50000]<br/>2. Unit: Kbps<br/> |
| HlsTsTime                  | Request.Video | HLS segment time          | String | No   | 5            | 1. (0, video duration] <br/>2.Unit: second |
| Pixfmt                     | Request.Video | Video color format          | String | No   | None           | yuv420p |


`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------| -------- | --------- | ---- |--------| ----- |
| Start              | Request.TimeInterval | Start time | String    | No   | None     | 1. [0, video duration] <br/> 2. Unit: second <br/> 3. Supports the float format, accurate to the millisecond. |
| Duration           | Request.TimeInterval | Duration | String    | No   | None     | 1. [0, video duration] <br/> 2. Unit: second <br/> 3. Supports the float format, accurate to the millisecond. |


`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ---- |
| Codec              | Request.Audio | Codec format     | String | No   | aac    | Valid values: aac, mp3 |
| Samplerate         | Request.Audio | Sample rate         | String | No   | 44100  | 1. Unit: Hz<br/>2. Valid values: 11025, 22050, 32000, 44100, 48000, 96000<br/>3. Different container formats support different MP3 sample rates, as shown in the table below.|
| Bitrate            | Request.Audio | Original audio bitrate   | String | No   | None     | 1. Unit: Kbps<br/>2. Value range: [8, 1000]|
| Channels           | Request.Audio | Number of sound channels         | String | No   |  None      | 1. If `Codec` is `aac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.<br/>2. If `Codec` is `mp3`, the value can be `1` or `2`. |


>? Y indicates supported, and N indicates unsupported.
>

| Container Format/Audio Sample Rate | 11025 | 22050 | 32000 | 44100 | 48000 | 96000 |
| ------------------ | ----- | ----- | ----- | ----- | ------| ------|
| flv	             | Y     | 	Y    | 	N    | 	Y    | 	N    | 	N    |
| mp4                | N     | 	Y    | 	Y    | 	Y    | 	Y    | 	N    |
| hls                | Y     | 	Y    | 	Y    | 	Y    | 	Y    | 	N    |


`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ---- |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | 1. Valid values: true, false <br/> 2. If the value is `false`, transcoding is performed based on settings.      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment method               | String    | No       | 0      | 1. Valid values: 0, 1. `0` indicates to use the original video resolution. `1` indicates to return the transcoding failure message.<br/>2. This parameter is valid only when `IsCheckReso` is `true`. |
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | Valid values: true, false                                                   |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>HighSpeedHd</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <HighSpeedHd>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </HighSpeedHd>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template     | Template ID                                                      | String    |
| Name               | Response.Template     | Template name                                                     | String    |
| BucketId           | Response.Template     | Template bucket                                                | String    |
| Category           | Response.Template     | Template category: Custom or Official                                | String    |
| Tag                | Response.Template | Template type: HighSpeedHd                                       | String    |
| UpdateTime         | Response.Template     | Update time                                                     | String    |
| CreateTime         | Response.Template     | Creation time                                                     | String    |
| HighSpeedHd        | Response.Template     | Template parameters                                                | Container |


`HighSpeedHd` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :-------------------------------------- | :-------- |
| TimeInterval       | Response.Template.HighSpeedHd | Same as `Request.TimeInterval` in the request body.  | Container |
| Container          | Response.Template.HighSpeedHd | Same as `Request.Container` in the request body.     | Container |
| Video              | Response.Template.HighSpeedHd | Same as `Request.Video` in the request body.         | Container |
| Audio              | Response.Template.HighSpeedHd | Same as `Request.Audio` in the request body.         | Container |
| TransConfig        | Response.Template.HighSpeedHd | Same as `Request.TransConfig` in the request body.   | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>HighSpeedHd</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Crf></Crf>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
        <Gop></Gop>
        <Preset>medium</Preset>
        <ScanMode></ScanMode>
        <Bufsize>0</Bufsize>
        <Maxrate>0</Maxrate>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>HighSpeedHd</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <HighSpeedHd>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </HighSpeedHd>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
