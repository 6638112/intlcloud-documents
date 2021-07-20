빠른 영상 통화 기능이 필요한 경우, Tencent Cloud가 제공하는 Demo를 기반으로 설정을 적절하게 수정하거나 TRTCCalling 모듈을 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

## Demo UI 인터페이스 재사용

### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인한 후 [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예시: `TestVideoCall`)을 입력한 후 [생성]을 클릭합니다.

>!본 기능은 기본 PaaS 서비스인 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/zh/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. 인스턴트 메시지 IM은 부가 서비스이며, 자세한 과금 규정은 [인스턴트 메시지 IM 요금 가이드](https://intl.cloud.tencent.com/document/product/1047/34350)를 참조하십시오.

[](id:ui.step2)

### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 들어가서 다운로드한 소스 패키지에 적합한 개발 환경을 선택합니다.
2. `/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.dart` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.
>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 귀하의 App이 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

[](id:ui.step4)

### 4단계: Demo 실행

>! Android는 실제 기기에서 실행해야 하며, 시뮬레이터 디버깅을 지원하지 않습니다.

1. `flutter pub get`을 실행합니다.
2. 컴파일 실행 디버깅:
<dx-tabs>
:::  Android\s
1. `flutter run`을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 열고 [실행]을 클릭합니다.
:::
::: iOS\s
1. XCode(11.0 버전 이상)를 사용해 소스 코드 디렉터리에 있는 `/ios 프로그램`을 엽니다.
2. Demo 프로그램을 컴파일 및 실행합니다.
:::
</dx-tabs>

[](id:ui.step5)
### 5단계: Demo 소스 코드 수정
[소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)폴더 `TRTCCallingDemo`에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, ui 폴더는 모두 인터페이스 코드입니다.

| 파일 또는 폴더            | 기능 설명                                                     |
| ----------------------- | ------------------------------------------------------------ |
| TRTCCallingVideo.dart   | 멀티미디어 통화의 메인 인터페이스입니다. 통화를 수신하거나 거절합니다. |
| TRTCCallingContact.dart | 대화 상대 선택 시 사용되는 인터페이스입니다. 등록된 사용자를 검색하고 통화를 요청할 수 있습니다. |

[](id:model)

## 사용자 정의 UI 인터페이스 구현
[소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)폴더 `TRTCCallingDemo`에는 두 개의 하위 폴더 ui와 model이 있으며, model 폴더에는 Tencent Cloud가 구현한 재사용 가능 오픈 소스 모듈 TRTCCalling이 포함되어 있습니다. `TRTCCalling.dart` 파일에서 해당 모듈이 제공하는 인터페이스 함수를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/36220937e8689dac4499ce9f2f187889.png)

오픈 소스 모듈 TRTCCalling을 사용해 맞춤형 UI 인터페이스를 구현할 수 있습니다. 즉, model 부분만 재사용하여 UI 부분을 자체적으로 구현할 수 있습니다.

[](id:model.step1)
### 1단계: SDK 통합
멀티미디어 통화 모듈 TRTCCalling는 [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)와 [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)에 종속되며, `pubspec.yaml` 설정을 통해 자동으로 다운로드 및 업데이트할 수 있습니다.

프로젝트의 `pubspec.yaml`에 다음과 같이 종속성을 입력합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
  tencent_im_sdk_plugin: 최신 버전 넘버
