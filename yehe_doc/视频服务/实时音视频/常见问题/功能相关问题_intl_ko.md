<span id="que1"></span>
### TRTC RoomID는 무엇입니까? 값의 범위는 어떻게 됩니까?
RoomID는 방 번호로 방의 단일 식별자로 사용됩니다. 방 번호 값 범위는 1~4294967295로 개발자가 점검 및 할당합니다.

<span id="que2"></span>
### TRTC 방 입장 UserID는 무엇입니까? 길이와 조건은 어떻게 됩니까? 
UserID는 사용자 ID로 TRTC 앱에서 사용자 단일 식별자로 사용됩니다. 길이는 32바이트 이하를 권장합니다. 알파벳(대소문자 구별 없음), 숫자 또는 언더바를 사용합니다.


<span id="que3"></span>
### TRTC 방의 라이프사이클은 어떻게 됩니까?
- 최초 방 입장자가 해당 방의 소유자지만 소유자가 직접 방을 삭제할 수 없습니다.
- 모든 사용자들이 현재 방에서 퇴장하면 방이 즉시 사라집니다.
- 방의 개별 사용자가 오류로 인해 접속이 끊긴 경우 30초 후 서버에서 해당 사용자를 현재 방에서 퇴장시킵니다. 방의 모든 사용자가 오류로 인해 접속이 끊긴 경우 30초 후 서버에서 현재 방을 자동으로 삭제합니다.
- 사용자가 입장하고자 하는 방이 없을 경우 백그라운드에서 방이 자동으로 생성됩니다.

<span id="que4"></span>
### TRTC에서 비구독 멀티미디어 스트리밍을 지원합니까? 
“바로 재생”을 위해 방 입장 시 자동으로 스트리밍을 구독하게 되며, setDefaultStreamRecvMode 인터페이스를 통해 수동으로 구독 모드를 전환할 수 있습니다.

<span id="que5"></span>
### TRTC에서 사용자 정의 릴레이 푸시 스트리밍의 스트리밍 ID를 지원합니까?  
지원합니다. enterRoom의 매개변수 TRTCParams로 streamId를 지정할 수 있으며, startPublishing 인터페이스를 호출하여 매개변수 streamId를 전송할 수도 있습니다.

<span id="que6"></span>
### TRTC 라이브 방송은 어떤 역할을 지원하며, 어떤 차이가 있습니까?
라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)는 TRTCRoleAnchor(호스트)와 TRTCRoleAudience(관객)이라는 두 가지 역할을 지원합니다. 호스트 역할은 멀티미디어 데이터를 동시에 업스트림, 다운스트림할 수 있으며, 관객 역할은 다른 사람의 데이터를 다운스트림 재생만 할 수 있습니다. switchRole() 호출을 통해 역할을 교체할 수 있습니다.

<span id="que7"></span>
### TRTC의 역할(Role)을 어떻게 이해하면 됩니까? 
라이브 방송에서 호스트와 관객의 역할을 설정할 수 있습니다. 호스트 역할 TRTCRoleAnchor은 멀티미디어 업스트림, 다운스트림 권한을 가지고 있으며 동시에 최대 30명까지 가능합니다. 관객 TRTCRoleAudience는 멀티미디어 다운스트림 권한만을 가지고 있으며 동시에 최대 10만 명까지 가능합니다.
>? 웹에서는 최대 20명이 동시에 카메라 또는 마이크를 활성화할 수 있도록 지원합니다.


<span id="que8"></span>
### TRTC 방에서 어떤 응용 시나리오를 지원합니까?  
다음 시나리오를 지원합니다.
- TRTCAppSceneVideoCall: 비디오 통화 시나리오. 일대일 비디오 통화, 300인 화상 회의, 온라인 진료, 화상 채팅, 원격 면접 등에 적합합니다.
- TRTCAppSceneLIVE: 비디오 ILVB. 비디오 저 딜레이 라이브 방송, 10만 인터랙션 강의, 비디오 라이브 방송 PK, 화상 소개팅, 인터랙션 강의, 원격 교육, 초대형 회의 등에 적합합니다.
- TRTCAppSceneAudioCall: 음성 통화 시나리오. 일대일 음성 통화, 300인 음성 회의, 음성 채팅, 음성 회의, 온라인 마피아 게임 등에 적합합니다.
- TRTCAppSceneVoiceChatRoom: 음성 ILVB. 음성 저 딜레이 라이브 방송, 음성 라이브 방송 마이크 연결, 음성 채팅, 노래방, FM 라디오 등에 적합합니다.


