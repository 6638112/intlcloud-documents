
To enable LVB porn detection, you need to enable LVB screencapture first either in the [LVB console](https://intl.cloud.tencent.com/document/product/267/31072) or through API. This document describes how to implement LVB porn detection through API.

## Enabling LVB Porn Detection
As the LVB porn detection feature is based on the LVB screencapture feature, you have to enable LVB screencapture first before you can enable LVB porn detection. The steps are as follows:

### 1. Create a porn detection-enabled LVB screencapture template
Call [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834) and set `PornFlag` to 1 to create a porn detection-enabled LVB screencapture template.

### 2. Create a porn detection-enabled LVB screencapture rule
Call [CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835) to create a porn detection-enabled LVB screencapture rule and bind the LVB screencapture template ID created in step 1 to the `AppID`, `DomainName`, `AppName`, and `StreamName` of the live stream that needs to undergo porn detection.

### 3. Start a live stream and start porn detection
After a porn detection-enabled LVB screencapture rule is created, the porn detection feature will be automatically enabled for new live streams. If you want to enable porn detection for a live stream that is in progress, you need to stop and restart the stream for the feature to take effect.

## Getting LVB Porn Detection Result
After LVB porn detection is enabled, you can configure the registered callback domain name in the porn detection callback template to have the LVB backend call back the porn detection result.
>! By default, only suspicious results will be called back.

### 1. Create an LVB porn detection callback template
Call [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) and set `PornCensorshipNotifyUrl` to your domain name to create an LVB porn detection callback template.
### 2. Create an LVB porn detection callback rule

Call [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) to create a porn detection-enabled LVB screencapture rule and bind the LVB screencapture template ID created in the previous step to the `AppId`, `DomainName`, and `AppName` of the live stream that needs to undergo porn detection.

### 3. Get the porn detection result
The LVB backend sends the porn detection result to your registered domain name through an HTTP POST request where the result is stored in the HTTP body in JSON format. You can determine whether the live stream is pornographic by the `type` field alone.
>!We recommend you use the `type` of an image to determine whether it is pornographic. As the detection system cannot achieve 100% accuracy, there may be false positives or false negatives, and human confirmation is recommended.  

#### Complete protocol
| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| tid | Yes | Number | Alert policy ID. Video content alert: 20001 |
| streamId | No | String | Stream name |
| channelId | No | string | Channel ID |
| img | Yes | string | Link to alerted image |
| type | Yes | Array | Image type. 0: normal, 1–5: non-compliant, 6–9: others |
| confidence | Yes | Number | Confidence of detected pornographic information in the range of 0–100, which is an overall score of `normalScore`, `hotScore`, and `pornScore` |
| normalScore | Yes | Number | Normal score of image |
| hotScore | Yes | Number | Sexual score of image |
| pornScore | Yes | Number | Pornographic score of image |
| level | No | Number | Image level |
| ocrMsg | No | string | OCR information of image (if any) |
| screenshotTime | Yes | Number | Screencaptured time |
| sendTime | Yes | Number | Request sent time (UNIX timestamp) |
| abductionRisk | No | Array | An array containing the `AbductionRisk` structure |
| gameDetails | No | Object | Game details |
| similarScore  | No | Number | Similarity score of image |
| stream_param  | No | String | Push parameter 
| app  | No | String | Push domain name |
| appid  | No | Number | Business ID |
| appname  | No | String | Push path |



#### AbductionRisk description

| **Parameter** | **Required ** | **Data Type** | **Description** |
| --- | --- | --- | --- |
| level | Yes | Number | Risk level in the range of 0–4. The larger the number, the higher the risk. 3 and 4 indicate maliciousness and should be handled |
| type | Yes | Number | Risk type. 20002: porn |

#### faceDetail description
| **Parameter** | **Required** | **Type** | **Description** |
| --- | --- | --- | --- |
| gender | No | Number | Gender [0 (female)–100 (male)] |
| age | No | Number | Age |
| expression | No | Number | Expression [0 (normal)–50 (smile)–100 (laugh)] |
| beauty | No | Number | Charm [0–100] |
| x | No | Number | x coordinate of the top-left corner of face frame |
| y | No | Number | y coordinate of the top-left corner of face frame |
| width | No | Number | Face frame width |
| height | No | Number | Face frame height |

#### gameDetails description
| **Parameter** | **Required** | **Type** | **Description** |
| --- | --- | --- | --- |
| battlegrounds | No | Object | PUBG information |
| gameList | No | Array | Game list |

#### gameList description

| **Parameter** | **Required** | **Type** | **Description** |
| --- | --- | --- | --- |
| name | No | String | Game name |
| confidence | No | Number | Probability |


#### Sample request
HTTP Body:
```
{
    "ocrMsg":"",
            
    "type":[2],
            
    "confidence":0,
            
    "normalScore":2,
            
    "hotScore":97,
            
    "pornScore":0,
            
    "screenshotTime":1575513174,
            
    "level":0,
            
    "img":"http://test-10000.cos.ap-shanghai.myqcloud.com/2019-12-05/teststream-screenshot-10-32-54-960x540.jpg",
            
    "abductionRisk":[ ],
            
    "sendTime":1575513176,
            
    "similarScore":0,
            
    "tid":20001,
            
    "streamId":"teststream",
            
    "channelId":"teststream",
            
    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
            
    "app":"testlive.myqcloud.com",
            
    "appname":"live",
            
    "appid":10000
}  
```

## Disabling LVB Porn Detection

LVB porn detection can be disabled by deleting the screencapture rule or modifying the screencapture template. Both deletion and modification are effective only for new live streams. If you want to disable LVB porn detection for a live stream that has already started, you have to stop and restart the stream.

### 1. Delete the porn detection-enabled screencapture rule

Call [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833) to delete the corresponding LVB screencapture rule under `DomainName`, `AppName`, and `StreamName` by template ID.

### 2. Delete or modify the porn detection-enabled screencapture template

Call [ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828) to set the porn detection flag of the LVB screencapture template to 0.
