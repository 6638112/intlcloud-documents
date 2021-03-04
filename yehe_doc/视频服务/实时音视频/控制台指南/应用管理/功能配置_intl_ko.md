애플리케이션 생성 완료 후 [Function Configuration]에서 현재 애플리케이션의 [릴레이 푸시 스트림](#bypass), [클라우드 녹화](#record), [고급 권한 제어](#purview) 기능을 활성화할 수 있으며 페이지에서 기능 설정을 모두 진행한 후 적용하는데 약 5분의 시간이 소요됩니다.

[](id:bypass)
## 릴레이 푸시 스트림 설정

### 주의사항

- UDP 전송 프로토콜을 기반으로 한 TRTC 서비스로, 프로토콜 전환을 통해 멀티미디어 스트림을 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 시스템으로 연결하며, 해당 프로세스를 “릴레이 푸시 스트림”이라고 합니다.
- 릴레이 푸시 스트림 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 LVB 서비스를 활성화해야 합니다.
- 릴레이 푸시 스트림은 [CDN 라이브 방송 보기](https://intl.cloud.tencent.com/document/product/647/35242) 시 LVB에서 라이브 방송 보기에 따라 발생하는 다운스트림 트래픽/대역폭 관련 요금을 부과하는데 사용되며, 자세한 내용은 [LVB>트래픽/대역폭 과금](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) 설명을 참조하십시오.
- 릴레이 푸시 스트림은 [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 시 발생하는 녹화 및 녹화 파일 저장 등의 비용 부과에 사용되며, 자세한 내용은 [클라우드 녹화 및 재생>관련 요금](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 설명을 참조하십시오.
- [LVB 콘솔](https://console.cloud.tencent.com/live/domainmanage)에서 릴레이 푸시 스트림에 사용하는 푸시 스트림 도메인(`xxxx.livepush.myqcloud.com`)에 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등의 유료 기능을 바인딩한 경우, 릴레이 푸시 스트림 시 템플릿에 해당하는 [부가 요금](https://intl.cloud.tencent.com/zh/document/product/267/2819#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B4.B9.E7.94.A8)이 발생합니다.

[](id:open_bypass)
### 릴레이 푸시 스트림 기능 활성화
1. TRTC 콘솔에 접속하여 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 선택합니다.
2. 기능 설정 수정이 필요한 애플리케이션을 선택하고 타깃 애플리케이션의 [기능 설정]을 클릭합니다.
 ![](https://main.qcloudimg.com/raw/e5b5b5494f2c75a7ea7a48caae32f256.png)
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화]버튼을 우측으로 클릭 설정합니다.
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
4. 팝업된 [릴레이 푸시 스트림 기능 활성화] 창에서 **리스크 설명을 잘 읽어주시고**, [릴레이 푸시 스트림 기능 활성화]를 클릭하면 활성화가 완료됩니다.
![](https://main.qcloudimg.com/raw/d39ff108d2f200cc92a78b42359bff6e.png)

[](id:select)
### 릴레이 푸시 스트림 방식 선택
[릴레이 푸시 스트림 기능 활성화](#open_bypass) 후 실제 비즈니스 상황에 따라 릴레이할 푸시 스트림 방식을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/3fd6fbe8c5837a6d7f78a19f079b477a.png)

- **지정 스트림 릴레이**: “지정 스트림 릴레이”를 선택한 후 혼합 스트림 트랜스 코딩이 필요 없는 경우, 클라이언트 SDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) 인터페이스를 호출하여 직접 릴레이 푸시 스트림을 실행할 수 있습니다. 혼합 스트림 트랜스 코딩이 필요한 경우에는 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) 문서 가이드에 따라 진행하면 혼합 스트림 트랜스 코딩 후 자동으로 푸시 스트림을 릴레이 합니다.
- **전역 자동 릴레이** “전역 자동 릴레이”를 선택한 후 TRTC의 모든 업스트림 멀티미디어 스트림은 자동으로 LVB 시스템에 릴레이 푸시 스트림 됩니다.


[](id:close__bypass)
### 릴레이 푸시 스트림 기능 비활성화
릴레이 푸시 스트림 기능 비활성화 작업 순서의 자세한 내용은 아래와 같습니다.
1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화]버튼을 우측으로 클릭 설정합니다.
![](https://main.qcloudimg.com/raw/0ac618f3fb643a3d5fd1ff11566eef31.png)
4. [릴레이 푸시 스트림 기능 비활성화]팝업창에 보이는 **리스크 설명을 자세히 읽습니다.** 비활성화를 하려면 [릴레이 푸시 스트림 기능 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/1306f736ff0b5337f468325cabdfee54.png)


[](id:record)
## 클라우드 녹화 설정

### 주의사항
- TRTC 서비스는 릴레이 푸시 스트림 방식으로 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 기능을 이용해 전체 과정을 녹화할 수 있으며, 녹화한 파일은 [VOD](https://intl.cloud.tencent.com/zh/document/product/266)에 저장됩니다.
- 녹화 기능은 LVB 서비스를 이용하여 LVB의 라이브 방송 녹화 요금이 발생하며, 당월 라이브 방송 녹화 동시 피크 채널 수를 청구 기준으로 합니다. 자세한 과금 규정은 [LVB>라이브 방송 녹화 요금 설명](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)을 참조하십시오.
- 녹화 후 파일은 VOD 플랫폼에 저장되며, VOD 스토리지 요금이 발생합니다. VOD 플랫폼 스토리지 용량에 따라 과금되며, 자세한 과금 규정은 [VOD>비디오 스토리지(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 녹화한 비디오 파일을 재생 또는 다운로드하는 경우 VOD 서비스의 트래픽(비디오 가속) 비용이 발생하며, 다운스트림 가속 트래픽에 따라 과금됩니다. 자세한 과금 규정은 [VOD>비디오 가속(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 처음에는 클라우드 녹화 기능이 비활성화 상태이므로 클라우드 녹화 기능을 사용하려면 먼저 LVB와 VOD 서비스를 활성화해야 합니다.
- 클라우드 녹화는 릴레이 푸시 스트림에 종속되므로, 먼저 [릴레이 푸시 스트림](#open_bypass)을 활성화해야 합니다.


[](id:open_record)
### 클라우드 녹화 기능 활성화
TRTC의 클라우드 녹화는 각 방마다 사용자별 멀티미디어 스트리밍을 독립 파일로 녹화할 수 있습니다. 클라우드 녹화 기능 활성화의 자세한 작업 가이드는 [클라우드 녹화 실행 및 다시보기](https://intl.cloud.tencent.com/document/product/647/35426#open)를 참고하십시오.

[](id:change_record)
### 클라우드 녹화 설정 수정
>! 클라우드 녹화 설정을 수정하는 경우 현재 온라인에서 실행되고 있는 서비스 데이터에 영향이 미칠 수 있습니다. 리스크를 확인한 후 신중하게 수정하시기 바랍니다.

1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)에서 클라우드 녹화 설정 수정이 필요한 애플리케이션을 선택해 타깃 애플리케이션에서 수행하는 [기능 설정]을 클릭합니다.
3. [기능 설정]>[클라우드 녹화 활성화]에서 오른쪽에 있는 [편집]을 클릭하여 클라우드 녹화 설정 수정 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/1e0ac1e9704a5901466ad6ec3ccac89b.png)
4. 실제 상황에 따라 [설정 정보](https://intl.cloud.tencent.com/document/product/647/35426#recordType)를 수정하고 [확인]을 누르면 수정 사항이 저장됩니다.


[](id:close_record)
### 클라우드 녹화 기능 비활성화
클라우드 녹화 비활성화를 진행한 후 현재 온라인에서 실행하는 비즈니스에서 모바일 녹화 및 자동 녹화와 같은 클라우드 녹화를 진행할 수 없습니다. 비즈니스에서 클라우드 녹화가 필요 없는지 확인한 후 비활성화를 진행하십시오.

1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정]>[클라우드 녹화 설정]에서 [클라우드 녹화 활성화]오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/93761fae36103906ddbd4e134460be0a.png)
3. 비활성화 진행 후의 영향에 대해 자세히 읽습니다. 클라우드 녹화 비활성화를 하려면 [클라우드 녹화 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/3202cb938030085babc0210283ce9221.png)



[](id:purview)
## 고급 권한 제어
입장 혹은 마이크 켜짐 권한을 제한하고 싶은 경우 지정 사용자만 입장하고 마이크를 켤 수 있도록 허용할 수 있습니다. 클라이언트 권한에 대한 크래킹 공격이 걱정되는 경우 [고급 권한 제어 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 고려해볼 수 있습니다.
![](https://main.qcloudimg.com/raw/8fd4b0d09aeea46a15714c59e5e0419e.png)


### 주의사항
고급 권한 제어를 활성화한 후 SDKAppID를 사용하는 모든 계정은 TRTCParams에서 privateMapKey 매개변수를 정확히 전송받아야만 입장할 수 있습니다. 온라인에서 해당 SDKAppID를 사용하는 계정은 이 기능을 함부로 활성화하지 마십시오.


### 고급 권한 제어 활성화
1. [애플리케이션 관리] 클릭하여 고급 권한 제어를 활성화할 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정>[고급 권한 제어 기능]에서 [고급 권한 제어 기능 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/196e32293f8f5c159a3513cbf4b9723a.png)

### 고급 권한 제어 비활성화
1. [애플리케이션 관리]를 클릭하여 고급 권한 제어 비활성화가 필요한 애플리케이션을 선택하고 타깃 애플리케이션에서 수행하는 [기능 설정]을 클릭합니다.
2. [기능 설정]>[고급 권한 제어]에서 [고급 권한 제어 비활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/b7015cb446cd022d591fda7e22689e44.png)

## 관련 문서
- 새로운 애플리케이션 생성이 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 생성](https://intl.cloud.tencent.com/zh/document/product/647/39077)을 참고하십시오.
- 애플리케이션 리스트에서 관련 애플리케이션 검색이 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 검색](https://intl.cloud.tencent.com/zh/document/product/647/39078)을 참고하십시오.
- 애플리케이션 기본 정보 조회가 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 정보](https://intl.cloud.tencent.com/zh/document/product/647/39079)를 참고하십시오.
- 클라우드 혼합 스트림 트랜스 코딩이 필요한 경우 사용자 정의 배경 이미지 설정은 소재 관리에서 대응하는 이미지 소재를 추가할 수 있습니다. 작업에 대한 자세한 내용은 [소재 관리](https://intl.cloud.tencent.com/zh/document/product/647/39081)를 참고하십시오.
- 애플리케이션으로 Demo 소스 코드를 얻어 빠른 시작을 해야 할 경우 작업에 대한 자세한 내용은 [빠른 시작](https://intl.cloud.tencent.com/zh/document/product/647/39082)을 참고하십시오.





애플리케이션 생성 완료 후 [Function Configuration]에서 현재 애플리케이션의 [릴레이 푸시 스트림](#bypass), [클라우드 녹화](#record), [고급 권한 제어](#purview) 기능을 활성화할 수 있으며 페이지에서 기능 설정을 모두 진행한 후 적용하는데 약 5분의 시간이 소요됩니다.

[](id:bypass)
## 릴레이 푸시 스트림 설정

### 주의사항

- UDP 전송 프로토콜을 기반으로 한 TRTC 서비스로, 프로토콜 전환을 통해 멀티미디어 스트림을 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 시스템으로 연결하며, 해당 프로세스를 “릴레이 푸시 스트림”이라고 합니다.
- 릴레이 푸시 스트림 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 LVB 서비스를 활성화해야 합니다.
- 릴레이 푸시 스트림은 [CDN 라이브 방송 보기](https://intl.cloud.tencent.com/document/product/647/35242) 시 LVB에서 라이브 방송 보기에 따라 발생하는 다운스트림 트래픽/대역폭 관련 요금을 부과하는데 사용되며, 자세한 내용은 [LVB>트래픽/대역폭 과금](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) 설명을 참조하십시오.
- 릴레이 푸시 스트림은 [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 시 발생하는 녹화 및 녹화 파일 저장 등의 비용 부과에 사용되며, 자세한 내용은 [클라우드 녹화 및 재생>관련 요금](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 설명을 참조하십시오.
- [LVB 콘솔](https://console.cloud.tencent.com/live/domainmanage)에서 릴레이 푸시 스트림에 사용하는 푸시 스트림 도메인(`xxxx.livepush.myqcloud.com`)에 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등의 유료 기능을 바인딩한 경우, 릴레이 푸시 스트림 시 템플릿에 해당하는 [부가 요금](https://intl.cloud.tencent.com/zh/document/product/267/2819#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B4.B9.E7.94.A8)이 발생합니다.

[](id:open_bypass)
### 릴레이 푸시 스트림 기능 활성화
1. TRTC 콘솔에 접속하여 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 선택합니다.
2. 기능 설정 수정이 필요한 애플리케이션을 선택하고 타깃 애플리케이션의 [기능 설정]을 클릭합니다.
 ![](https://main.qcloudimg.com/raw/e5b5b5494f2c75a7ea7a48caae32f256.png)
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화]버튼을 우측으로 클릭 설정합니다.
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
4. 팝업된 [릴레이 푸시 스트림 기능 활성화] 창에서 **리스크 설명을 잘 읽어주시고**, [릴레이 푸시 스트림 기능 활성화]를 클릭하면 활성화가 완료됩니다.
![](https://main.qcloudimg.com/raw/d39ff108d2f200cc92a78b42359bff6e.png)

[](id:select)
### 릴레이 푸시 스트림 방식 선택
[릴레이 푸시 스트림 기능 활성화](#open_bypass) 후 실제 비즈니스 상황에 따라 릴레이할 푸시 스트림 방식을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/3fd6fbe8c5837a6d7f78a19f079b477a.png)

- **지정 스트림 릴레이**: “지정 스트림 릴레이”를 선택한 후 혼합 스트림 트랜스 코딩이 필요 없는 경우, 클라이언트 SDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) 인터페이스를 호출하여 직접 릴레이 푸시 스트림을 실행할 수 있습니다. 혼합 스트림 트랜스 코딩이 필요한 경우에는 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) 문서 가이드에 따라 진행하면 혼합 스트림 트랜스 코딩 후 자동으로 푸시 스트림을 릴레이 합니다.
- **전역 자동 릴레이** “전역 자동 릴레이”를 선택한 후 TRTC의 모든 업스트림 멀티미디어 스트림은 자동으로 LVB 시스템에 릴레이 푸시 스트림 됩니다.


[](id:close__bypass)
### 릴레이 푸시 스트림 기능 비활성화
릴레이 푸시 스트림 기능 비활성화 작업 순서의 자세한 내용은 아래와 같습니다.
1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화]버튼을 우측으로 클릭 설정합니다.
![](https://main.qcloudimg.com/raw/0ac618f3fb643a3d5fd1ff11566eef31.png)
4. [릴레이 푸시 스트림 기능 비활성화]팝업창에 보이는 **리스크 설명을 자세히 읽습니다.** 비활성화를 하려면 [릴레이 푸시 스트림 기능 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/1306f736ff0b5337f468325cabdfee54.png)


[](id:record)
## 클라우드 녹화 설정

### 주의사항
- TRTC 서비스는 릴레이 푸시 스트림 방식으로 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 기능을 이용해 전체 과정을 녹화할 수 있으며, 녹화한 파일은 [VOD](https://intl.cloud.tencent.com/zh/document/product/266)에 저장됩니다.
- 녹화 기능은 LVB 서비스를 이용하여 LVB의 라이브 방송 녹화 요금이 발생하며, 당월 라이브 방송 녹화 동시 피크 채널 수를 청구 기준으로 합니다. 자세한 과금 규정은 [LVB>라이브 방송 녹화 요금 설명](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)을 참조하십시오.
- 녹화 후 파일은 VOD 플랫폼에 저장되며, VOD 스토리지 요금이 발생합니다. VOD 플랫폼 스토리지 용량에 따라 과금되며, 자세한 과금 규정은 [VOD>비디오 스토리지(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 녹화한 비디오 파일을 재생 또는 다운로드하는 경우 VOD 서비스의 트래픽(비디오 가속) 비용이 발생하며, 다운스트림 가속 트래픽에 따라 과금됩니다. 자세한 과금 규정은 [VOD>비디오 가속(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 처음에는 클라우드 녹화 기능이 비활성화 상태이므로 클라우드 녹화 기능을 사용하려면 먼저 LVB와 VOD 서비스를 활성화해야 합니다.
- 클라우드 녹화는 릴레이 푸시 스트림에 종속되므로, 먼저 [릴레이 푸시 스트림](#open_bypass)을 활성화해야 합니다.


[](id:open_record)
### 클라우드 녹화 기능 활성화
TRTC의 클라우드 녹화는 각 방마다 사용자별 멀티미디어 스트리밍을 독립 파일로 녹화할 수 있습니다. 클라우드 녹화 기능 활성화의 자세한 작업 가이드는 [클라우드 녹화 실행 및 다시보기](https://intl.cloud.tencent.com/document/product/647/35426#open)를 참고하십시오.

[](id:change_record)
### 클라우드 녹화 설정 수정
>! 클라우드 녹화 설정을 수정하는 경우 현재 온라인에서 실행되고 있는 서비스 데이터에 영향이 미칠 수 있습니다. 리스크를 확인한 후 신중하게 수정하시기 바랍니다.

1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)에서 클라우드 녹화 설정 수정이 필요한 애플리케이션을 선택해 타깃 애플리케이션에서 수행하는 [기능 설정]을 클릭합니다.
3. [기능 설정]>[클라우드 녹화 활성화]에서 오른쪽에 있는 [편집]을 클릭하여 클라우드 녹화 설정 수정 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/1e0ac1e9704a5901466ad6ec3ccac89b.png)
4. 실제 상황에 따라 [설정 정보](https://intl.cloud.tencent.com/document/product/647/35426#recordType)를 수정하고 [확인]을 누르면 수정 사항이 저장됩니다.


[](id:close_record)
### 클라우드 녹화 기능 비활성화
클라우드 녹화 비활성화를 진행한 후 현재 온라인에서 실행하는 비즈니스에서 모바일 녹화 및 자동 녹화와 같은 클라우드 녹화를 진행할 수 없습니다. 비즈니스에서 클라우드 녹화가 필요 없는지 확인한 후 비활성화를 진행하십시오.

1. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정]>[클라우드 녹화 설정]에서 [클라우드 녹화 활성화]오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/93761fae36103906ddbd4e134460be0a.png)
3. 비활성화 진행 후의 영향에 대해 자세히 읽습니다. 클라우드 녹화 비활성화를 하려면 [클라우드 녹화 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/3202cb938030085babc0210283ce9221.png)



[](id:purview)
## 고급 권한 제어
입장 혹은 마이크 켜짐 권한을 제한하고 싶은 경우 지정 사용자만 입장하고 마이크를 켤 수 있도록 허용할 수 있습니다. 클라이언트 권한에 대한 크래킹 공격이 걱정되는 경우 [고급 권한 제어 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 고려해볼 수 있습니다.
![](https://main.qcloudimg.com/raw/8fd4b0d09aeea46a15714c59e5e0419e.png)


### 주의사항
고급 권한 제어를 활성화한 후 SDKAppID를 사용하는 모든 계정은 TRTCParams에서 privateMapKey 매개변수를 정확히 전송받아야만 입장할 수 있습니다. 온라인에서 해당 SDKAppID를 사용하는 계정은 이 기능을 함부로 활성화하지 마십시오.


### 고급 권한 제어 활성화
1. [애플리케이션 관리] 클릭하여 고급 권한 제어를 활성화할 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정>[고급 권한 제어 기능]에서 [고급 권한 제어 기능 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/196e32293f8f5c159a3513cbf4b9723a.png)

### 고급 권한 제어 비활성화
1. [애플리케이션 관리]를 클릭하여 고급 권한 제어 비활성화가 필요한 애플리케이션을 선택하고 타깃 애플리케이션에서 수행하는 [기능 설정]을 클릭합니다.
2. [기능 설정]>[고급 권한 제어]에서 [고급 권한 제어 비활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/b7015cb446cd022d591fda7e22689e44.png)

## 관련 문서
- 새로운 애플리케이션 생성이 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 생성](https://intl.cloud.tencent.com/zh/document/product/647/39077)을 참고하십시오.
- 애플리케이션 리스트에서 관련 애플리케이션 검색이 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 검색](https://intl.cloud.tencent.com/zh/document/product/647/39078)을 참고하십시오.
- 애플리케이션 기본 정보 조회가 필요한 경우 작업에 대한 자세한 내용은 [애플리케이션 정보](https://intl.cloud.tencent.com/zh/document/product/647/39079)를 참고하십시오.
- 클라우드 혼합 스트림 트랜스 코딩이 필요한 경우 사용자 정의 배경 이미지 설정은 소재 관리에서 대응하는 이미지 소재를 추가할 수 있습니다. 작업에 대한 자세한 내용은 [소재 관리](https://intl.cloud.tencent.com/zh/document/product/647/39081)를 참고하십시오.
- 애플리케이션으로 Demo 소스 코드를 얻어 빠른 시작을 해야 할 경우 작업에 대한 자세한 내용은 [빠른 시작](https://intl.cloud.tencent.com/zh/document/product/647/39082)을 참고하십시오.





