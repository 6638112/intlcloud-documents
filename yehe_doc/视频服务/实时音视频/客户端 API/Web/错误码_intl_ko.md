
>!본문은 4.x.x 버전의 TRTC Web SDK에 적용됩니다.

## 오류 코드 정의

| Key         | getCode | 에러 코드 | 설명          |
|------|----|---|------------------------------|
| INVALID_PARAMETER   | 4096    | 0x1000 | 잘못된 매개 변수<br>처리 제안: 전송 매개 변수가 유형이 올바른지 등 SDK 요구 사항을 충족하는지 확인하십시오. |
| INVALID_OPERATION   | 4097    | 0x1001 | 잘못된 작업<br/>처리 제안: API 호출 로직이 해당 인터페이스 문서에 따라 SDK 요구 사항을 충족하는지 확인하십시오. 예: 방 미입장 시 publish 인터페이스를 호출하는 것은 금지되어 있습니다. |
| NOT_SUPPORTED       | 4098    | 0x1002 | SDK 인터페이스를 호출할 때 발생하며 현재 브라우저가 해당 인터페이스 호출을 지원하지 않습니다<ul style="margin:0"><li/>설명: SDK 인터페이스를 호출할 때 발생하며 현재 브라우저가 해당 인터페이스 호출을 지원하지 않습니다<li/>처리 제안: SDK에서 지원하는 브라우저를 사용하도록 안내합니다. [브라우저 지원 점검](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html)을 참고하십시오          |
| DEVICE_NOT_FOUND    | 4099    | 0x1003 | 현재 장치에 마이크나 카메라가 없지만 마이크나 카메라를 수집하려고 합니다<br>처리 제안: 사용자가 장치의 카메라와 마이크가 정상인지 확인하도록 안내합니다. 서비스측은 방에 들어가기 전에 장치 점검 로직을 추가해야 합니다. [통화 전 환경 및 장치 점검](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html)을 참고하십시오. |
| INITIALIZE_FAILED   | 4100    | 0x1004 | LocalStream.initialize() 수집 실패, [자세한 처리 제안](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.INITIALIZE_FAILED)을 참고하십시오.         |
| SIGNAL_CAHNNEL_SETUP_FAILED        | 16385   | 0x4001 | 신호 채널 설정 실패. 일반적으로 Tencent Cloud 계정과 관련이 있습니다. [계정 관련 오류 메시지](https://intl.cloud.tencent.com/document/product/647/41665)를 참고하십시오.       |
| SIGNAL_CHANNEL_ERROR               | 16386   | 0x4002 | 신호 채널 오류.         |
| ICE_TRANSPORT_ERROR                | 16387   | 0x4003 | ICE Transport 연결 오류, 즉, 멀티미디어 데이터 전송 채널 오류입니다. 이것은 주로 클라이언트의 비정상적인 UDP 포트에 의해 발생합니다(사용자 컴퓨터의 방화벽 또는 라우터의 방화벽의 포트 제한에 의해 발생할 수 있음). 특정 포트에 대해서는 [포트 화이트리스트](https://intl.cloud.tencent.com/document/product/647/35164)를 참고하십시오.  |
| JOIN_ROOM_FAILED    | 16388   | 0x4004 | 방 입장 실패. 자세한 내용은 [방 입장 실패 관련 오류 정보](https://intl.cloud.tencent.com/document/product/647/41665)를 참고하십시오          |
| CREATE_OFFER_FAILED                | 16389   | 0x4005 | sdp offer 생성 실패.          |
| SIGNAL_CHANNEL_RECONNECTION_FAILED | 16390   | 0x4006 | WebSocket 신호 터널 재연결 실패<ul style="margin:0"><li/>설명: WebSocket 연결이 끊어지면 SDK는 여러 번 재연결을 시도하고, 실패 시 이 오류 발생<li/>처리 제안: 사용자에게 네트워크를 확인하고 다시 방에 들어가도록 알립니다      |
| UPLINK_RECONNECTION_FAILED         | 16391   | 0x4007 | 업스트림 PeerConnection 재연결 실패<ul style="margin:0"><li/>설명: 업스트림 PeerConnection의 연결이 끊어지면 SDK는 여러 번 재연결을 시도하며 실패 시 이 오류 발생<li/>처리 제안: 사용자에게 네트워크를 확인한 다음 다시 푸시 스트림하거나 방에 다시 입장하도록 알립니다       |
| DOWNLINK_RECONNECTION_FAILED       | 16392   | 0x4008 | 다운스트림 PeerConnection 재연결 실패<ul style="margin:0"><li/>설명: 다운스트림 PeerConnection이 비정상적으로 연결이 끊긴 경우 SDK는 여러 번 재연결을 시도하며 실패 시 이 오류 발생<li/>처리 제안: 사용자에게 네트워크를 확인하고 다시 방에 입장하도록 알립니다       |
| REMOTE_STREAM_NOT_EXIST            | 16400   | 0x4010 | 원격 스트림이 존재하지 않음<ul style="margin:0"><li/>설명: A가 B가 푸시한 스트림을 구독하려고 시도할 때 B가 푸시 스트림을 취소하여 A가 B를 구독하는데 실패<li/>처리 제안: 정상적인 인터랙티브 프로세스에 속하며 액세스 측에서 처리할 필요가 없습니다     |
| CLIENT_BANNED       | 16448   | 0x4040 | 사용자가 방에서 퇴장됨. 이유:<ul style="margin:0"><li/>같은 이름의 사용자가 같은 방에 입장, **참고**: 같은 이름의 사용자는 같은 방에 동시에 입장할 수 없으며, 양측 간에 비정상적인 음성 및 영상 통화가 발생할 수 있습니다. 서비스측에서 이런 상황을 방지해야 합니다.<li/>서버 API를 사용하여 계정 관리자에 의해 방에서 퇴장됩니다  |
| SERVER_TIMEOUT      | 16449   | 0x4041 | MediaConnect 서비스 시간 초과     |
| SUBSCRIPTION_TIMEOUT               | 16450   | 0x4042 | 원격 스트림 구독 시간 초과       |
| PLAY_NOT_ALLOWED    | 16451   | 0x4043 | 자동 재생 금지 오류<ul style="margin:0"><li/>설명: 'play()'를 호출하여 멀티미디어를 재생할 때 [자동 재생 정책](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes)의 제한으로 인해 자동으로 재생되지 않음<li/>처리 제안: 사용자는 'resume()'을 호출하여 제스처 작업을 통해 계속 재생하도록 안내 해야 합니다. [자동 재생 제한 처리 제안](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)을 참고하십시오 |
| DEVICE_AUTO_RECOVER_FAILED         | 16452   | 0x4044 | 카메라 및 마이크의 자동 수집에 실패했습니다. LocalStream의 error 이벤트 발생<ul style="margin:0"><li/>스트리밍 중인 사용자의 미디어 장치가 변경되면(예시: 카메라 연결/해제, 마이크, 연결 헐거워짐 등) SDK는 수집 복구를 시도합니다. 이 오류 발생 시 복구 실패<li/>처리 제안: 미디어 장치가 자동으로 수집을 복구하지 못한다는 사실을 사용자에게 알립니다. 카메라와 마이크 연결이 헐거운지 확인하고, 다른 애플리케이션에 의해 점유되고 있지 않은지 확인합니다.<li/>페이지에 재시도 버튼을 제공하여, 사용자가 재시도를 클릭하면 카메라와 마이크가 재수집됩니다 |
| START_PUBLISH_CDN_FAILED           | 16453   | 0x4045 | CDN으로 푸시 스트림 시작 실패          |
| STOP_PUBLISH_CDN_FAILED            | 16454   | 0x4046 | CDN으로 푸시 스트림 중지 실패          |
| START_MIX_TRANSCODE_FAILED         | 16455   | 0x4047 | 혼합 스트림 및 트랜스 코딩 시작 실패     |
| STOP_MIX_TRANSCODE_FAILED          | 16456   | 0x4048 | 혼합 스트림 및 트랜스 코딩 중지 실패     |
| NOT_SUPPORTED_H264  | 16457   | 0x4049 | 현재 장치는 H.264 미지원          |
| SWITCH_ROLE_FAILED  | 16458   | 0x404a | 역할 전환 실패         |
| UNKOWN      | 65535   | 0xFFFF | 알수없는 오류     |



## 계정 오류

| 에러 코드 | 오류 유형 | 설명        |
|:--|:-----|:-------------------|
| -8     | 계정 시스템 | sdkAppId가 정확하지 않습니다. sdkAppId가 올바르게 입력되었는지 확인하십시오              |
| 70001  | 계정 시스템 | userSig가 만료되었습니다. 다시 생성하십시오. 서명이 생성 직후 만료되는 경우 유효 기간이 너무 짧거나 0으로 설정되어 있는지 확인하십시오      |
| 70002  | 계정 시스템 | userSig의 길이는 0입니다. 서명 계산을 위한 소스 코드를 얻기 위해 sign_src에 액세스하고 서명이 올바르게 계산되었는지 확인하기 위해 매개변수를 확인하십시오 |
| 70003  | 계정 시스템 | userSig 인증에 실패했습니다. 짧은 버퍼 길이 등으로 인해 userSig가 잘렸는지 확인하십시오    |
| 70004  | 계정 시스템 | userSig 인증에 실패했습니다. 짧은 버퍼 길이 등으로 인해 userSig가 잘렸는지 확인하십시오    |
| 70005  | 계정 시스템 | userSig 인증에 실패했습니다. 생성된 userSig가 올바른지 도구를 사용하여 확인하십시오.    |
| 70006  | 계정 시스템 | userSig 인증에 실패했습니다. 생성된 userSig가 올바른지 도구를 사용하여 확인하십시오     |
| 70007  | 계정 시스템 | userSig 인증에 실패했습니다. 생성된 userSig가 올바른지 도구를 사용하여 확인하십시오     |
| 70008  | 계정 시스템 | userSig 인증에 실패했습니다. 생성된 userSig가 올바른지 도구를 사용하여 확인하십시오     |
| 70009  | 계정 시스템 | 비즈니스 공개키로 userSig 인증에 실패했습니다. userSig 생성에 사용된 개인키와 sdkAppId가 일치하는지 확인하십시오    |
| 70010  | 계정 시스템 | userSig 인증에 실패했습니다. 생성된 userSig가 올바른지 도구를 사용하여 확인하십시오     |
| 70013  | 계정 시스템 | userSig의 userId가 요청의 userId와 다릅니다. 로그인 시 입력한 userId가 userSig에 입력된 것과 동일한지 확인하십시오              |
| 70014  | 계정 시스템 | userSig의 sdkAppId가 요청의 sdkAppId와 다릅니다. 로그인 시 입력한 sdkAppId가 userSig에 입력된 것과 동일한지 확인하십시오        |
| 70015  | 계정 시스템 | 이 sdkAppId 및 계정 유형에 대한 인증 방법을 찾을 수 없습니다. 계정 연동이 되었는지 확인하십시오    |
| 70016  | 계정 시스템 | 가져온 공개키의 길이는 0입니다. 공개키가 업로드되었는지 확인하십시오. 방금 업로드한 경우 10분 후에 다시 시도하십시오    |
| 70017  | 계정 시스템 | 서드 파티 티켓의 내부 확인 시간이 초과되었습니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70018  | 계정 시스템 | 서드 파티 티켓의 내부 확인에 실패했습니다      |
| 70019  | 계정 시스템 | HTTPS 기반 유효성 검사를 위한 티켓 필드가 비어 있습니다. 올바른 userSig를 입력하십시오       |
| 70020  | 계정 시스템 | sdkAppId를 찾을 수 없습니다. Tencent Cloud에서 설정했는지 확인하십시오  |
| 70052  | 계정 시스템 | 잘못된 userSig입니다. 새로 생성하고 다시 시도하십시오   |
| 70101  | 계정 시스템 | 빈 요청 패킷입니다      |
| 70102  | 계정 시스템 | 요청 패킷에 잘못된 계정 유형이 있습니다   |
| 70103  | 계정 시스템 | 전화번호 형식이 잘못되었습니다    |
| 70104  | 계정 시스템 | 이메일 주소 형식이 잘못되었습니다        |
| 70105  | 계정 시스템 | 잘못된 TLS 계정 형식입니다    |
| 70106  | 계정 시스템 | 잘못된 계정 형식 유형입니다    |
| 70107  | 계정 시스템 | userId가 등록되지 않았습니다     |
| 70113  | 계정 시스템 | 잘못된 배치 수량입니다      |
| 70114  | 계정 시스템 | 보안상의 이유로 제한됩니다      |
| 70115  | 계정 시스템 | uin이 sdkAppId 개발자의 uin과 일치하지 않습니다     |
| 70140  | 계정 시스템 | sdkAppId와 acctype이 일치하지 않습니다          |
| 70145  | 계정 시스템 | 잘못된 계정 유형입니다        |
| 70169  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70201  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70202  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70203  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70204  | 계정 시스템 | sdkAppId에 일치하는 acctype이 없습니다         |
| 70205  | 계정 시스템 | acctype을 찾지 못했습니다. 다시 시도하십시오    |
| 70206  | 계정 시스템 | 요청에 잘못된 배치 수량이 있습니다        |
| 70207  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오     |
| 70208  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오     |
| 70209  | 계정 시스템 | 개발자의 uin을 가져오지 못했습니다     |
| 70210  | 계정 시스템 | 요청한 uin은 개발자의 uin이 아닙니다   |
| 70211  | 계정 시스템 | 요청에 잘못된 uin이 있습니다     |
| 70212  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70213  | 계정 시스템 | 내부 데이터에 액세스하지 못했습니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70214  | 계정 시스템 | 내부 티켓 확인에 실패했습니다    |
| 70221  | 계정 시스템 | 잘못된 로그인 상태입니다. UserSig로 로그인을 다시 인증하십시오   |
| 70222  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오     |
| 70225  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70231  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70236  | 계정 시스템 | user signature 인증에 실패했습니다    |
| 70308  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70346  | 계정 시스템 | 티켓 인증에 실패했습니다       |
| 70347  | 계정 시스템 | 티켓이 만료되어 인증에 실패했습니다      |
| 70348  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70362  | 계정 시스템 | 내부 시간 초과입니다. 다시 시도하십시오. 재시도 실패 시 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |
| 70401  | 계정 시스템 | 내부 오류입니다. 다시 시도하십시오     |
| 70402  | 계정 시스템 | 잘못된 매개 변수. 모든 필수 필드를 채우고 입력한 값이 요구 사항을 충족하는지 확인하십시오     |
| 70403  | 계정 시스템 | 작업 요청자가 애플리케이션 관리자가 아니며 작업을 수행할 권한이 없습니다      |
| 70050  | 계정 시스템 | 로그인 실패 및 여러 번의 재시도 때문에 계정이 일시적으로 잠겼습니다. 티켓이 맞는지 확인하고 잠시 후 다시 시도하십시오   |
| 70051  | 계정 시스템 | 차단된 계정입니다. [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오 |

## 방 입장 오류
| 에러 코드 | 오류 정보              |
|:--|:-----------|
| 10006  | 연체로 인해 서비스가 중단되었습니다. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인하고 생성한 애플리케이션을 찾은 다음 **애플리케이션 정보**를 클릭하여 TRTC 서비스 상태를 확인합니다 |
| -10011 | 알 수 없는 서버 오류입니다. 다시 시도하십시오        |
| -10012 | roomId가 전달되지 않았거나 요구 사항을 충족하지 않습니다. string 유형으로 roomId를 사용하려면 `TRTC.createClient`를 호출할 때 useStringRoomId를 true로 설정합니다   |
| -10013 | userSig 인증에 실패했습니다     |
| -10015 | 서버에서 서버 노드를 가져오지 못했습니다. 다시 시도하십시오      |
| -10016 | 서버에 룸을 만들지 못했습니다. roomId가 트래픽 제어 범위 내에 있는지 확인하십시오               |
| -10018 | 고급 권한 제어 기능 활성화 후 client.join은 privateMapKey를 전달하지 않거나 privateMapKey는 ‘ ’ 입니다. 자세한 내용은 [고급 권한 제어 기능 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 참고하십시오 |
| -10019 | 고급 권한 제어가 활성화된 후 client.join이 전달하는 privateMapKey가 요구 사항을 충족하지 않습니다. 자세한 내용은 [고급 권한 제어 기능 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 참고하십시오 |
| -10020 | 서버 연결 시간이 초과되었습니다. 다시 시도하십시오    |

## 일반적인 오류 및 처리 방법
다음 오류는 응용 프로그램 측 개입을 통해 수정해야 합니다. 예를 들어 카메라 액세스가 거부된 경우 영상 통화를 할 수 있으려면 애플리케이션에서 사용자에게 카메라 액세스 권한을 부여하라는 메시지를 표시해야 합니다.


| 오류 정보    | 오류 원인    | 솔루션    |
|:--------------|:------------|:-------------|
| publish timeout     | publish 시간 초과               | 새로 고침하고 publish()를 다시 호출합니다          |
| join room timeout   | 방 입장 시간 초과    | 페이지를 새로고침하고 다시 시도하십시오    |
| DTLS Transport connection timeout (10s)     | DTLS Transport 연결 시간 초과    | 새로고침하고 다시 시도하십시오      |
| failed to connect to remote server via websocket           | websocket 연결 실패         | 새로고침하고 다시 시도하십시오      |
| ICE/DTLS Transport connection failed   | 미디어 전송 연결 설정 실패     | [방화벽 설정](https://intl.cloud.tencent.com/document/product/647/35164)을 확인하십시오         |
| previous publishing is ongoing, please avoid re-publishing | 이미 publishing 상태   | publish 후 다시 publish()를 호출하지 마십시오      |
| AbortError          | 알 수 없는 장치/시스템 오류로 인해 장치에 액세스 불가        | 통화 전에 장치를 테스트하십시오           |
| NotReadableError    | 하드웨어, 브라우저 또는 운영 체제의 웹 수준 오류로 인해 액세스할 수 없는 장치를 찾을 수 없음 | 브라우저의 오류 메시지 처리에 따라 사용자에게 현재 카메라/마이크에 대한 액세스를 요청하는 다른 애플리케이션이 없는지 확인하고 다시 시도하십시오  |
| NotFoundError       | 요청 매개변수의 미디어(오디오, 비디오 또는 화면 공유)를 찾을 수 없음     | 통화 전에 장치를 테스트하십시오           |
| NotAllowedError | 사용자가 현재 브라우저 인스턴스의 오디오, 비디오, 화면 공유 액세스 요청을 거절한 상태   | 사용자는 카메라/마이크의 액세스를 인증해야 멀티미디어 통화를 할 수 있습니다       |
| SignalChannel reconnect failed      | websocket 연결 끊김             | 새로고침하고 다시 시도하십시오      |
| duplicate publishing, please unpublish and then re-publish | publish 중복               | publish() 전에 unpublish()를 먼저 호출하십시오      |
| OverconstrainedError        | 브라우저에서 cameraId / microphoneId를 가져올 수 없음     | cameraId / microphoneId의 값이 비어 있지 않은 유효한 문자열인지 확인하십시오      |
| RtcError: no valid ice candidate found      | TRTC Web SDK가 STUN에 홀 펀칭 실패      | 자세한 내용은 [방화벽 설정](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오       |
