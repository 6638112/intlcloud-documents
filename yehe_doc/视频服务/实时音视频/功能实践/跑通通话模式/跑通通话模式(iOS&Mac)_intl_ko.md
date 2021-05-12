## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 그중 영상 통화(VideoCall)와 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/35107)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스'와 '프록시' 라는 상이한 서버 노드로 구성됩니다.
- **인터페이스**
인터페이스 노드는 가장 우수한 회로와 고성능 기기를 채택하여 엔드 투 엔드의 마이크 통화 시 딜레이 시간이 짧고, 시간당 높은 과금이 적용됩니다.
- **프록시**
프록시 노드는 일반 회로와 일반 성능의 기기를 채택하여 동시 접속에 의한 시청 수요를 충족할 수 있으며, 시간당 낮은 과금이 적용됩니다.

통화 모드에서 TRTC 방에 입장한 모든 사용자는 인터페이스를 할당받습니다. 각 사용자 모두가 '호스트'로서 언제든지 발언할 수 있어(업스트림 동시 접속 최대 30개) 온라인 회의 등 시나리오의 사용에 적합합니다. 단, 단일 방 참가자 수는 300명으로 제한됩니다.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)


## 예시 코드
[Github]에 로그인하면 본 문서와 관련된 예시 코드를 받을 수 있습니다.
![](https://main.qcloudimg.com/raw/9cc33faf91173116e2d259f6b8b97d55.png)

>?Github 액세스가 느리다면 [TXLiteAVSDK_TRTC_iOS_latest.zip](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)을 직접 다운로드하십시오.

## 작업 순서
<span id="step1"> </span>
### 1단계: SDK 통합
다음의 방법으로 **TRTC SDK**를 프로젝트로 통합할 수 있습니다.
#### 방법1: CocoaPods로 통합
1. [CocoaPods 공식 홈페이지 설치 가이드](https://guides.cocoapods.org/using/getting-started.html)를 참조해 **CocoaPods**를 설치합니다.
2. 현재 프로젝트의 루트 디렉터리에서 'Podfile' 파일을 연 뒤 다음 내용을 추가합니다.
>?루트 디렉터리에 'Podfile' 파일이 없는 경우, 'pod init' 명령어를 실행하여 파일을 생성한 뒤 다음 내용을 추가합니다.
>
```
target 'Your Project' do
        pod 'TXLiteAVSDK_TRTC'
end
```
3. 다음 명령어를 실행하여 **TRTC SDK**를 설치합니다.
```
pod install
```
설치가 완료되면 현재 프로젝트의 루트 디렉터리에 **xcworkspace** 파일 하나가 생성됩니다.
4. 새로 생성된 **xcworkspace** 파일을 열면 완료됩니다.

#### 방법2: ZIP 다운로드 후 수동 통합
CocoaPods 환경을 설치하지 않거나 이미 설치했으나 CocoaPods 리포지토리 액세스 속도가 느리다면 [ZIP 압축 프로그램](https://intl.cloud.tencent.com/document/product/647/34615)을 다운로드한 뒤 [빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)을 참조하여 SDK를 프로젝트에 통합하십시오.

<span id="step2"> </span>
### 2단계: 미디어 디바이스 권한 추가
'Info.plist' 파일에서 카메라, 마이크의 신청 권한을 추가합니다.

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | 카메라 권한 사용 이유 설명. 예: 카메라 권한을 획득해 실행해야 영상 채팅 시 화면이 표시됨 |
| Privacy - Microphone Usage Description | 마이크 권한 사용 이유 설명. 예: 마이크 권한을 획득해 실행해야 채팅 시 음성이 나옴 |

<span id="step3"></span>
### 3단계: SDK 인스턴스 초기화 및 이벤트 리슨 콜백

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) 인터페이스로 'TRTCCloud' 인스턴스를 생성합니다. 
```swift
// trtcCloud 인스턴스 생성
let trtcCloud: TRTCCloud = TRTCCloud.sharedInstance()
trtcCloud.delegate = self
```
2. 'delegate' 속성을 설정하여 이벤트 콜백을 등록한 뒤 관련 이벤트와 오류 알림을 리슨합니다.
```swift
// 오류 통지는 리스너를 통해 파악하고 사용자에게 고지됨
func onError(_ errCode: TXLiteAVError, errMsg: String?, extInfo: [AnyHashable : Any]?) {
        if ERR_ROOM_ENTER_FAIL == errCode {
                toastTip("방 입장 실패[\(errMsg ?? "")]")
                exitRoom()
        }
}
```

<span id="step4"> </span>
### 4단계: 방 입장 매개변수 TRTCParams 어셈블리
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스 호출 시 핵심 매개변수[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) 하나를 입력해야 합니다. 다음 필드는 매개변수 필수 작성 사항입니다.

| 매개변수 이름 | 필드 유형 | 보충 설명 | 작성 예시 |
|---------|---------|---------|---------|
| sdkAppId | 숫자 | 애플리케이션 ID, <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID 조회 가능 |1400000123 |
| userId | 문자열 |영문 알파벳 대소문자(a~z, A~Z), 숫자(0~9), 언더바, 하이픈만 입력 가능 |test_user_001 |
| userSig | 문자열 | userId로 userSig 계산, 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166) 참조  | eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 문자열 타입의 방 번호 미지원이 기본값임. 이 타입으로 방 번호 설정 시 방 입장 속도 느려짐. 문자열 타입의 방 번호를 꼭 사용해야 할 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의 | 29834 |

>! TRTC에서는 2개의 동일한 userId로 동시에 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.

<span id="step5"> </span>
### 5단계: 방 생성 및 입장
1. [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)을 호출하여 TRTCParams 매개변수 'roomId'가 지정한 멀티미디어 방에 들어갈 수 있습니다. 해당 방이 존재하지 않는 경우 SDK는 필드 'roomId'를 방 번호로 하는 신규 방을 자동 생성합니다.
2. 응용 시나리오에 따라 적합한 **'appScene'** 매개변수를 설정하십시오. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.
 - 영상 통화는 'TRTCAppScene.videoCall'로 설정하십시오.
 - 음성 통화는 'TRTCAppScene.audioCall'로 설정하십시오.
3. 방에 입장하면 SDK는 'onEnterRoom(result)' 이벤트를 콜백합니다. 매개변수 'result'가 0보다 크면 방 입장 성공을 뜻하며, 세부 값은 방 입장 소요 시간으로, 단위는 밀리세컨드(ms)입니다. 'result'가 0보다 작으면 방 입장 실패를 뜻하며, 세부 값은 방 입장 실패 에러 코드입니다.

```swift
func enterRoom() {
    let params = TRTCParams.init()
    params.sdkAppId = sdkappid
    params.userId   = userid
    params.userSig  = usersig
    params.roomId   = 908
    trtcCloud.enterRoom(params, appScene: TRTCAppScene.videoCall)
}

func onEnterRoom(_ result: Int) {
    if result > 0 {
        toastTip("방 입장 성공, 총 소요 시간[\(result)]ms")
    } else {
        toastTip("방 입장 실패, 에러 코드[\(result)]")
    }
}
```

> !
>- 방 입장에 실패하면 SDK는 동시에 'onError' 이벤트를 콜백하며, 'errCode'([에러 코드](https://intl.cloud.tencent.com/document/product/647/35124)), 'errMsg'(에러 원인), 'extraInfo'(보관 매개변수)를 반환합니다.
>- 이미 방에 입장한 경우 `exitRoom()`을 호출하여 해당 방에서 퇴장해야만 다른 방에 들어갈 수 있습니다.

<span id="step6"> </span>
### 6단계: 원격 멀티미디어 스트림 구독
SDK는 자동 구독 및 수동 구독 기능을 지원합니다.

#### 자동 구독 모드(기본값)
자동 구독 모드에서 특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.
1. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.
2. [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)를 이용하여 특정 userId의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트가 공지됩니다. 단, 이때 SDK는 비디오 데이터 명령어 처리법을 수신받지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 원격 사용자의 비디오 데이터와 표시 'view'를 연결하십시오.
4. [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff)를 통해 비디오 화면의 표시 모드를 지정하십시오.
 - Fill 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066)를 이용하여 특정 userId의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

```swift
// 인스턴스 코드: 구독 통지(또는 구독 취소)한 원격 사용자의 비디오 화면
func onUserVideoAvailable(_ userId: String, available: Bool) {
    let remoteView = remoteViewDic[userId] as! UIView
    if available {
        trtcCloud.startRemoteView(userId, view: remoteView)
        trtcCloud.setRemoteViewFillMode(userId, mode: TRTCVideoFillMode.fit)
    } else {
        trtcCloud.stopRemoteView(userId)
    }
}
```

>? 'onUserVideoAvailable()' 이벤트 콜백이 발생한 뒤 즉시 'startRemoteView()'를 호출하여 비디오 스트림을 구독하지 않으면 SDK는 5초 이내에 원격 비디오 데이터의 수신을 중지합니다.

#### 수동 구독 모드
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) 인터페이스를 이용해 SDK를 수동 구독 모드로 설정할 수 있습니다. 수동 구독 모드에서 SDK는 같은 방에 입장한 사용자의 멀티미디어 데이터를 자동 수신하지 않습니다. API 함수를 이용해 직접 트리거해야 합니다.

1. **방 입장 이전** [setDefaultStreamRecvMode(false, video: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) 인터페이스를 호출하면 SDK가 수동 구독 모드로 설정됩니다.
2. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) 이벤트가 공지됩니다. 이때 [muteRemoteAudio(userId, mute: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트가 공지됩니다. 이때 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.

<span id="step7"> </span>
### 7단계: 로컬의 멀티미디어 스트림 배포
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)를 호출하면 로컬 마이크 수집 기능이 실행되고, 수집한 음성을 인코딩한 뒤 송신할 수 있습니다.
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)를 호출하면 로컬 카메라가 실행되고, 수집한 화면을 인코딩한 뒤 송신할 수 있습니다.
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15)를 호출하면 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드는 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화면 질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.

```swift
//예시 코드: 로컬의 멀티미디어 스트림 배포
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.fit)
trtcCloud.startLocalPreview(frontCamera, view: localView)
trtcCloud.startLocalAudio()
```

>! Mac 버전의 SDK는 카메라와 마이크의 기본값이 설정돼 있습니다. [setCurrentCameraDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc)와 [setCurrentMicDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6)를 통해 카메라와 마이크 설정을 변경할 수 있습니다.

<span id="step8"> </span>
### 8단계: 현재 방에서 퇴장하기

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3)을 호출하여 방에서 퇴장합니다. 이때 SDK가 카메라와 마이크 등 기기를 차단 및 릴리스하기 때문에 [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) 콜백을 수신한 뒤에야 퇴장 처리됩니다.

```swift
// 퇴장 호출 뒤 onExitRoom 이벤트 콜백 대기
trtcCloud.exitRoom()

func onExitRoom(_ reason: Int) {
    print("방 나가기[\(roomId)]: reason[\(reason)]")
}
```

>! App이 다수의 멀티미디어 SDK를 동시에 통합했다면 하드웨어 점유 상황을 고려하여 'onExitRoom' 콜백을 수신한 뒤 다른 멀티미디어 SDK를 실행하십시오.
