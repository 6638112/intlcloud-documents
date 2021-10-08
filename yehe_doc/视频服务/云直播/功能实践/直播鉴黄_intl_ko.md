
라이브 방송 음란물 감지를 활성화하려면 먼저 라이브 방송 화면 캡처 기능을 활성화해야 합니다. 이는 [CSS 콘솔](https://intl.cloud.tencent.com/document/product/267/31072) 또는 라이브 방송 화면 캡처 및 음란물 감지 API를 통해 실현할 수 있습니다. 본 문서에서는 라이브 방송 화면 캡처 및 음란물 감지 API를 통해 라이브 방송 음란물 감지 기능을 사용하는 방법을 설명합니다.

## 라이브 방송 음란물 감지 활성화
라이브 방송 음란물 감지는 라이브 방송 화면 캡처를 기반으로 하므로, 라이브 방송 음란물 감지 기능을 사용하려면 먼저 라이브 방송 화면 캡처 기능을 활성화해야 합니다. 다음은 구체적인 활성화 방법입니다.

### 1. 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 템플릿 생성
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)을 호출한 후에 PornFlag = 1을 설정하여 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 템플릿을 생성합니다.

### 2. 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙 생성
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)을 호출해 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙을 생성한 후, 1단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지 기능이 필요한 라이브 방송 AppId, DomainName, AppName, StreamName 차원에 연결합니다.

### 3. 라이브 방송 시작 후 음란물 감지 시작
음란물 감지 규칙이 적용된 라이브 방송 화면 캡처 규칙을 생성하고 나면 새로 시작되는 라이브 방송에 자동으로 음란물 감지 기능이 적용됩니다. 진행 중인 라이브 방송 스트리밍에서 음란물 감지 기능을 활성화하려면 방송을 정지하고 다시 시작해야 합니다.

## 라이브 방송 음란물 감지 결과 획득
라이브 방송 음란물 감지 기능을 활성화하고 나면 음란물 감지 콜백 템플릿에서 접속할 콜백 도메인을 설정할 수 있습니다. 이를 통해 CSS 백그라운드에서 음란물 감지 결과가 콜백됩니다.
>! 기본적으로 의심스러운 결과만 콜백하며, 정상적인 결과는 콜백하지 않습니다.

### 1. 라이브 방송 음란물 감지 콜백 템플릿 생성
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)을 호출한 후에 PornCensorshipNotifyUrl 매개변수를 귀하의 도메인으로 설정하여 라이브 방송 음란물 감지 콜백 템플릿을 생성합니다.
### 2. 라이브 방송 음란물 감지 콜백 규칙 생성

[CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)을 호출해 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙을 생성한 후, 이전 단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지 콜백이 필요한 라이브 방송 AppId, DomainName, AppName 차원에 연결합니다.

### 3. 음란물 감지 결과 획득
라이브 방송 백그라운드에서는 음란물 감지 결과를 HTTP POST 요청을 통해 귀하가 접속한 도메인으로 전송합니다. 음란물 감지 결과는 HTTP Body에 JSON 포맷으로 저장되므로, 해당 라이브 방송의 음란물 여부는 type 필드에서만 확인할 수 있습니다.
>!이미지를 사용한 `type`으로 음란물 판정을 진행할 것을 권장합니다. 검사 시스템의 정확도가 100%를 달성할 수는 없기 때문에, 일부 이미지가 음란물 의심 판정을 받거나 잘못된 식별 결과가 나올 수 있습니다. 육안으로 2차 확인 작업을 진행할 것을 권장합니다.  

