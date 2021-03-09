[](id:que1)
### TRTC RoomID는 무엇인가요? 값의 범위는 어떻게 되나요?
RoomID는 방 번호이며 방의 고유 식별자로 사용됩니다. 방 번호 값 범위는 1~4294967295로 개발자가 점검 및 할당합니다.

[](id:que2)
### TRTC 방 입장 UserID는 무엇인가요? 값의 범위는 어떻게 되나요? 
UserID는 사용자 ID로, TRTC 애플리케이션에서 사용자의 고유 식별자로 사용됩니다. 길이는 32바이트 이하를 권장합니다. 영어 알파벳(대소문자 구별), 숫자 또는 언더바를 사용합니다.


[](id:que3)
### TRTC 방의 라이프사이클은 어떻게 되나요?
- 최초로 방에 입장한 사용자가 해당 방의 소유자이지만, 소유자가 직접 방을 삭제할 수는 없습니다.
- **통화 모드에서**: 모든 사용자가 퇴장하면 백그라운드에서 즉시 방을 삭제합니다.
- **라이브 방송 모드에서**: 호스트 역할의 사용자가 맨 마지막에 퇴장하는 경우 백그라운드에서 즉시 방을 삭제하며, 시청자가 맨 마지막에 퇴장하는 경우 백그라운드에서 10분 대기 후 방을 삭제합니다.
- 방의 개별 사용자가 오류로 인해 접속이 끊긴 경우 90초 후 서버에서 해당 사용자를 방에서 퇴장시킵니다. 방의 모든 사용자가 오류로 인해 접속이 끊긴 경우 90초 후 서버에서 방을 자동으로 삭제합니다.
- 사용자가 입장하고자 하는 방이 없을 경우 백그라운드에서 방이 자동으로 생성됩니다.

[](id:que4)
### TRTC에서 비구독 멀티미디어 스트림을 지원하나요? 
'바로 재생'을 위해 방 입장 시 자동으로 스트리밍을 구독하게 되며, setDefaultStreamRecvMode 인터페이스를 통해 수동 구독 모드로 전환할 수 있습니다.

[](id:que5)
### TRTC에서 사용자 정의 릴레이 푸시 스트림의 스트림 ID를 지원하나요?  
지원합니다. enterRoom의 매개변수 TRTCParams로 streamId를 지정할 수 있으며, startPublishing 인터페이스를 호출하여 매개변수 streamId를 전송할 수도 있습니다.

[](id:que6)
### TRTC 라이브 방송은 어떤 역할을 지원하며, 어떤 차이가 있나요?
라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)는 TRTCRoleAnchor(호스트)와 TRTCRoleAudience(시청자)라는 두 가지 역할을 지원합니다. 호스트 역할은 멀티미디어 데이터를 동시에 업스트림/다운스트림할 수 있으며, 시청자 역할은 다른 사람의 데이터를 다운스트림 재생만 할 수 있습니다. switchRole() 호출을 통해 역할을 교체할 수도 있습니다.

[](id:que7)
### TRTC의 역할(Role)을 어떻게 이해하면 되나요? 
라이브 방송에서 호스트와 시청자의 역할을 설정할 수 있습니다. 호스트 역할 TRTCRoleAnchor은 멀티미디어 업스트림/다운스트림 권한을 가지고 있으며 최대 30명까지 동시 접속을 지원합니다. 시청자 TRTCRoleAudience는 멀티미디어 다운스트림 권한만을 가지고 있으며 동시 접속 가능 인원은 최대 10만 명입니다.


[](id:que8)
### TRTC 방에서 어떤 응용 시나리오를 지원하나요?  
다음 시나리오를 지원합니다.
- TRTCAppSceneVideoCall: 일대일 영상 통화, 300인 화상 회의, 온라인 진료, 화상 채팅, 원격 면접 등에 적합한 영상 통화 시나리오입니다.
- TRTCAppSceneLIVE: 비디오 저 딜레이 라이브 방송, 10만 인터랙션 강의, 비디오 라이브 방송 PK, 화상 소개팅, 인터랙션 강의, 원격 교육, 초대형 회의 등에 적합한 비디오 ILVB입니다.
- TRTCAppSceneAudioCall: 일대일 음성 통화, 300인 음성 회의, 음성 채팅, 음성 회의, 온라인 마피아 게임 등에 적합한 음성 통화 시나리오입니다.
- TRTCAppSceneVoiceChatRoom: 음성 저 딜레이 라이브 방송, 음성 라이브 방송 마이크 연결, 음성 채팅, 노래방, FM 라디오 등에 적합한 음성 ILVB입니다.