```

[](id:model.step2)

### 2단계: 권한 및 난독화 규칙 설정

<dx-tabs>
::: iOS\s
`Info.plist`에 카메라와 마이크에 대한 권한 신청을 추가해야 합니다.
```
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화를 진행할 수 있습니다.</string>
```

:::  Android\s

1. `/android/app/src/main/AndroidManifest.xml` 파일을 엽니다.
2. `xmlns:tools="http://schemas.android.com/tools"`를 manifest에 추가합니다.
3. `tools:replace="android:label"`을 application에 추가합니다.
>? 이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/document/product/647/39242) 문제가 발생합니다.

:::
</dx-tabs>

[](id:model.step3)

### 3단계: TRTCCalling 모듈 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
```
/lib/TRTCCallingDemo/model
```

[](id:model.step4)

### 4단계: 모듈 초기화 및 로그인
1. `TRTCCalling.sharedInstance()`를 호출해 모듈 인스턴스를 획득합니다.
2. `login(SDKAppID, userId, userSig)`을 호출해 모듈에 로그인합니다. 주요 매개변수는 다음 테이블을 참조하십시오.
 <table>
<tr><th>매개변수 이름</th><th>역할</th></tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://intl.cloud.tencent.com/login">TRTC 콘솔</a>에서 SDKAppID를 조회할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자의 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 계산 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr></table>
<dx-codeblock>
::: java 
// 초기화
sCall = await TRTCCalling.sharedInstance();
sCall.login(1400000123, "userA", "xxxx");
:::
</dx-codeblock>

[](id:model.step5)
### 5단계: 일대일 영상 통화 구현
1. 발신자: `TRTCCalling`의 `call()`을 호출하여 통화를 요청하고, 사용자 ID(userid)와 통화 유형(Type)을 전송합니다. 통화 유형 매개변수는 `TRTCCalling.typeVideoCall`입니다.
2. 수신자: 수신자가 로그인 상태인 경우 `onInvited()`라는 이벤트 공지를 받게 됩니다. 콜백의 `callType` 매개변수는 발신자가 입력한 통화 유형으로, 이 매개변수를 통해 해당하는 인터페이스를 실행할 수 있습니다. 
3. 수신자: 통화 수신을 원하는 경우 수신자는 `accept()` 함수를 호출할 수 있으며, 동시에 `openCamera()` 함수를 호출하여 자신의 로컬 카메라를 활성화할 수 있습니다. 또한 `reject()`를 호출하여 통화를 거절할 수도 있습니다.
4. 멀티미디어 터널이 구축되면 양측은 `onUserVideoAvailable()`이라는 이벤트 공지를 받게 되며, 상대의 비디오 화면을 받았다는 의미입니다. 이때 양측의 사용자 모두 `startRemoteView()`를 호출하여 원격 비디오 화면을 볼 수 있습니다. 원격 음성의 기본값은 자동 재생입니다.

[](id:model.offline)
### 6단계: 오프라인 통화 구현
현재 오프라인 통화를 지원하지 않으며, 6월부터 지원할 예정입니다.

[](id:api)
## 모듈 API 리스트
TRTCCalling 모듈의 API 인터페이스 리스트는 다음과 같습니다.

| 인터페이스 함수           | 인터페이스 기능                                                  |
| ------------------ | --------------------------------------------------------- |
| registerListener   | TRTCCalling 리스너를 추가하면 사용자는 해당 리스너를 통해 상태 공지를 받을 수 있습니다. |
| unRegisterListener | 리스너 제거                                                |
| destroy            | 인스턴스 폐기                                                  |
| login              | IM에 로그인합니다. 모든 기능은 먼저 로그인한 후 사용할 수 있습니다.                 |
| logout             | IM에서 로그아웃합니다. 로그아웃 후에는 발신 기능을 사용할 수 없습니다.                         |
| call               | C2C 통화에 초대합니다. 초대받은 사람은 onInvited 이벤트 공지를 받게 됩니다.         |
| accept             | 초대된 사용자 통화 수신                                      |
| reject             | 초대된 사용자 통화 거절                                      |
| hangup             | 통화 종료                                                  |
| startRemoteView    | 원격 사용자의 카메라 데이터를 지정한 TXCloudVideoView로 렌더링합니다.    |
| stopRemoteView     | 특정 원격 사용자의 카메라 데이터 렌더링을 중지합니다.                          |
| openCamera         | 카메라를 활성화하고 지정한 TXCloudVideoView로 렌더링합니다.            |
| closeCamera        | 카메라 비활성화                                                |
| switchCamera       | 전면/후면 카메라 전환                                            |
| setMicMute         | mic 음소거 여부                                              |
| setHandsFree       | 핸즈프리 활성화 여부                                              |