#### 전체 프로토콜은 다음과 같습니다.
| 매개변수      | 필수 입력 여부 | 데이터 유형 | 설명                                                    |
| ---------- | ---------- | ---------- | --------------------------- |
| streamId       | 선택 사항         | String       | 스트림 이름                                                       |
| channelId      | 선택 사항         | string       | 채널 ID                                                      |
| img | 필수 입력 | string | 알람 이미지 링크 |
| type | 필수 입력    | Array | 점검 결과(labelResults)에 상응하는**우선순위가 가장 높은 악성 태그**를 반환하며 모델에서 권장하는 심사 결과를 표시합니다. 비즈니스 상황에 맞춰, 규정 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>0:정상<li/>1: 음란물<li/>6: 욕설<li/>8: 광고<li/>2-5, 7: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| score | 필수 입력     | Array | type 해당 평점 |
| hotScore       | 필수 입력         | Number       | 선정적 이미지 평점                                         |
| pornScore      | 필수 입력         | Number       | 음란성 이미지 평점                                         |
| illegalScore |  필수 입력 | Number  | 불법 이미지 평점 |
| polityScore    | 필수 입력         | Number       | 정치 관련 이미지 평점                                         |
| terrorScore  | 필수 입력 | Number  | 테러 관련 이미지 평점|
| abuseScore | 필수 입력     | Number | 욕설 관련 이미지 평점 |
| teenagerScore | 필수 입력     | Number | 청소년에게 부적절한 이미지 평점 |
| adScore | 필수 입력     | Number | adScore 이미지 평점 |
| ocrMsg         | 선택 사항         | string       | 이미지의 OCR 식별 정보(존재할 경우)                              |
| suggestion | 필수 입력     | string | 권장 값, 선택 가능 값:<ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 정상</ul>     |
| label | 필수 입력     | string                | 점검 결과(labelResults)에 상응하는**우선순위가 가장 높은 악성 태그**를 반환하며 모델에서 권장하는 심사 결과를 표시합니다. 비즈니스 상황에 맞춰, 규정 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| subLabel | 필수 입력     | string | 서브 태그 이름, 서브 태그 미스 시, 공백 반환             |
| labelResults | 선택 사항    | Array of [LabelResult](#labelresult)  | 음란물, 선정적인 내용, 폭력, 불법 규정 위반 등 심사 결과를 포함한 분류 점검 모델 심사 결과 |
| objectResults | 선택 사항     | Array of [ObjectResult](#objectresult) | 정치적 내용, 광고 마크, QR 코드 등 심사 정보를 포함한 점검 모델 심사 결과  |
| ocrResults | 선택 사항     | Array of [OcrResult](#ocrresult) | OCR 텍스트 관련 정보 및 텍스트 심사 상세 결과를 포함한 OCR 텍스트 심사 결과 |
| libResults | 선택 사항     | Array of [LibResult](#libresult) | 리스크 이미지 라이브러리 심사 결과 |
| screenshotTime | 필수 입력         | Number       | 화면 캡처 시간                                                     |
| sendTime       | 필수 입력         | Number       | 요청 발송 시간, UNIX 타임스탬프                                    |
| similarScore   | 선택 사항         | Number       | 이미지 유사도 평점                                               |
| stream_param   | 선택 사항         | String       | 푸시 스트림 매개변수                                                     |
| app  | 선택 사항 | String | 푸시 스트림 도메인 |
| appid  | 선택 사항 | Number | 비즈니스 ID  |
| appname        | 선택 사항         | String       | 푸시 스트림 path 경로                                               |

 

#### LabelResult
분류 모델 히트 결과.

| 이름   | 유형                 | 설명                                                     |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | 모델 식별 시나리오 결과 반환, 예: 광고, 음란물, 유해 콘텐츠 등 시나리오.      |
| Suggestion | String                                       | 현재 악성 태그의 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값:<ul style="margin:0"><li/>Block:차단 권장<li/>Review:수동 재심사 권장<li/>Pass:통과 권장</ul> |
| Label      | String                                       | 점검 결과에 상응하는 악성 태그를 반환합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| SubLabel   | String | 서브 태그 이름                                                   |
| Score      | Integer | 해당 태그 모델 히트 점수                                         |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 분류 모델의 서브 태그 히트 상세 결과                                   |

#### LabelDetailItem

분류 모델의 서브 태그 히트 결과.

| 이름   | 유형               | 설명                |
| -------- | -------- | --------------------------- |
| Id       | Integer  | 시리얼 넘버                        |
| Name     | String   | 서브 태그 이름                  |
| Score    | Integer  | 서브 태그 점수, 점수 범위 0점 - 100점|


#### ObjectResult

엔터티 점검 상세 결과.

| 이름   | 유형              | 설명              |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                 | 식별 엔터티 시나리오 결과 반환, 예: QR 코드, logo, 이미지 OCR 등 시나리오. |
| Suggestion | String                                 | 현재 악성 태그의 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값:<ul style="margin:0"><li/>Block:차단 권장<li/>Review::수동 재심사 권장<li/>Pass:통과 권장</ul> |
| Label      | String                                 | 점검 결과에 상응하는 악성 태그를 반환하며 모델에서 권장하는 심사 결과를 표시합니다. 비즈니스 상황에 맞춰, 규정 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| SubLabel   | String             | 서브 태그 이름 |
| Score      | Integer | 해당 시나리오 모델의 서브 태그 히트 점수, 점수 범위 0점 - 100점 |
| Names      | Array of String       | 엔터티 이름 리스트 |
| Details    | Array of [ObjectDetail](#objectdetail) | 점검 상세 결과 |

#### ObjectDetail

점검 상세 결과로 시나리오가 정치, 정치적 인물, 광고 마크, QR 코드 및 안면 속성과 관련된 내용이면 모델 점검 타깃창의 태그 이름, 태그값, 태그 점수 및 점검창의 위치 정보를 표시합니다.

| 이름   | 유형               | 설명                |
| -------- | -------- | -------- |
| Id       | Integer  | 시리얼 넘버  |
| Name     | String   | 태그 이름  |
| Value    | String   | 태그값:<ul style="margin:0"><li/>시나리오가 Ad일 때, URL 주소를 표시합니다. 예를 들어 Name이 QrCode일 때, Value 값은 `http//abc.com/aaa`<br><li/>시나리오가 FaceAttribute일 때는 안면 속성 정보를 의미합니다. 예를 들어 Name이 Age일 때, Value 값은 `18`입니다.</ul>|
| Score    | Integer  | 점수, 점수 범위 0점 - 100점 |
| Location | [Location](#location) | 점검창 좌표 |

#### Location

좌표.

| 이름   | 유형               | 설명                |
| -------- | -------- | ---------------- |
| X        | Float    | 왼쪽 상단 가로 좌표     |
| Y        | Float    | 왼쪽 상단 세로 좌표     |
| Width    | Float    | 폭             |
| Height   | Float    | 높이             |
| Rotate   | Float    | 점검창의 회전 각도 |

#### OcrResult

OCR 결과 점검 상세 내용.

| 이름   | 유형               | 설명                |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | 식별 시나리오 표시, 기본 값 OCR(이미지 OCR 식별).              |
| Suggestion | String                                   | 우선순위가 가장 높은 악성 태그에 상응하는 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값:<ul style="margin:0"><li/>Block:차단 권장<li/>Review:수동 재심사 권장<li/>Pass:통과 권장</ul> |
| Label      | String                                   | OCR 점검 결과에 상응하는 우선순위가 가장 높은 악성 태그를 반환하며 모델에서 권장하는 심사 결과를 표시합니다. 비즈니스 상황에 맞춰, 규정 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| SubLabel   | String             | 서브 태그 이름 |
| Score      | Integer | 해당 시나리오 모델의 서브 태그 히트 점수, 점수 범위 0점 - 100점 |
| Text       | String | 텍스트 콘텐츠 |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 상세 결과 |


#### OcrTextDetail
OCR 텍스트 상세 결과.

| 이름 | 유형        | 설명                                                     |
| -------- | --------------- | --------------- |
| Text     | String                | OCR 식별 텍스트 콘텐츠 반환(OCR 텍스트 식별**5000 바이트 이내**로 제한). |
| Label      | String                           | 점검 결과에 상응하는 악성 태그를 반환합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| Keywords | Array of String | 해당 태그에 히트된 키워드 |
| Score    | Integer         | 해당 태그 모델의 히트 점수, 점수 범위 0점 - 100점 |
| Location | [Location](#location) | OCR 텍스트 좌표 위치 |


#### LibResult
블랙/화이트 라이브러리 상세 내용

| 이름   | 유형           | 설명                                                     |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | 모델의 시나리오 식별 결과 표시, 기본값 Similar.                 |
| Suggestion | String                           | 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값:<ul style="margin:0"><li/>Block:차단 권장<li/>Review:수동 재심사 권장<li/>Pass:통과 권장</ul> |
| Label      | String                           | 점검 결과에 상응하는 악성 태그를 반환합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom: 기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| SubLabel   | String             | 서브 태그 이름 |
| Score      | Integer            | 이미지 인덱스 모델 식별 점수, 점수 범위 0점 - 100점 |
| Details    | Array of [LibDetail](#libdetail) | 블랙/화이트 라이브러리  결과 상세 내용 |

#### LibDetail
사용자 정의 라이브러리/블랙/화이트 라이브러리 상세 내용

| 이름   | 유형                 | 설명                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | 시리얼 넘버                                                         |
| ImageId  | String   | 이미지 ID                                                       |
| Label    | String                | 점검 결과에 상응하는 악성 태그를 반환합니다. 반환값: <ul style="margin:0"><li/>Normal: 정상<li/>Porn: 음란물<li/>Abuse: 욕설<li/>Ad: 광고<li/>Custom:기타 반감을 일으키는, 안전하지 않고 적절하지 않은 콘텐츠 유형</ul> |
| Tag      | String   | 사용자 정의 태그                                                   |
| Score    | Integer  | 모델 식별 점수, 점수 범위 0점 - 100점                               |



#### 요청 예시
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "hotScore": 0,
        "pornScore": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "illegalScore": 0,
        "polityScore": 0,
        "similarScore": 0,
        "terrorScore": 0,
        "abuseScore": 0,
        "teenagerScore": 0,
        "adScore": 0,
        "suggestion": "Block",
        "label": "Porn",
        "subLabel": "PornHigh",
        "labelResults": [{
                "HitFlag": 0,
                "Scene": "Illegal",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 1,
                "Scene": "Porn",
                "Suggestion": "Block",
                "Label": "Porn",
                "SubLabel": "PornHigh",
                "Score": 99,
                "Details": [{
                        "Id": 0,
                        "Name": "PornHigh",
                        "Score": 99
                }, {
                        "Id": 1,
                        "Name": "WomenChest",
                        "Score": 99
                }]
        }, {
                "HitFlag": 0,
                "Scene": "Sexy",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "Terror",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }],
        "objectResults": [{
                "HitFlag": 0,
                "Scene": "QrCode",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "MapRecognition",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "PolityFace",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }],
        "ocrResults": [{
                "HitFlag": 0,
                "Scene": "OCR",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Text": "",
                "Details": []
        }],
        "streamId": "teststream",
        "channelId": "teststream",
        "stream_param": "txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
        "app": "5000.myqcloud.com",
        "appname": "live",
        "appid": 10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}

:::
</dx-codeblock>


## 라이브 방송 음란물 감지 비활성화

라이브 방송 음란물 감지는 화면 캡처 규칙을 삭제하거나 화면 캡처 템플릿을 수정해 비활성화할 수 있습니다. 삭제 또는 수정 작업은 새로운 라이브 방송에만 적용됩니다. 이미 시작된 라이브 방송에 적용 중인 음란물 감지 기능을 비활성화하려면 반드시 방송을 중지한 다음 다시 실행해야 합니다.

### 1. 음란물 감지 화면 캡처 규칙 삭제를 통한 방법

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)를 호출한 후 템플릿 ID에서 DomainName, AppName, StreamName의 해당 라이브 방송 화면 캡처 규칙을 삭제합니다.

### 2. 음란물 감지 화면 캡처 템플릿 삭제 또는 수정을 통한 방법

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)을 호출한 후에 라이브 방송 템플릿의 음란물 감지 태그를 0으로 수정합니다.
