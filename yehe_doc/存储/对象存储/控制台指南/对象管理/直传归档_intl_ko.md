## 소개
COS는 아카이브 다이렉트 업로드를 지원하며 곧바로 객체를 아카이브 유형으로 설정하여 COS에 업로드할 수 있습니다. 아카이브 다이렉트 업로드 방식은 콘솔, API, SDK, COSCMD 툴이 있습니다. 그 외에도 COS의 라이프사이클 기능을 통해 업로드된 객체를 CAS 유형이나 DEEP ARCHIVE 유형으로 전환할 수 있습니다.


## 아카이브 다이렉트 업로드 방법

- 콘솔 업로드
 [COS 콘솔](https://console.cloud.tencent.com/cos5)의 [파일 업로드]에서 업로드할 객체를 선택한 후 객체 속성 설정에서 스토리지 유형을 [CAS]나 [DEEP ARCHIVE]로 선택합니다. 자세한 내용은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)를 참조하십시오.
![](https://main.qcloudimg.com/raw/8f3b05d1407a9017c54c86c9cec693c7.png)

- API 업로드
PUT Object, POST Object, Initiate Multipart Upload 중에서 x-cos-storage-class를 ARCHIVE 혹은 DEEP_ARCHIVE으로 설정하여 아카이브 다이렉트 업로드를 합니다.
>!Append Object는 아카이브 다이렉트 업로드를 지원하지 않습니다.

- SDK 업로드
현재 COS에서 배포하는 모든 SDK는 아카이브 다이렉트 업로드를 지원합니다. 파일 업로드 시 StorageClass 매개변수를 ARCHIVE나 DEEP_ARCHIVE로 설정하여 아카이브 다이렉트 업로드를 구현할 수 있습니다.

- COSCMD 툴 업로드
COSCMD 툴은 아카이브 다이렉트 업로드를 지원합니다. 파일 업로드 시 헤더 필드 x-cos-storage-class를 추가하고 ARCHIVE나 DEEP_ARCHIVE로 설정하여 아카이브 다이렉트 업로드를 구현합니다.

#### 보관 복구 및 다운로드
CAS와 DEEP ARCHIVE 유형의 객체 다운로드는 표준 스토리지/표준IA 스토리지와 다르게 CAS 다운로드 전에 복구 작업(동결 해제)을 진행해야 합니다. 복구가 완료되면 다운로드가 가능하며 복구 작업은 아래 3가지 방식으로 할 수 있습니다.
- 고속 모드: 소요 시간이 가장 짧으며 일반적으로 데이터를 검색하는 데 1 - 5분 정도 소요됩니다.
- 표준 모드: 표준 모드를 사용하면 일반적으로 데이터를 검색하는 데 3 - 5시간 정도 소요됩니다.
- 일괄 모드: 비용이 가장 적게 들며 일반적으로 데이터를 검색하는 데 5 - 12시간 정도 소요됩니다.

>?DEEP ARCHIVE 유형 파일은 고속 모드의 복구 형식을 지원하지 않습니다. 표준 모드일 경우 복구하는 데 12 - 24시간 소요되며 일괄 모드일 경우 24 - 48시간 소요됩니다.

콘솔, API, SDK, COSCMD 툴은 CAS 복구와 다운로드를 모두 지원합니다.

#### 아카이브 다이렉트 업로드 제한 설명
- CAS와 DEEP ARCHIVE 유형의 객체를 다운로드할 때 먼저 복구를 진행한 후 다운로드해야 합니다.
- CAS와 DEEP ARCHIVE 유형의 객체를 복사할 때 먼저 복구를 진행하고 복사할 수 있습니다.
- CAS와 DEEP ARCHIVE 유형의 객체는 리전 간 복제를 지원하지 않습니다.
- CAS와 DEEP ARCHIVE 유형 객체는 표준 스토리지, 표준IA 스토리지와 같은 활발한 스토리지 유형으로 전환할 수 없습니다.

