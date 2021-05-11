## 작업 시나리오
도메인 푸시 스트리밍 완료 후, CSS 콘솔로 이동해 재생 주소 생성기를 이용하여 푸시 스트리밍 주소의 StreamName과 동일한 StreamName을 입력하고 해당 스트림의 재생 주소를 생성하면, 해당 재생 주소를 통해 라이브 방송 화면을 확인할 수 있습니다.

## 전제 조건
 - [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
 - **재생 도메인**이 추가되어 있어야 합니다. 자세한 내용은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하십시오.

## 작업 순서
1. [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 [관리]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [재생 설정]>[재생 주소 생성기]를 선택하여 다음과 같이 설정합니다.
	1. 만료 시간을 선택합니다. (예시: `2019-02-28 23:59:59`)
	2. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`) 재생 주소 StreamName과 푸시 스트리밍 주소 StreamName이 일치해야 해당 스트림을 재생할 수 있습니다.
	3. 설정되어 있는 트랜스 코딩 템플릿을 선택할 수 있습니다.
	3. [재생 주소 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/6118cad9cca141bcee5c54d8211a9567.png)
3. 재생 도메인의 재생 인증이 비활성화 상태인 경우, [재생 설정]>[재생 주소] 탭에서 해당 재생 도메인의 RTMP, FLV, HLS 세 가지 재생 주소를 확인할 수 있습니다. 재생 주소 상의 StreamName(스트림 이름)을 변경하여 푸시 스트리밍 주소와 연결하면 재생 주소로 라이브 방송 화면을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/eb03329524d2ccfc2470e27c1b2b8eef.png)

>?CSS 재생에 관한 자세한 내용은 [CSS 재생](https://intl.cloud.tencent.com/document/product/267/31559)을 참조하십시오.




## 재생 주소
### 1. 재생 주소 생성 규칙
```
RTMP 포맷: rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV 포맷: http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8 포맷: http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- domain: 외부 재생 도메인입니다.
- AppName: 라이브 방송 애플리케이션 이름으로, 기본값은 live이고 사용자 정의 가능합니다.
- StreamName: 스트림 이름으로, 사용자 정의가 가능하며 라이브 방송 스트림을 식별하는 데 사용됩니다.
- txSecret: 재생 인증을 활성화하면 생성되는 인증 문자열입니다.
- txTime: 재생 주소에 설정된 타임스탬프로, 콘솔 재생 주소의 유효 시간입니다.

>!
>- 도메인 인증을 활성화한 경우 실제 만료 시간은 txTime + 인증 유효시간입니다.
>- 콘솔에서는 사용 편의를 위해 설정하는 시간이 곧 실제 만료시간이 됩니다. 도메인 인증을 활성화한 경우 재생 주소 연산 시 공식에 따라 txTime을 역산출합니다.

### 2. 트랜스 코딩 후의 라이브 방송 주소
라이브 방송 도메인에 트랜스 코딩 템플릿을 설정하고 트랜스 코딩 후의 라이브 방송 스트림을 재생해야 하는 경우, 트랜스 코딩 재생 주소는 원본 재생 주소 상의 StreamName 뒤에 `_트랜스 코딩 템플릿 이름`을 추가하는 방식으로 조합됩니다.

예를 들어 원본 재생 주소가 `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`이고 연결된 트랜스 코딩 템플릿 이름이 `hd`인 경우, 트랜스 코딩 재생 주소는 `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`이 됩니다.

### 3. H.265 재생 주소
CSS는 H.265 인코딩을 통한 푸시 스트리밍 및 재생을 지원합니다. 라이브 방송 원본 스트림이 H.264를 통해 인코딩된 경우, 라이브 방송 트랜스 코딩 템플릿을 통해 H.265 라이브 방송 스트림으로 전환되어 재생될 수도 있습니다. 콘솔 트랜스 코딩에 관한 내용은 [라이브 방송 콘솔 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/31561)을, API 트랜스 코딩에 관한 내용은 [라이브 방송 트랜스 코딩 API](https://intl.cloud.tencent.com/document/product/267/31561)를 참조하십시오.
