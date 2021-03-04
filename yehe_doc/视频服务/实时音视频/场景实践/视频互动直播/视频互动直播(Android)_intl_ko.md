## 효과
Tencent Cloud의 Demo를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 대화형 라이브 방송 기능을 체험해볼 수 있습니다. Demo에는 인터랙션 마이크 연결, 호스트 PK, 저딜레이 시청, 댓글 자막 채팅 등 대화형 라이브 방송 시나리오에서의 TRTC 관련 기능이 포함되어 있습니다.

신속한 비디오 대화형 라이브 방송 기능이 필요할 경우, Tencent Cloud의 Demo를 기반으로 직접 수정 및 모델링을 진행하거나 TRTCLiveRoom 모듈을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

<span id="DemoUI"> </span>
## Demo UI 인터페이스 재사용




<span id="ui.step1"></span>
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인하여 [개발 보조]>[빠른 Demo 활성화](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestLiveRoom`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>?해당 기능은 Tencent Cloud의 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [IM](https://intl.cloud.tencent.com/document/product/1047) 두 가지 서비스 기반의 PAAS 서비스를 이용합니다. TRTC가 활성화되면 인스턴트 메시징 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오.

<span id="ui.step2"></span>
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 커서를 해당하는 부분으로 이동한 후, [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)를 클릭하여 Github(또는 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip) 클릭)로 이동하여 SDK와 Demo 소스 코드를 다운로드합니다.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

<span id="ui.step3"></span>
### 3단계: Demo 프로젝트 파일 설정
1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
 3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 방법입니다. 여기에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 귀하의 App이 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

<span id="ui.step4"></span>
### 4단계: Demo 실행
Android Studio(3.5 버전 이상)를 사용하여 오픈 소스 프로그램인 `TRTCScenesDemo`를 열고 [실행]을 클릭하면 해당 Demo가 디버깅됩니다.

<span id="ui.step5"></span>
### 5단계: Demo 소스 코드 수정
소스 코드 trtcliveroomdemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 관련 코드입니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| anchor | 호스트 관련 UI 구현 코드 |
| audience | 시청자 관련 UI 구현 코드 |
| common | 범용 UI 모듈 구현 코드 |
| liveroomlist | 방 리스트 페이지 구현 코드 |
| widget | 범용 컨트롤러 |

<span id="model"> </span>
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcliveroomdemo/src/main/java/com/tencent/liteav/liveroom)의 trtcliveroomdemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 모듈인 TRTCLiveRoom이 포함되어 있습니다. `TRTCLiveRoom.java` 파일에서 해당 모듈에서 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

<span id="model.step1"> </span>
### 1단계: SDK 통합
영상 통화 모듈인 TRTCLiveRoom은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: Maven 웨어하우스를 통한 종속 **
1. dependencies에 TRTCSDK와 IMSDK의 종속 패키지를 추가합니다.
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?해당 두 SDK의 최신 버전은 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK) Github 메인 페이지에서 다운로드할 수 있습니다.
>
2. defaultConfig에서 앱이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3. [Sync Now]를 클릭하면 SDK가 자동으로 다운로드되고 프로그램에 통합됩니다.

**방법2: 로컬 AAR를 통한 종속**
maven 웨어하우스 연결이 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참조하여 프로젝트에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>통합 가이드</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">통합 가이드 문서</a></td>
</tr>
</table>

<span id="model.step2"> </span>
### 2단계: 권한 및 난독화 규칙 설정
AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한(6.0 이상의 Android 시스템의 경우 카메라 및 스토리지 읽기 동적 권한 신청 필요)이 필요합니다.
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

proguard-rules.pro 파일에서 SDK 관련 사항을 비난독화 리스트에 추가합니다.
```
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>
### 3단계: TRTCLiveRoom 모듈 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 붙여넣습니다.
```
src/main/java/com/tencent/liteav/liveroom/model
```

<span id="model.step4"> </span>
### 4단계: 모듈 생성 및 로그인
1. `sharedInstance` 인터페이스를 호출하여 TRTCLiveRoom 모듈의 인스턴스 객체를 생성합니다.
2. `TRTCLiveRoomConfig` 객체를 생성합니다. 해당 객체에서는 useCDNFirst와 CDNPlayDomain 속성을 설정할 수 있습니다.
 - useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자가 CDN을 통해 시청하도록 설정하며, 요금이 저렴하지만 딜레이가 비교적 많이 발생합니다. false는 일반 시청자가 저딜레이를 통해 시청하도록 설정하며, 요금이 CDN과 마이크 연결 요금의 중간 정도지만 딜레이가 1초 이내로 제어됩니다.
 - CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용됩니다. CDN을 통해 시청하는 재생 도메인을 지정하는 데 사용하며, 라이브 방송 콘솔에 로그인하여 [도메인 관리](https://console.cloud.tencent.com/live/domainmanage) 페이지에서 설정할 수 있습니다.
3. `login` 함수를 호출해 모듈에 로그인하고, 다음 표를 참고하여 관련 매개변수를 입력합니다.
 <table>
<tr>
<th>매개변수 이름</th>
<th>작용</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr>
<tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr>
<tr>
<td>config</td>
<td>전체 설정 정보입니다. 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다.<ul style="margin:0;">
<li>useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자가 CDN을 통해 시청하도록 설정하며, 요금이 저렴하지만 딜레이가 비교적 많이 발생합니다. false는 일반 시청자가 저딜레이를 통해 시청하도록 설정하며, 요금이 CDN과 마이크 연결 요금의 중간 정도지만 딜레이가 1초 이내로 제어됩니다.</li>
<li>CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용됩니다. CDN을 통해 시청하는 재생 도메인을 지정하는 데 사용하며, 라이브 방송 콘솔에 로그인하여 <a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a> 페이지에서 설정할 수 있습니다.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>
<pre>
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst: true: 일반 시청자가 CDN을 통해 시청, false: 일반 시청자가 저딜레이를 통해 시청
//yourCDNPlayDomain: CDN을 통해 시청하는 경우 설정하는 재생 도메인
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, yourCDNPlayDomain);
mLiveRoom.login(SDKAPPID, userId, userSig, config, 
    new TRTCLiveRoomCallback.ActionCallback() {
            @Override
            public void onCallback(int code, String msg) {
                if (code == 0) {
                    //로그인 성공
                }
            }
});
</pre>

<span id="model.step5"> </span>
### 5단계: 호스트의 방송 시작
1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 방송 시작 전 먼저 `startCameraPreview`를 호출하여 카메라 미리보기를 실행할 수 있으며, 인터페이스에 뷰티 필터 조절 버튼을 설정해 호출하고`getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
 >?엔터프라이즈 버전 이외의 SDK는 얼굴 변경 및 스티커 효과 기능을 지원하지 않습니다.
 >
3. 호스트는 뷰티 필터 효과 조정 후 `createRoom`을 호출하여 새로운 라이브 룸을 생성할 수 있습니다.
4. 호스트가 `startPublish`를 호출해 푸시 스트림을 시작합니다. CDN을 통해 시청하도록 설정하고 싶은 경우 login 시 전달되는 `TRTCLiveRoomConfig` 매개변수에서 `useCDNFirst` 및 `CDNPlayDomain`을 설정하고, `startPublish` 시 라이브 방송 풀 스트림에 사용할 streamID를 지정합니다.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```java
// 1. 호스트 닉네임 및 프로필 사진 설정
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2. 호스트 라이브 시작 전 미리보기 및 뷰티 필터 매개변수 설정
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3. 호스트 방 생성
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "테스트 룸";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. 호스트 푸시 스트림 시작 및 스트림을 CDN에 배포
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
```

<span id="model.step6"> </span>
### 6단계: 시청자 시청
1. 시청자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 시청자 측에서 서비스 백그라운드로부터 최신 라이브 방송 방 리스트를 가져옵니다.
 >?Demo의 라이브 룸 리스트는 참고용입니다. 라이브 룸 리스트 로직은 매우 다양하여 Tencent Cloud에서는 현재 라이브 룸 리스트 관리 서비스를 제공하지 않으며, 라이브 룸 리스트는 직접 관리하시기 바랍니다.
 >
3. 시청자가 `getRoomInfos`을 호출해 방 상세 정보를 가져옵니다. 해당 정보는 호스트가 `createRoom`을 호출하여 라이브 룸 생성 시 설정한 간단한 설명 정보입니다.
 >!라이브 룸 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfos` 호출 관련 단계는 건너뛸 수 있습니다.
4. 시청자가 라이브 룸 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
5. `startPlay`를 호출하고 호스트의 userId를 전달하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자 측에서 직접 `startPlay`를 호출하고 호스트의 userId를 제출하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자가 방 입장 후 `onAnchorEnter`의 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userId정보가 포함되어 있어 `startPlay`를 호출하면 재생됩니다. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```java
// 1. 서비스 백그라운드로부터 획득하는 방 리스트가 roomList라고 가정할 경우,
List<Integer> roomList = GetRoomList();

// 2. getRoomInfos 호출을 통해 방 상세 정보 획득
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // 방 상세 정보 획득 후, 호스트 리스트 페이지에 호스트 닉네임, 프로필 사진 등 관련 정보를 표시할 수 있습니다.
        }
    }
})

// 3. 방 roomid를 선택해 입장
mLiveRoom.enterRoom(roomid, null);

// 4. 시청자가 호스트의 입장 알림을 수신하고, 재생 시작
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. 시청자가 호스트 화면 재생
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

<span id="model.step7"> </span>
### 7단계: 시청자와 호스트 마이크 연결
1. 시청자가 `requestJoinAnchor`를 호출하여 호스트에게 마이크 연결을 요청합니다.
2. 호스트가 `TRTCLiveRoomDelegate#onRequestJoinAnchor`(즉, 시청자의 마이크 연결 요청) 이벤트 알림을 수신합니다.
3. 호스트가 `responseJoinAnchor`를 호출하여 시청자의 마이크 연결 요청을 수락할지 여부를 결정합니다.
4. 시청자가 `TRTCLiveRoomDelegate#responseCallback` 이벤트 알림을 수신합니다. 해당 알림에는 호스트가 처리한 결과가 포함되어 있습니다.
5. 호스트가 마이크 연결 요청에 동의하면, 시청자는 `startCameraPreview`를 호출하여 로컬 카메라를 켜고 `startPublish`를 호출하여 시청자의 푸시 스트림을 시작할 수 있습니다.
6. 호스트는 시청자의 푸시 스트림 시작 알림 후 `TRTCLiveRoomDelegate#onAnchorEnter` (즉, 다른 채널의 멀티미디어 스트림 도착) 알림을 수신하며, 해당 알림에는 시청자의 userId가 포함되어 있습니다.
7. 호스트가 `startPlay`를 호출하면 마이크가 연결된 시청자의 비디오 화면을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```java
// 1. 시청자가 마이크 연결 요청
mLiveRoom.requestJoinAnchor(mSelfUserId + "님이 마이크 연결을 요청합니다.", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. 호스트가 시청자 요청 수락
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. 시청자가 미리보기 실행 및 푸시 스트림 시작
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2. 호스트가 마이크 연결 요청 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
		    String reason, final int timeout) {
        // 3. 상대방의 마이크 연결 요청 수락
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "마이크 연결 수락");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6. 호스트가 마이크가 연결된 시청자의 마이크 켜짐 알림 수신
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7. 호스트가 시청자 화면 재생
        mLiveRoom.startPlay(userId, view, null);
    }
});
```

<span id="model.step8"> </span>
### 8단계: 호스트간의 PK
1. 호스트 A가 `requestRoomPK`를 호출하여 호스트 B에게 마이크 연결을 요청합니다.
2. 호스트 B가 `TRTCLiveRoomDelegate onRequestRoomPK` 콜백 알림을 수신합니다.
3. 호스트 B가 `responseRoomPK`를 호출하여 호스트 A의 PK 요청을 수락할지 여부를 결정합니다.
4. 호스트 B가 호스트 A의 요청을 수락하면 `TRTCLiveRoomDelegate onAnchorEnter` 알림을 기다린 후 `startPlay`를 호출하여 호스트 A의 비디오 화면을 재생합니다.
5. 호스트 A가 PK 요청 수락 여부에 대한 `responseCallback` 콜백 알림을 수신합니다.
6. 호스트 A의 요청이 수락되면 `TRTCLiveRoomDelegate onAnchorEnter` 알림을 기다린 후 `startPlay`를 호출하여 호스트 B의 비디오 화면을 재생합니다.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```java
// 호스트 A:
// 호스트 A가 12345 방 생성
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. B의 방 입장 알림 수신
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1. 호스트 A가 호스트 B에게 PK 요청
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5. 동의 여부 콜백 수신
        if (code == 0) {
            // 사용자가 수락
        } else {
            // 사용자가 거절
        }
    }
});

// 호스트 B:
// 호스트 B가 54321 방 생성
mLiveRoom.createRoom(54321, param, null);

// 2. 호스트 B가 호스트 A의 메시지 수신
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. 호스트 B가 호스트 A의 요청 수락
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. 호스트 B가 호스트 A의 방 입장 알림 수신, 호스트 A의 화면 재생
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

<span id="model.step9"> </span>
### 9단계: 문자 채팅 및 댓글 자막 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
 IM의 백그라운드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
```java
// 발신 측: 텍스트 메시지 발송
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// 수신 측: 텍스트 메시지 리슨
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String roomId, 
		    String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        Log.d(TAG, userInfo.userName + "님이 발송한 메시지:" + message);
    }
});
```
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
사용자 정의 메시지는 좋아요 메시지 발송 등과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
```java
// 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 좋아요 메시지를 구분할 수 있습니다.
// eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": 좋아요 메시지
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 수신 측: 사용자 정의 메시지 리슨
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
		    String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 댓글 자막 메시지 수신
            Log.d(TAG, userInfo.userName + "님이 발송한 댓글 자막 메시지:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 좋아요 메시지 수신
            Log.d(TAG, userInfo.userName + "님이 좋아합니다.");
        }
    }
});
```