<span id="que9"></span>
### TRTC에서 지원하는 플랫폼에는 어떤 것이 있습니까?
iOS, Android, Windows(C++), Windows(C#), Mac, 데스크톱 브라우저, Electron, Linux 서버 등의 플랫폼을 지원합니다. 자세한 내용은 [플랫폼 지원](https://intl.cloud.tencent.com/document/product/647/35078)을 참조하십시오.

<span id="que10"></span>
### TRTC의 라이트 버전, 프로 버전, 엔터프라이즈 버전 등 각 버전의 차이점은 무엇입니까? 
자세한 내용은 [각 버전 차이 대조표](https://intl.cloud.tencent.com/document/product/647/34615)를 참조하십시오.


<span id="que11"></span>
### TRTC에서 라이브 방송 마이크 연결을 지원합니까?
지원합니다. 운영 가이드를 참조하십시오.
- [온라인 라이브 방송(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)
- [온라인 라이브 방송(Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [온라인 라이브 방송(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [온라인 라이브 방송(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35110)


<span id="que12"></span>
### TRTC는 동시에 최대 몇 개의 방을 생성할 수 있습니까?
동시에 4294967294개의 방이 존재할 수 있으며, 누적 방 수량에는 제한이 없습니다.

<span id="que13"></span>
### 방은 어떻게 생성합니까?
방은 Tencent Cloud 백그라운드에서 클라이언트 방 입장 시 자동으로 생성합니다. 수동으로 생성할 필요 없이 클라이언트의 관련 인터페이스 “방 입장”을 호출하면 됩니다.
- [iOS & Mac > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows（C++） > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)
- [Windows（C#） > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b)
- [Electron > enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?_ga=1.212321108.1562552652.1542703643#enterRoom)
- [데스크톱 브라우저 > join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html?_ga=1.256770123.1562552652.1542703643#join)

<span id="que14"></span>
### TRTC의 비디오 서버는 대역폭을 최대 얼마까지 지원합니까?
제한이 없습니다.


<span id="que15"></span>
### TRTC는 사유화 배포를 지원합니까?
현재는 지원하지 않습니다.

<span id="que16"></span>
### TRTC에서 릴레이 라이브 방송 활성화 시 도메인은 ICP비안이 필요합니까?
릴레이 라이브 방송을 활성화하고자 할 경우 중국 관련 부처의 규정에 따라 중국대륙의 재생 도메인은 ICP비안이 있어야 사용할 수 있습니다. 자세한 내용은 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242)을 참조하십시오.

<span id="que17"></span>
### TRTC는 대략 어느 정도 딜레이됩니까?
글로벌 end to end로 평균 300ms 미만으로 딜레이됩니다.

<span id="que18"></span>
### TRTC는 액티브 콜 기능을 지원합니까?
신호 터널을 결합해야 합니다. 예를 들어 [인스턴트 메시징 IM](https://intl.cloud.tencent.com/product/im) 서비스의 사용자 정의 메시지를 사용하여 호출할 수 있습니다. [SDK](https://intl.cloud.tencent.com/document/product/647/34615) 소스 코드의 시나리오 Demo 사례를 참조하십시오.

<span id="que19"></span>
### TRTC의 2인 비디오 통화는 블루투스 이어폰을 지원합니까?
지원합니다.


<span id="que20"></span>
### TRTC는 국외 사용을 지원합니까?
지원합니다.

<span id="que21"></span>
### TRTC의 PC 액세스에 화면 공유 기능을 지원합니까?
지원합니다. 다음 문서를 참조하십시오.
- [화면 공유(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [화면 공유(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [화면 공유(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/35163)

화면 공유 인터페이스에 대한 자세한 내용은 [Windows(C++) API](https://intl.cloud.tencent.com/document/product/647/35131) 또는 [Windows(C#) API](https://intl.cloud.tencent.com/document/product/647/35136)를 참조하십시오. 그 외 [Electron 인터페이스](https://intl.cloud.tencent.com/document/product/647/35141)를 사용할 수도 있습니다.

<span id="que23"></span>
### 로컬 비디오 파일의 TRTC 공유를 지원합니까?

지원합니다. [사용자 정의 컬렉션](https://intl.cloud.tencent.com/document/product/647/35158) 기능으로 실현할 수 있습니다.

<span id="que24"></span>
### TRTC에서 라이브 방송 비디오 녹화 후 휴대폰 로컬에 저장할 수 있습니까?
휴대폰 로컬 저장은 지원하지 않습니다. 녹화 후 비디오 파일은 VOD 플랫폼에 저장되며 자체적으로 다운로드하여 휴대폰에 저장할 수 있습니다. 자세한 내용은 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426)을 참조하십시오.


<span id="que25"></span>
### TRTC는 실시간 퓨어 오디오를 지원합니까?
퓨어 오디오를 지원합니다.


<span id="que26"></span>
### 방에서는 동시에 몇 개 채널의 화면을 공유할 수 있습니까?
현재 방에서는 한 채널의 서브스트림 화면만 공유할 수 있습니다.

<span id="que27"></span>
### 지정 창 공유(SourceTypeWindow) 시 창의 크기가 달라질 경우 비디오 스트리밍의 해상도도 변경됩니까?
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 코드 매개변수를 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 코딩 매개변수를 설정하거나 startScreenCapture 호출 시 해당 코딩 매개변수를 지정해야 합니다.


<span id="que28"></span>
### TRTC는 1080P를 지원합니까?
지원합니다. SDK의 비디오 코딩 매개변수 setVideoEncoderParam을 통해 해상도를 설정할 수 있습니다.

<span id="que29"></span>
### TRTC는 사용자 정의 데이터 컬렉션이 가능합니까?
일부 플랫폼에서만 지원합니다. 자세한 내용은 [사용자 정의 컬렉션 및 렌더링](https://intl.cloud.tencent.com/document/product/647/35158)을 참조하십시오.

<span id="que30"></span>
### TRTC는 LVB SDK와의 통신이 가능합니까?
불가능합니다.

<span id="que31"></span>
### TRTC는 MLVB와의 통신이 가능합니까? 
TRTC는 MLVB와 백그라운드 솔루션 아키텍처가 달라 직접적인 상호 통신을 지원하지 않습니다. TRTC에서 CDN으로의 릴레이 푸시 스트리밍만이 가능합니다.



<span id="que32"></span>
### TRTC 방 입장 모드 AppScene은 무엇이 다릅니까?
TRTC는 4가지 모드를 지원합니다. 그중 비디오 통화(VideoCall), 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 라이브 방송 모드라고 부릅니다.
- 통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 30명이 동시에 발언할 수 있습니다. 일대일 비디오 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.
- 라이브 방송 모드의 TRTC는 단일 방에 최대 10만 명이 동시에 접속할 수 있으며 300ms 미만의 마이크 연결 딜레이 및 1000ms 미만의 시청 딜레이, 상하 이동 마이크 꺼짐 등의 기능을 갖추고 있습니다. 저 딜레이 ILVB, 10만 인터랙션 강의, 화상 소개팅, 온라인 교육, 원격 교육, 초대형 회의 등의 응용 시나리오에 적합합니다.

>? 웹에서는 최대 20명이 동시에 카메라 또는 마이크를 활성화할 수 있도록 지원합니다.

<span id="que33"></span>
### TRTC는 멀티미디어 통화 핸즈프리 모드를 지원합니까?
지원합니다. 핸즈프리 모드는 음성 라우팅 설정을 통해 실현하며, Native SDK는 setAudioRoute 인터페이스를 통해 전환합니다.

<span id="que34"></span>
### TRTC는 음량 크기 알림을 지원합니까?
지원합니다. enableAudioVolumeEvaluation 인터페이스를 통해 활성화합니다.

<span id="que35"></span>
###  TRTC는 이미지 화면 설정을 지원합니까? 
지원합니다. setLocalViewMirror 인터페이스를 통해 로컬 카메라 미리보기 화면의 이미지 모드를 설정하거나 setVideoEncoderMirror 인터페이스를 통해 인코더 출력 화면 이미지 모드를 설정합니다.

<span id="que36"></span>
### TRTC는 통화 시의 음성을 로컬 파일에 녹음하는 기능을 지원합니까? 
지원합니다. startAudioRecording 인터페이스를 통해 통화 시의 모든 음성(로컬 음성, 원격 음성, BGM 등 포함)을 하나의 문서에 녹음할 수 있습니다. 현재 지원되는 음성 포맷으로는 PCM, WAV, AAC가 있습니다.

<span id="que37"></span>
### TRTC는 멀티미디어 통신 시의 비디오를 파일로 녹화하는 기능을 지원합니까?
자체 서버 녹화(녹음/녹화)를 지원합니다. 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)로 문의하시면 SDK 및 관련 가이드를 제공합니다.
[클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426)을 사용하여 비디오를 녹화할 수 있습니다.

<span id="que38"></span>
### TRTC는 WeChat 비디오 통화처럼 플로팅 창, 화면 크기 변경 등 기능을 지원합니까?
해당 기능은 UI 레이아웃 로직으로 SDK에서 UI상의 표시 프로세스를 제한하지 않습니다. 공식 홈페이지 Demo에서 화면 전후 스택 및 아홉 개 칸 레이아웃 모드의 예시 코드를 제공하고 있으며, 플로팅 창, 화면 크기 변경, 화면 드래그를 지원합니다. 자세한 내용은 [공식 홈페이지 Demo](https://github.com/tencentyun/TRTCSDK)를 참조하십시오.

<span id="que39"></span>
### TRTC는 어떻게 음성 통화를 실현합니까?
TRTC는 음성과 비디오 터널의 구분이 없어 startLocalAudio만 호출하고 startLocalPreview를 호출하지 않으면 음성 통화 모드가 됩니다.

<span id="que40"></span>
### TRTC 음성 통화는 어떻게 릴레이 푸시 스트리밍 및 녹화를 실현합니까?
- 6.9 이전 버전: 방 입장 시 `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}`을 생성하여 TRTCParams.businessInfo에 전송해야 합니다. 1은 릴레이 푸시 스트리밍을, 2는 릴레이 푸시 스트리밍+녹화를 나타냅니다.
- TRTC SDK 6.9 및 이후 버전: 방 입장 시 시나리오 매개변수로 TRTCAppSceneAudioCall 또는 TRTCAppSceneVoiceChatRoom을 선택하면 됩니다.

<span id="que41"></span>
### TRTC 방에서 강제 퇴장, 발언 금지, 음소거 기능을 지원합니까?  
지원합니다.
- 간단한 조작 명령인 경우 TRTC의 사용자 정의 명령 인터페이스 sendCustomCmdMsg를 사용해 개발자가 해당 제어 명령을 사용자 정의할 수 있으며, 제어 명령을 수신하는 통화 상대방이 해당 조작을 실행하면 됩니다. 예를 들어 강제 퇴장의 경우 강제 퇴장 명령을 정의하면 되며, 해당 명령을 수신한 사용자는 스스로 방을 퇴장하게 됩니다.
- 더 완벽한 조작 로직이 필요한 경우 개발자가 [인스턴트 메시징 IM](https://intl.cloud.tencent.com/document/product/1047)을 통해 관련 로직을 실현하는 것이 좋습니다. TRTC의 방과 IM 그룹을 매핑하고 IM 그룹에서 사용자 정의 정보를 수신/발신해 해당 조작을 실현하십시오.

<span id="que42"></span>
### TRTC는 RTMP/FLV 스트리밍의 풀 스트리밍 재생을 지원합니까?  
지원합니다. 현재 TRTC SDK에는 TXLivePlayer가 포함되어 있습니다. 더 많은 플레이어 기능이 필요할 경우 LiteAVSDK_Professional 버전을 사용하면 전체 기능을 포함합니다.

<span id="que43"></span>
### TRTC는 최대 몇 명의 동시 통화를 지원합니까?
- 통화 모드에서는 한 방에 최대 300명까지 동시 접속이 가능하며 최대 30명까지 동시에 카메라 또는 마이크를 활성화할 수 있습니다.
- 라이브 방송 모드에서는 한 방에 10만 명 이상이 관객 자격으로 접속하여 시청할 수 있으며, 최대 30명까지 호스트 자격으로 카메라 또는 마이크를 활성화할 수 있습니다.

>? 웹에서는 최대 20명이 동시에 카메라 또는 마이크를 활성화할 수 있도록 지원합니다.

<span id="que44"></span>
### TRTC는 라이브 방송 시나리오 애플리케이션을 어떻게 실행합니까?
TRTC는 온라인 라이브 방송 시나리오 전용으로 10만 명 참여 시의 ILVB 저 딜레이 솔루션을 출시했으며, 이를 통해 호스트와 마이크가 연결된 호스트의 최저 딜레이 시간은 200ms 이내, 일반 관객의 딜레이 시간은 1s 이내로 보장합니다. 또한 약한 네트워크 보완 기술을 통해 복잡한 모바일 네트워크 환경에 대응합니다.
자세한 작업 가이드는 [라이브 방송 모드 실행](https://intl.cloud.tencent.com/document/product/647/35107)을 참조하십시오.

<span id="que45"></span>
### TRTC 사용자 정의 메시지 발송 인터페이스로 채팅방, 댓글 자막 등의 기능을 사용할 수 있습니까?
불가능합니다. TRTC 사용자 정의 메시지 발송은 간단한 저주파 신호 전송 시나리오에 적용됩니다. 자세한 내용은 [사용 제한](https://intl.cloud.tencent.com/document/product/647/35159)을 참조하십시오.

<span id="que46"></span>
### TRTC SDK는 배경음 재생 시 순환 재생을 지원합니까? 배경음의 재생 진행 상황 조정을 지원합니까?  
지원합니다. 순환 재생 희망 시 콜백 완료 후 다시 재생을 호출할 수 있으며, 재생 진행 상황은 setBGMPosition()을 통해 설정할 수 있습니다.

<span id="que47"></span>
### TRTC에는 방 멤버의 방 출입 리슨 콜백이 있습니까? onUserEnter/onUserExit를 사용할 수 있습니까?
있습니다. TRTC는 onRemoteUserEnterRoom/onRemoteUserLeaveRoom을 사용하여 방 멤버의 방 출입을 리슨합니다(업스트림 멀티미디어 권한을 보유한 사용자가 트리거할 수 있음).
>?onUserEnter/onUserExit는 6.8 버전에서 사용 지원이 중단되어 onRemoteUserEnterRoom/onRemoteUserLeaveRoom으로 대체합니다.

<span id="que48"></span>
### TRTC에서 연결 차단과 재연결을 어떻게 모니터링합니까?
다음 리스너 콜백을 통해 리슨합니다.
- onConnectionLost: SDK와 서버와의 연결 끊김
- onTryToReconnect: SDK의 서버와의 재연결 시도
- onConnectionRecovery: SDK와 서버의 연결 복구

<span id="que49"></span>
### TRTC에는 첫 번째 프레임 렌더링 콜백이 있습니까? 화면 렌더링 시작, 음성 재생 시작을 리슨할 수 있습니까?
지원합니다. onFirstVideoFrame/onFirstAudioFrame을 통해 리슨할 수 있습니다.

<span id="que50"></span>
### TRTC는 비디오 화면 캡처 기능을 지원합니까?
현재 iOS/Android에서 snapshotVideo()를 호출하여 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.

<span id="que51"></span>
### TRTC에서 블루투스 이어폰 등 주변기기 액세스 오류가 발생하는 이유는 무엇입니까?
현재 TRTC는 많이 사용되는 블루투스 이어폰 및 주변 기기와 호환이 되나 일부 디바이스에서는 호환 문제가 발생하고 있습니다. 공식 홈페이지 Demo 및 WeChat, QQ 멀티미디어 통화를 사용하여 정상 여부를 확인해 보십시오.

<span id="que52"></span>
### TRTC에서 멀티미디어의 업스트림 다운스트림 비트 레이트, 해상도, 패킷 손실률, 오디오 샘플링 레이트 등의 정보를 어떻게 획득합니까?
SDK 인터페이스 onStatistics()를 통해 해당 통계 정보를 획득할 수 있습니다.

<span id="que53"></span>
### TRTC 배경 음악 재생 인터페이스 playBGM()은 온라인 음악을 지원합니까?
현재는 로컬 음악만을 지원하며, 먼저 로컬에 다운로드한 후 playBGM()을 호출하여 재생할 수 있습니다.

<span id="que54"></span>
### TRTC는 로컬 음량 컬렉션 설정을 지원합니까? 원격 사용자의 재생 음량 설정을 지원합니까?
지원합니다. setAudioCaptureVolume() 인터페이스를 통해 SDK의 음량 컬렉션을 설정할 수 있으며, setRemoteAudioVolume() 인터페이스를 통해 원격 사용자의 재생 음량을 설정할 수 있습니다.

<span id="que55"></span>
### stopLocalPreview와 muteLocalVideo의 차이점은 무엇입니까?
- stopLocalPreview는 로컬 비디오 캡처를 중단합니다. 이 인터페이스를 호출하면 로컬 및 원격 화면에 블랙 스크린 현상이 나타납니다.
- muteLocalVideo는 백그라운드에 비디오 화면 발송할지 여부를 설정합니다. 이 인터페이스를 호출하면 다른 이용자가 시청하는 화면에는 블랙 스크린 현상이 나타나며 로컬의 미리보기에서는 화면을 볼 수 있습니다.

<span id="que56"></span>
### stopLocalAudio와 muteLocalAudio의 차이점은 무엇입니까? 
- stopLocalAudio는 로컬 오디오의 캡처 및 업스트림을 차단합니다.
- muteLocalAudio는 멀티미디어 데이터 발송을 멈추지 않으며, 비트 레이트가 매우 낮은 음소거 패키지를 계속해서 발송합니다.

<span id="que57"></span>
### TRTC SDK는 어떤 해상도를 지원합니까?
[화질 설정](https://intl.cloud.tencent.com/document/product/647/35153)을 참조하여 해상도를 설정해 화면을 최적화하는 것이 좋습니다.

<span id="que58"></span>
### TRTC SDK는 업스트림 비디오 비트 레이트, 해상도, 프레임 레이트를 어떻게 설정합니까? 
TRTCCloud의 setVideoEncoderParam() 인터페이스를 통해 TRTCVideoEncParam 매개변수 중 videoResolution(해상도), videoFps(프레임 레이트), videoBitrate(비트 레이트)를 설정할 수 있습니다.

<span id="que59"></span>
### SDK의 화면 각도 및 방향 제어는 어떻게 이루어집니까?  
자세한 내용은 [비디오 화면 회전 및 줌](https://intl.cloud.tencent.com/document/product/647/35154)을 참조하십시오.

<span id="que60"></span>
### 가로 모드 비디오 통화는 어떻게 실현합니까? 
자세한 내용은 [비디오 화면 회전 및 줌](https://intl.cloud.tencent.com/document/product/647/35154)을 참조하십시오.

<span id="que61"></span>
### TRTC 로컬과 원격 화면 방향이 불일치할 경우 어떻게 조정합니까?  
자세한 내용은 [비디오 화면 회전 및 줌](https://intl.cloud.tencent.com/document/product/647/35154)을 참조하십시오.


<span id="que62"></span>
### TRTC에는 권장하는 화질(비트 레이트, 해상도, 프레임 레이트) 관련 매개변수 설정이 있습니까?
자세한 내용은 [권장 설정](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE)을 참조하십시오.

<span id="que63"></span>
### TRTC는 네트워크 속도 테스트를 지원합니까? 어떻게 조작합니까?  
자세한 내용은 [통화 전 네트워크 속도 테스트](https://intl.cloud.tencent.com/document/product/647/35156)를 참조하십시오.

<span id="que64"></span>
### TRTC는 방에 대한 권한 인증을 지원합니까(예: 회원만 입장할 수 있는 시나리오)? 
지원합니다. 자세한 내용은 [방 입장 권한 보호](https://intl.cloud.tencent.com/document/product/647/35157)를 참조하십시오.

<span id="que65"></span>
### TRTC 멀티미디어 스트리밍은 CDN 풀 스트리밍 시청을 지원합니까? 
지원합니다. 자세한 내용은 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242)을 참조하십시오.

<span id="que66"></span>
### TRTC 사용자 정의 렌더링은 어떤 포맷을 지원합니까? 
- iOS에서는 i420, NV12, BGRA를 지원합니다.
- Android에서는 I420과 texture2d를 지원합니다.
