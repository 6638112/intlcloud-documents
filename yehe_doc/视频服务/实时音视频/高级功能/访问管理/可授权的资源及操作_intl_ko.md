>!본 문서는 **Tencent Real-Time Communication(TRTC)** Cloud Access Management(CAM) 기능에 대한 내용을 소개하고 있으며 기타 제품의 액세스 관리 관련 내용은 [CAM의 제품 지원](https://intl.cloud.tencent.com/document/product/598/10588)을 참조하십시오..

CAM의 핵심 기능은 **계정이 특정 리소스에 대해 특정 작업을 수행하는 것을 허용하거나 금지하는 것**입니다. TRTC CAM은 [리소스 권한 부여](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)를 지원합니다. 리소스의 데이터 분할 정도는 [TRTC 애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714)이며, 작업 데이터 분할 정도는 [Cloud API](https://intl.cloud.tencent.com/product/api)로 [서버 API](https://intl.cloud.tencent.com/document/product/647/34260)와 TRTC 콘솔 액세스 시 사용할 수 있는 API를 포함합니다.

TRTC CAM이 필요한 경우 Tencent Cloud의 [루트 계정](https://intl.cloud.tencent.com/document/product/598/34899)에 로그인하여 [사전 설정 정책](https://intl.cloud.tencent.com/document/product/647/39550) 또는 [사용자 정의 정책](https://intl.cloud.tencent.com/document/product/647/39551)을 사용해 세부 권한 부여 작업을 완료하십시오.

## 권한을 부여할 수 있는 리소스 유형
CAM 권한을 부여할 수 있는 리소스 유형 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714).

<span id="Support"></span> 
## 리소스 권한 부여를 지원하는 API
일부 [리소스 권한 부여를 지원하지 않는 API](#n_Support)를 제외하고, 본 섹션에 나열된 모든 API 작업은 리소스 권한 부여를 지원합니다. 이러한 API 작업에 대한 [권한 부여 정책 구문](https://intl.cloud.tencent.com/document/product/647/39551#grammar)의 **리소스 구문 설명**은 동일하며 구체적인 내용은 다음과 같습니다.
- 전체 애플리케이션에 액세스 권한 부여: `qcs::trtc::uin/${uin}:sdkappid/*`.
- 개별 애플리케이션에 액세스 권한 부여: `qcs::trtc::uin/${uin}:sdkappid/${SdkAppId}`.

### 서버 API 작업
| 인터페이스 이름                                                               | 인터페이스 분류     | 기능 설명               |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | 방 관리     | 방 해체               |
| [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | 방 관리     | 사용자 삭제               |
| [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) | 혼합 스트림 트랜스 코딩     |클라우드 혼합 스트림 실행           |
| [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) | 혼합 스트림 트랜스 코딩     | 클라우드 혼합 스트림 종료       |
| [CreateTroubleInfo](https://intl.cloud.tencent.com/document/product/647/37764) | 통화 품질 모니터링 | 오류 정보 생성           |
| [DescribeAbnormalEvent](https://intl.cloud.tencent.com/document/product/647/37763) | 통화 품질 모니터링 | 오류 경험 이벤트 조회       |
| [DescribeCallDetail](https://intl.cloud.tencent.com/document/product/647/36759) | 통화 품질 모니터링 | 사용자 목록 및 통화 지표 조회 |
| [DescribeHistoryScale](https://intl.cloud.tencent.com/document/product/647/36758) | 통화 품질 모니터링 | 방 및 사용자 수 내역 조회   |
| [DescribeRealtimeNetwork](https://intl.cloud.tencent.com/document/product/647/36757) | 통화 품질 모니터링 | 실시간 네트워크 상태 조회       |
| [DescribeRealtimeQuality](https://intl.cloud.tencent.com/document/product/647/36756) | 통화 품질 모니터링 | 실시간 품질 데이터 조회       |
| [DescribeRealtimeScale](https://intl.cloud.tencent.com/document/product/647/36755) | 통화 품질 모니터링 | 실시간 규모 조회           |
| [DescribeRoomInformation](https://intl.cloud.tencent.com/document/product/647/36754) | 통화 품질 모니터링 | 방 리스트 조회           |



### 콘솔 API 작업
<table>
<thead><tr><th >인터페이스 이름</th><th>사용 모듈</th><th width="38%">기능 설명</th></tr></thead>
<tbody><tr>
<td>DescribeAppStatList</td>
<td>TRTC 콘솔<ul style="margin:0">
<li> <a href="https://console.cloud.tencent.com/trtc">개요</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">사용량 통계</a>
<li><a href="https://console.cloud.tencent.com/trtc/monitor">모니터링 대시보드</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리</a>
</ul></td>
<td>애플리케이션 리스트 가져오기</td>
</tr><tr>
<td>DescribeSdkAppInfo</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 애플리케이션 정보</a></td>
<td>애플리케이션 정보 가져오기</td>
</tr><tr>
<td>ModifyAppInfo</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 애플리케이션 정보</a></td>
<td>애플리케이션 정보 편집</td>
</tr><tr>
<td>ChangeSecretKeyFlag</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 애플리케이션 정보</a></td>
<td>권한 보안키 상태 수정</td>
</tr><tr>
<td>CreateWatermark</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 소재 관리</a></td>
<td>이미지 업로드</td>
</tr><tr>
<td>DeleteWatermark</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 소재 관리</a></td>
<td>이미지 삭제</td>
</tr><tr>
<td>ModifyWatermark</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 소재 관리</a></td>
<td>이미지 편집</td>
</tr><tr>
<td>DescribeWatermark</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 소재 관리</a></td>
<td>이미지 검색</td>
</tr><tr>
<td>CreateSecret</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 퀵 스타트</a></td>
<td>대칭 암호화 키 생성</td>
</tr><tr>
<td>ToggleSecretVersion</td>
<td>TRTC 콘솔<a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 퀵 스타트</a></td>
<td>보안키 버전 전환（퍼블릭키 프라이빗키/대칭 암호화 키）</td>
</tr><tr>
<td>DescribeSecret</td>
<td>TRTC 콘솔<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">개발 보조 &gt; 빠른 Demo 활성화</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a>
<li><a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 퀵 스타트</a>
</ul></td>
<td>대칭 암호화 키 가져오기</td>
</tr><tr>
<td>DescribeTrtcAppAndAccountInfo</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a></td>
<td>애플리케이션 및 계정 정보를 불러와 퍼블릭 키와 프라이빗 키 가져오기</td>
</tr><tr>
<td>CreateSecretUserSig</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a></td>
<td>대칭 암호화 키로 UserSig 생성</td>
</tr><tr>
<td>DescribeSig</td>
<td>TRTC 콘솔<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a>
<li> <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 퀵 스타트</a>
</ul></td>
<td>이전 버전의 퍼블릭키와 프라이빗키로 생성한 UserSig 가져오기</td>
</tr><tr>
<td>VerifySecretUserSig</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a></td>
<td>대칭 암호화 키로 생성한 UserSig 검증</td>
</tr><tr>
<td>VerifySig</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/usersigtool">개발 보조 &gt; UserSig 생성&amp;검증</a></td>
<td>퍼블릭키와 프라이빗키로 생성된 UserSig 검증</td>
</tr>
<tr>
<td>CreateSpearConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리  &gt;  화면 설정</a></td>
<td>화면 설정 사양 추가. 이 기능 설정 카드는 iLiveSDK 1.9.6 및 그 이전 버전에만 해댱됩니다. TRTC SDK 6.0 및 그 이후 버전은 <a href="https://intl.cloud.tencent.com/document/product/647/35153">화면 품질 설정</a>을 참조하시기 바랍니다. </td>
</tr>
<tr>
<td>DeleteSpearConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리  &gt; 화면 설정</a></td>
<td>화면 설정 사양 삭제. 이 기능 설정 카드는 iLiveSDK 1.9.6 및 그 이전 버전에만 해댱됩니다. TRTC SDK 6.0 및 그 이후 버전은 <a href="https://intl.cloud.tencent.com/document/product/647/35153">화면 품질 설정</a>을 참조하시기 바랍니다. </td>
</tr>
<tr>
<td>ModifySpearConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리  &gt;  화면 설정</a></td>
<td>화면 설정 사양 수정. 이 기능 설정 카드는 iLiveSDK 1.9.6 및 그 이전 버전에만 해댱됩니다. TRTC SDK 6.0 및 그 이후 버전은 <a href="https://intl.cloud.tencent.com/document/product/647/35153">화면 품질 설정</a>을 참조하시기 바랍니다. </td>
</tr>
<tr>
<td>DescribeSpearConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리  &gt;  화면 설정</a></td>
<td>화면 설정 사양 가져오기. 이 기능 설정 카드는 iLiveSDK 1.9.6 및 그 이전 버전에만 해댱됩니다. TRTC SDK 6.0 및 그 이후 버전은 <a href="https://intl.cloud.tencent.com/document/product/647/35153">화면 품질 설정</a>을 참조하시기 바랍니다. </td>
</tr>
<tr>
<td>ToggleSpearScheme</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리  &gt;  화면 설정</a></td>
<td>화면 설정 시나리오 전환. 이 기능 설정 카드는 iLiveSDK 1.9.6 및 그 이전 버전에만 해댱됩니다. TRTC SDK 6.0 및 그 이후 버전은 <a href="https://intl.cloud.tencent.com/document/product/647/35153">화면 품질 설정</a>을 참조하시기 바랍니다. </td>
</tr>
</tbody></table>

<span id="n_Support"></span> 
## 리소스 권한 부여를 지원하지 않는 API
특수한 제한으로 인하여 다음 API는 리소스 권한 부여를 지원하지 않습니다:

### 서버 API 작업
|인터페이스 이름|인터페이스 분류|기능 설명|특수 제한 설명|
|---|---|---|---|
|[DescribeDetailEvent](https://intl.cloud.tencent.com/document/product/647/37762)|통화 품질 모니터링|상세 이벤트 가져오기|매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. |

### 콘솔 API 작업
<table>
<thead><tr><th>인터페이스 이름</th><th width="20%">사용 모듈</th><th width="15%">기능 설명</th><th>특수 제한 설명</th></tr></thead>
<tbody><tr>
<td>DescribeTrtcStatistic</td>
<td>TRTC 콘솔<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc">개요</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">사용량 통계</a>
</ul></td>
<td>과금 기간 사용량 통계 데이터 가져오기</td>
<td>해당 인터페이스에는 SDKAppID 전체량을 반환하는 통계 데이터가 포함되어 있어 비 전체량 SDKAppID가 오류를 반환하는 것을 제한합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>GetUserList</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/monitor">모니터링 대시보드</a></td>
<td>사용자 목록 가져오기</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>GetUserInfo</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/monitor">모니터링 대시보드</a></td>
<td>사용자 정보 가져오기</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>GetCommState</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/monitor">모니터링 대시보드</a></td>
<td>통화 상태 가져오기</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>GetElasticSearchData</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/monitor">모니터링 대시보드</a></td>
<td>ES 데이터 조회</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>CreateTrtcApp</td>
<td>TRTC 콘솔 <ul>
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">개발 보조 &gt; 빠른 Demo 활성화</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리</a>
</ul></td>
<td>TRTC 애플리케이션 생성</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. SDKAppID는 TRTC 애플리케이션의 유일한 식별자로, 애플리케이션이 생성되어야 SDKAppID가 발급됩니다. </td>
</tr>
<tr>
<td>HardDescribeMixConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 기능 설정</a></td>
<td>자동 릴레이 푸시 스트림 상태 조회</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
<tr>
<td>ModifyMixConf</td>
<td>TRTC 콘솔 <a href="https://console.cloud.tencent.com/trtc/app">애플리케이션 관리 &gt; 기능 설정</a></td>
<td>자동 릴레이 푸시 스트림 시작/종료</td>
<td>매개변수를 입력했으나 SDKAppID가 존재하지 않아, 리소스 권한 부여가 불가능합니다. 필요한 경우 DescribeAppStatList 인터페이스를 통해 조회 가능한 애플리케이션 리스트를 제한할 수 있습니다. </td>
</tr>
</tbody></table>

>! 리소스 권한 부여를 지원하지 않는 API 작업에 대해서도 [사용자 정의 정책](https://intl.cloud.tencent.com/document/product/647/39551)을 톨해 사용자에게 해당 작업의 사용 권한을 부여할 수 있으나, 반드시 정책 문구의 리소스 요소에 `*`를 지정해야 합니다.