[](id:que9)
### TRTC에서 지원하는 플랫폼에는 어떤 것이 있나요?
iOS, Android, Windows(C++), Windows(C#), Mac, 데스크톱 브라우저, Electron 등의 플랫폼을 지원합니다. 자세한 내용은 [플랫폼 지원](https://intl.cloud.tencent.com/document/product/647/35078)을 참조하십시오.

[](id:que10)
### TRTC의 라이트 버전, 프로 버전, 엔터프라이즈 버전 등 각 버전의 차이점은 무엇인가요? 
자세한 내용은 [각 버전 차이 대조표](https://intl.cloud.tencent.com/document/product/647/34615)를 참조하십시오.


[](id:que11)
### TRTC에서 라이브 방송 마이크 연결을 지원하나요?
지원합니다. 운영 가이드를 참조하십시오.
- [온라인 라이브 방송(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)
- [온라인 라이브 방송(Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [온라인 라이브 방송(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [온라인 라이브 방송(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35110)


[](id:que12)
### TRTC는 동시에 최대 몇 개의 방을 생성할 수 있나요?
동시에 4294967294개의 방이 존재할 수 있으며, 누적 방 수량에는 제한이 없습니다.

[](id:que13)
### 방은 어떻게 생성하나요?
방은 클라이언트 방 입장 시 Tencent Cloud 백그라운드에서 자동으로 생성합니다. 수동으로 생성할 필요 없이 클라이언트 관련 인터페이스 '방 입장'을 호출하면 됩니다.
- [iOS & Mac > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows(C++) > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)
- [Windows(C#) > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b)
- [Electron > enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?_ga=1.212321108.1562552652.1542703643#enterRoom)
- [데스크톱 브라우저 > join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html?_ga=1.256770123.1562552652.1542703643#join)

[](id:que14)
### TRTC의 비디오 서버는 대역폭을 최대 얼마까지 지원하나요?
제한이 없습니다.


[](id:que15)
### TRTC는 사유화 배포를 지원하나요?
현재는 지원하지 않습니다.

[](id:que16)
### TRTC에서 릴레이 라이브 방송 활성화 시 도메인은 ICP비안이 필요한가요?
릴레이 라이브 방송을 활성화하고자 할 경우, 재생 도메인은 중국 관련 부처의 규정에 따라 ICP비안이 있어야 사용할 수 있습니다. 자세한 내용은 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242)을 참조하십시오.

[](id:que17)
### TRTC는 대략 어느 정도 딜레이되나요?
글로벌 end to end로 평균 300ms 미만으로 딜레이됩니다.

[](id:que18)
### TRTC는 액티브 콜 기능을 지원하나요?
신호 터널을 결합해야 합니다. 예를 들어 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/product/im) 서비스의 사용자 정의 메시지를 사용하여 호출할 수 있습니다. [SDK](https://intl.cloud.tencent.com/document/product/647/34615) 소스 코드의 시나리오 Demo 사례를 참조하십시오.

[](id:que19)
### TRTC의 2인 영상 통화는 블루투스 이어폰을 지원하나요?
지원합니다.


[](id:que20)
### TRTC는 해외 사용을 지원하나요?
지원합니다.

[](id:que21)
### TRTC의 PC 액세스에 화면 공유 기능을 지원하나요?
지원합니다. 다음 문서를 참조하십시오.
- [화면 공유(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [화면 공유(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [화면 공유(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35163)

화면 공유 인터페이스에 대한 자세한 내용은 [Windows(C++) API](https://intl.cloud.tencent.com/document/product/647/35131) 또는 [Windows(C#) API](https://intl.cloud.tencent.com/document/product/647/35136)를 참조하십시오. 그 외 [Electron 인터페이스](https://intl.cloud.tencent.com/document/product/647/35141)를 사용할 수도 있습니다.

[](id:que23)
### 로컬 비디오 파일의 TRTC 공유를 지원하나요?

지원합니다. [사용자 정의 컬렉션](https://intl.cloud.tencent.com/document/product/647/35158) 기능으로 실현할 수 있습니다.

[](id:que24)
### TRTC에서 라이브 방송 비디오 녹화 후 휴대폰 로컬에 저장할 수 있나요?
휴대폰 로컬 저장은 지원하지 않습니다. 녹화 후 비디오 파일은 기본적으로 VOD 플랫폼에 저장되며 자체적으로 다운로드하여 휴대폰에 저장할 수 있습니다. 자세한 내용은 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426)을 참조하십시오.


[](id:que25)
### TRTC는 실시간 퓨어 오디오를 지원하나요?
퓨어 오디오를 지원합니다.


[](id:que26)
### 한 개의 방에서 동시에 몇 개 채널의 화면을 공유할 수 있나요?
현재 한 개의 방에서 한 채널의 서브스트림 화면만 공유할 수 있습니다.

[](id:que27)
### 창 공유(SourceTypeWindow) 지정 시, 창의 크기가 달라질 경우 비디오 스트림의 해상도도 변경되나요?
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 인코딩 매개변수를 조정합니다.
해상도 고정이 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 인코딩 매개변수를 설정하거나 startScreenCapture 호출 시 상응하는 인코딩 매개변수를 지정해야 합니다.


[](id:que28)
### TRTC는 1080P를 지원하나요?
지원합니다. SDK의 비디오 인코딩 매개변수 setVideoEncoderParam을 통해 해상도를 설정할 수 있습니다.

[](id:que29)
### TRTC는 사용자 정의 데이터 컬렉션이 가능한가요?
일부 플랫폼에서만 지원합니다. 자세한 내용은 [사용자 정의 컬렉션 및 렌더링](https://intl.cloud.tencent.com/document/product/647/35158)을 참조하십시오.

[](id:que30)
### TRTC는 ILVB SDK와의 통신이 가능한가요?
불가능합니다.

[](id:que31)
### TRTC는 MLVB와의 통신이 가능한가요? 
TRTC는 MLVB와 백그라운드 솔루션 아키텍처가 달라 직접적인 상호 통신을 지원하지 않습니다. TRTC 백그라운드에서 CDN으로의 릴레이 푸시 스트림만 가능합니다.



[](id:que32)
### TRTC 방 입장 모드 AppScene은 무엇이 다른가요?
TRTC는 4가지의 방 입장 모드를 지원합니다. 그중 영상 통화(VideoCall), 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 라이브 방송 모드라고 부릅니다.
- 통화 모드의 TRTC는 단일 방에 최대 300명이 동시 접속할 수 있으며 최대 30명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.
- 라이브 방송 모드의 TRTC는 단일 방에 최대 10만 명이 동시에 접속할 수 있으며 300ms 미만의 마이크 연결 딜레이 및 1000ms 미만의 시청 딜레이, 매끄러운 마이크 켜짐/꺼짐 등의 기능을 갖추고 있습니다. 저 딜레이 ILVB, 10만 인터랙션 강의, 화상 소개팅, 온라인 교육, 원격 교육, 초대형 회의 등의 응용 시나리오에 적합합니다.


[](id:que33)
### TRTC는 멀티미디어 통화 핸즈프리 모드를 지원하나요?
지원합니다. 핸즈프리 모드는 음성 라우팅 설정을 통해 활성화되며, Native SDK는 setAudioRoute 인터페이스를 통해 전환합니다.

[](id:que34)
### TRTC는 음량 크기 알림을 지원하나요?
지원합니다. enableAudioVolumeEvaluation 인터페이스를 통해 활성화됩니다.

[](id:que35)
###  TRTC는 이미지 화면 설정을 지원하나요? 
지원합니다. setLocalViewMirror 인터페이스를 통해 로컬 카메라 미리보기 화면의 이미지 모드를 설정하거나 setVideoEncoderMirror 인터페이스를 통해 인코더 출력 화면 이미지 모드를 설정합니다.

[](id:que36)
### TRTC는 통화 시의 음성을 로컬 파일에 녹음하는 기능을 지원하나요? 
지원합니다. startAudioRecording 인터페이스를 통해 통화 시의 모든 음성(로컬 음성, 원격 음성, BGM 등 포함)을 하나의 파일에 녹음할 수 있습니다. 현재 지원되는 음성 포맷으로는 PCM, WAV, AAC가 있습니다.

[](id:que37)
### TRTC는 멀티미디어 통신 시의 비디오를 파일로 녹화하는 기능을 지원하나요?
자체 서버 녹화(녹음/녹화)를 지원합니다. 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)로 문의하시면 SDK 및 관련 가이드를 제공합니다.
[클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426)을 사용하여 비디오를 녹화할 수 있습니다.

[](id:que38)
### TRTC는 WeChat 영상 통화처럼 플로팅 창, 화면 크기 변경 등 기능을 지원하나요?
해당 기능은 UI 레이아웃 로직으로, SDK에서 UI상의 표시 프로세스를 제한하지 않습니다. 공식 홈페이지 Demo에서 화면 전후 스택 및 아홉 개 칸 레이아웃 모드의 예시 코드를 제공하고 있으며, 플로팅 창, 화면 크기 변경, 화면 드래그를 지원합니다. 자세한 내용은 [공식 홈페이지 Demo](https://github.com/tencentyun/TRTCSDK)를 참조하십시오.

[](id:que39)
### TRTC는 퓨어 오디오 통화를 어떻게 하나요?
TRTC는 음성과 비디오 터널의 구분이 없으므로 startLocalAudio만 호출하고 startLocalPreview를 호출하지 않으면 퓨어 오디오 통화 모드가 됩니다.

[](id:que40)
### TRTC 퓨어 오디오 통화는 릴레이 푸시 스트림 및 녹화를 어떻게 하나요?
- 6.9 이전 버전: 방 입장 시 `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}`을 생성하여 TRTCParams.businessInfo에 전송해야 합니다. 1은 릴레이 푸시 스트림을, 2는 릴레이 푸시 스트림+녹화를 의미합니다.
- TRTC SDK 6.9 및 이후 버전: 방 입장 시 시나리오 매개변수로 TRTCAppSceneAudioCall 또는 TRTCAppSceneVoiceChatRoom을 선택하면 됩니다.

[](id:que41)
### TRTC 방에서 강제 퇴장, 발언 금지, 음소거 기능을 지원하나요?  
지원합니다.
- 간단한 조작 명령인 경우 TRTC의 사용자 정의 명령 인터페이스 sendCustomCmdMsg를 사용해 개발자가 해당 제어 명령을 사용자 정의할 수 있으며, 제어 명령을 수신하는 통화 상대방이 해당 조작을 실행하면 됩니다. 예를 들어 강제 퇴장의 경우 강제 퇴장 명령을 정의하면 되며, 해당 명령을 수신한 사용자는 자동으로 방에서 퇴장하게 됩니다.
- 더 완벽한 조작 로직이 필요한 경우 개발자가 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/document/product/1047)을 통해 관련 로직을 실현하는 것이 좋습니다. TRTC의 방과 IM 그룹을 매핑하고 IM 그룹에서 사용자 정의 정보를 수신/발신해 해당 조작을 실행하십시오.

[](id:que42)
### TRTC는 RTMP/FLV 스트림의 풀 스트림 재생을 지원하나요?  
지원합니다. 현재 TRTC SDK에는 TXLivePlayer가 포함되어 있습니다. 더 많은 플레이어 기능이 필요할 경우 모든 기능을 포함한 LiteAVSDK_Professional 버전을 사용하면 됩니다.

[](id:que43)
### TRTC는 최대 몇 명의 동시 통화를 지원하나요?
- 통화 모드에서는 단일 방에 최대 300명까지 동시 접속이 가능하며 최대 30명까지 동시에 카메라 또는 마이크를 활성화할 수 있습니다.
- 라이브 방송 모드에서는 당일 방에 10만 명 이상이 시청자로 접속하여 시청할 수 있으며, 최대 30명까지 호스트로 카메라 또는 마이크를 활성화할 수 있습니다.


[](id:que44)
### TRTC는 라이브 방송 시나리오 애플리케이션을 어떻게 실행하나요?
TRTC는 온라인 라이브 방송 시나리오 전용으로 10만 명 저딜레이 ILVB 솔루션을 출시했습니다. 이를 통해 호스트와 마이크가 연결된 호스트의 최저 딜레이 시간은 200ms 이내, 일반 시청자의 딜레이 시간은 1s 이내로 보장합니다. 또한 허술한 네트워크를 강력하게 보완하는 기술을 통해 복잡한 모바일 네트워크 환경에 대응합니다.
자세한 작업 가이드는 [라이브 방송 모드 실행](https://intl.cloud.tencent.com/document/product/647/35107)을 참조하십시오.

[](id:que45)
### TRTC 사용자 정의 메시지 발송 인터페이스로 채팅방, 댓글 자막 등의 기능을 사용할 수 있나요?
불가능합니다. TRTC 사용자 정의 메시지 발송은 간단한 저주파 신호 전송 시나리오에 적용됩니다. 자세한 내용은 [사용 제한](https://intl.cloud.tencent.com/document/product/647/35159)을 참조하십시오.

[](id:que46)
### TRTC SDK는 배경음 재생 시 순환 재생을 지원하나요? 배경음 재생 조정을 지원하나요?  
지원합니다. 순환 재생은 콜백 완료 후 다시 재생을 호출할 수 있으며, 재생 조정은 TXAudioEffectManager seekMusicToPosInMS를 통해 설정할 수 있습니다.

>?  setBGMPosition()는 v7.3 버전에서 사용 지원이 중단되고 TXAudioEffectManager seekMusicToPosInMS로 대체되었습니다.

[](id:que47)
### TRTC에는 방 멤버의 방 출입 수신 콜백이 있나요? onUserEnter/onUserExit를 사용할 수 있나요?
있습니다. TRTC는 onRemoteUserEnterRoom/onRemoteUserLeaveRoom을 사용하여 방 멤버의 방 출입을 수신합니다(업스트림 멀티미디어 권한을 보유한 사용자만 트리거 가능).
>?onUserEnter/onUserExit는 6.8 버전에서 사용 지원이 중단되어 onRemoteUserEnterRoom/onRemoteUserLeaveRoom으로 대체되었습니다.

[](id:que48)
### TRTC에서 연결 차단과 재연결을 어떻게 모니터링하나요?
다음 콜백을 통해 수신합니다.
- onConnectionLost: SDK와 서버의 연결 끊김
- onTryToReconnect: SDK의 서버 재연결 시도
- onConnectionRecovery: SDK와 서버의 연결 복구

[](id:que49)
### TRTC에 첫 프레임 렌더링 콜백이 있나요? 화면 렌더링 시작, 음성 재생 시작을 수신할 수 있나요?
지원합니다. onFirstVideoFrame/onFirstAudioFrame을 통해 수신할 수 있습니다.

[](id:que50)
### TRTC는 비디오 화면 캡처 기능을 지원하나요?
현재 iOS/Android에서 snapshotVideo()를 호출하여 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.

[](id:que51)
### TRTC에서 블루투스 이어폰 등 주변기기 액세스 오류가 발생하는 이유는 무엇인가요?
현재 TRTC는 주로 사용되는 블루투스 이어폰 및 주변 기기와 호환이 되나 일부 디바이스에서 호환 문제가 발생하고 있습니다. 공식 홈페이지 Demo 및 WeChat, QQ 멀티미디어 통화로 정상 호환 여부 확인을 권장합니다.

[](id:que52)
### TRTC 멀티미디어의 업스트림/다운스트림 비트 레이트, 해상도, 패킷 손실률, 오디오 샘플링 레이트 등의 정보를 어떻게 획득하나요?
SDK 인터페이스 onStatistics()를 통해 해당 통계 정보를 획득할 수 있습니다.

[](id:que53)
### TRTC 배경 음악 재생 인터페이스 playBGM()은 온라인 음악을 지원하나요?
현재는 로컬 음악만을 지원하며, 먼저 로컬에 다운로드한 후 playBGM()을 호출하여 재생할 수 있습니다.

[](id:que54)
### TRTC는 로컬 음량 컬렉션 설정을 지원하나요? 원격 사용자의 재생 음량 설정을 지원하나요?
지원합니다. setAudioCaptureVolume() 인터페이스를 통해 SDK의 음량 컬렉션을 설정할 수 있으며, setRemoteAudioVolume() 인터페이스를 통해 원격 사용자의 재생 음량을 설정할 수 있습니다.

[](id:que55)
### stopLocalPreview와 muteLocalVideo의 차이점은 무엇인가요?
- stopLocalPreview는 로컬 비디오 수집을 중단합니다. 이 인터페이스를 호출하면 로컬 및 원격 화면에 블랙 스크린 현상이 나타납니다.
- muteLocalVideo는 백그라운드에 비디오 화면 발송 여부를 설정합니다. 이 인터페이스를 호출하면 다른 이용자가 시청하는 화면에는 블랙 스크린 현상이 나타나며 로컬의 미리보기에서는 화면을 볼 수 있습니다.

[](id:que56)
### stopLocalAudio와 muteLocalAudio의 차이점은 무엇인가요? 
- stopLocalAudio는 로컬 오디오의 수집 및 업스트림을 차단합니다.
- muteLocalAudio는 멀티미디어 데이터 발송을 멈추지 않으며, 비트 레이트가 매우 낮은 음소거 패키지를 계속해서 발송합니다.

[](id:que57)
### TRTC SDK는 어떤 해상도를 지원하나요?
[화질 설정](https://intl.cloud.tencent.com/document/product/647/35153)을 참조하여 해상도 설정으로 화질을 최적화할 수 있습니다.

[](id:que58)
### TRTC SDK는 업스트림 비디오 비트 레이트, 해상도, 프레임 레이트를 어떻게 설정하나요? 
TRTCCloud의 setVideoEncoderParam() 인터페이스를 통해 TRTCVideoEncParam 매개변수 중 videoResolution(해상도), videoFps(프레임 레이트), videoBitrate(비트 레이트)를 설정할 수 있습니다.

[](id:que59)
### SDK의 화면 각도 및 방향 제어는 어떻게 이루어지나요?  
자세한 내용은 [비디오 화면 회전 및 축소/확대](https://intl.cloud.tencent.com/document/product/647/35154)를 참조하십시오.

[](id:que60)
### 가로 모드 영상 통화는 어떻게 하나요? 
자세한 내용은 [비디오 화면 회전 및 축소/확대](https://intl.cloud.tencent.com/document/product/647/35154)를 참조하십시오.

[](id:que61)
### TRTC 로컬과 원격 화면 방향이 불일치할 경우 어떻게 조정하나요?  
자세한 내용은 [비디오 화면 회전 및 축소/확대](https://intl.cloud.tencent.com/document/product/647/35154)를 참조하십시오.


[](id:que62)
### TRTC에는 화질(비트 레이트, 해상도, 프레임 레이트) 관련 권장하는 매개변수 설정이 있나요?
자세한 내용은 [권장 설정](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE)을 참조하십시오.

[](id:que63)
### TRTC는 네트워크 속도 테스트를 지원하나요? 어떻게 조작하나요?  
자세한 내용은 [통화 전 네트워크 속도 테스트](https://intl.cloud.tencent.com/document/product/647/35156)를 참조하십시오.

[](id:que64)
### TRTC는 방에 대한 권한 인증을 지원하나요(예: 회원만 입장할 수 있는 시나리오인지)? 
지원합니다. 자세한 내용은 [방 입장 권한 보호](https://intl.cloud.tencent.com/document/product/647/35157)를 참조하십시오.

[](id:que65)
### TRTC 멀티미디어 스트리밍은 CDN 풀 스트림 시청을 지원하나요? 
지원합니다. 자세한 내용은 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242)을 참조하십시오.

[](id:que66)
### TRTC 사용자 정의 렌더링은 어떤 포맷을 지원하나요? 
- iOS에서는 i420, NV12, BGRA를 지원합니다.
- Android에서는 I420과 texture2d를 지원합니다.
