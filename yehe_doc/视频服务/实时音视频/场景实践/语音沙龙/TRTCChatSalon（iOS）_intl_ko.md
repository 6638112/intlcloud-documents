TRTCChatSalon은 Tencent Cloud의 Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 기반으로 구성된 모듈이며, 다음 기능을 지원합니다.

- 호스트가 신규 음성 살롱을 생성하면 시청자가 음성 살롱에 입장해 시청 및 인터랙션할 수 있습니다.
- 호스트가 시청자에게 마이크 켜기를 요청하거나 마이크가 켜진 사용자의 마이크를 강제로 끌 수 있습니다.
- 시청자가 마이크 켜기를 신청하여 마이크가 켜진 호스트가 될 수 있고, 다른 사람들과 음성으로 인터랙션할 수 있으며, 언제든지 마이크를 끄고 일반 시청자가 될 수 있습니다.
- 다양한 텍스트 메시지 및 사용자 정의 메시지를 지원합니다. 사용자 정의 메시지를 이용해 댓글 자막, 좋아요, 선물 기능 등을 구현할 수 있습니다.

TRTCChatSalon은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [음성 살롱(iOS)](https://intl.cloud.tencent.com/document/product/647/39803)을 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저딜레이 음성 채팅 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 AVChatroom을 이용해 채팅방 기능을 구현하며, IM 속성 인터페이스를 통해 마이크 위치 리스트 등 방 정보를 저장하고 초대 신호를 마이크 켜기/끄기 신청에 사용할 수 있습니다.


<span id="TRTCChatSalon"></span>

## TRTCChatSalon API 개요

### SDK 기본 함수

| API                                             | 설명                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | 단일 항목 객체 획득           |
| [destroySharedInstance](#destroysharedinstance) | 단일 항목 객체 폐기           |
| [setDelegate](#setdelegate)                     | 이벤트 콜백 설정           |
| [setDelegateQueue](#setdelegatequeue)           | 이벤트 콜백이 존재하는 스레드 설정 |
| [login](#login)                                 | 로그인                   |
| [logout](#logout)                               | 로그아웃                   |
| [setSelfProfile](#setselfprofile)               | 개인 정보 수정           |

### 방 관련 인터페이스 함수

| API                                 | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | 방 생성(호스트 호출). 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방 생성 |
| [destroyRoom](#destroyroom)         | 방 폐기(호스트 호출)                                       |
| [enterRoom](#enterroom)             | 방 입장(시청자 호출)                                       |
| [exitRoom](#exitroom)               | 방 퇴장(시청자 호출)                                       |
| [getRoomInfoList](#getroominfolist) | 방 리스트의 세부 정보 획득                                     |
| [getUserInfoList](#getuserinfolist) | 특정 userId의 사용자 정보 획득. nil인 경우 방 안에 있는 모든 사용자 정보 획득 |

### 마이크 켜짐/꺼짐 인터페이스

| API                     | 설명                               |
| ----------------------- | ---------------------------------- |
| [enterSeat](#enterseat) | 직접 마이크 켬(시청자와 호스트 모두 호출 가능) |
| [leaveSeat](#leaveseat) | 직접 마이크 끔(시청자와 호스트 모두 호출 가능) |
| [pickSeat](#pickseat)   | 특정 사용자 마이크 켬(호스트 호출)             |
| [kickSeat](#kickseat)   | 특정 사용자 마이크 끔(호스트 호출)             |

### 로컬 오디오 작업 인터페이스

| API                                             | 설명                 |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | 마이크 수집 시작     |
| [stopMicrophone](#stopmicrophone)               | 마이크 수집 종료     |
| [setAudioQuality](#setaudioquality)             | 오디오 품질 설정           |
| [muteLocalAudio](#mutelocalaudio)               | 로컬 음소거 활성화/비활성화  |
| [setSpeaker](#setspeaker)                       | 스피커 활성화 설정     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | 마이크 수집 음량 설정 |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 재생 음량 설정       |


### 원격 사용자 오디오 작업 인터페이스

| API                                       | 설명                    |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 특정 사용자 음소거/음소거 해제 |
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 사용자 음소거/음소거 해제 |

### 배경 음악 음향 효과 관련 인터페이스

| API                                             | 설명                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득 |

### 메시지 발송 관련 인터페이스

| API                                     | 설명                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용 |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송                     |

### 초대 신호 관련 인터페이스

| API                                   | 설명             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | 사용자에게 초대 발송 |
| [acceptInvitation](#acceptinvitation) | 초대 수락       |
| [rejectInvitation](#rejectinvitation) | 초대 거부       |
| [cancelInvitation](#cancelinvitation) | 초대 취소       |

<span id="TRTCChatSalonDelegate"></span>
## TRTCChatSalonDelegate API 개요

### 일반적인 이벤트 콜백

| API                       | 설명       |
| ------------------------- | ---------- |
| [onError](#onerror)       | 오류 콜백 |
| [onWarning](#onwarning)   | 경고 콜백 |
| [onDebugLog](#ondebuglog) | Log 콜백 |

### 방 이벤트 콜백

| API                                       | 설명                   |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | 방 폐기 콜백     |
| [onRoomInfoChange](#onroominfochange)     | 음성 채팅방 정보 변경 콜백 |
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 음량 콜백     |

### 마이크 위치 변경 콜백

| API                                            | 설명                                   |
| ---------------------------------------------- | -------------------------------------- |
| [onEnterRoomSeatListNotify](#onenterroomseatlistnotify) | 시청자 방 입장 후, 해당 방 호스트 정보 콜백 |
| [onAnchorEnterSeat](#onanchorenterseat)        | 사용자 마이크 켜짐(직접 마이크 켬/호스트가 특정 사용자 마이크 켬)  |
| [onAnchorLeaveSeat](#onanchorleaveseat)        | 사용자 마이크 꺼짐(직접 마이크 끔/호스트가 특정 사용자 마이크 끔)  |
| [onSeatMute](#onseatmute)                      | 호스트 마이크 음소거                             |

### 시청자 입장/퇴장 이벤트 콜백

| API                                 | 설명               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 공지 수신 |
| [onAudienceExit](#onaudienceexit)   | 시청자 퇴장 공지 수신 |

### 메시지 이벤트 콜백

| API                                         | 설명             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | 텍스트 메시지 수신   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신 |

### 신호 이벤트 콜백

| API                                               | 설명               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 새로운 초대 요청 수신 |
| [onInviteeAccepted](#oninviteeaccepted)           | 초대된 사용자가 초대 수락 |
| [onInviteeRejected](#oninviteerejected)           | 초대된 사용자가 초대 거부 |
| [onInvitationCancelled](#oninvitationcancelled)   | 초대한 사용자가 초대 취소   |

## SDK 기본 함수

<span id="sharedInstance"></span>

### sharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39803) 단일 항목 객체 획득

```Objective-C
/**
* TRTCChatSalon 단일 항목 객체 획득
*
* - returns: TRTCChatSalon 인스턴스
* - note: {@link TRTCChatSalon#destroySharedInstance()}를 호출하여 단일 항목 객체를 폐기할 수 있습니다.
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39803) 단일 항목 객체 폐기

>?인스턴스 폐기 후에는 외부에 캐시된 TRTCChatSalon 인스턴스를 다시 사용할 수 없으며, 다시 [sharedInstance](#sharedinstance)를 호출해 새로운 인스턴스를 획득해야 합니다.

```Objective-C
/**
* TRTCChatSalon 단일 항목 객체 폐기
*
* - note: 인스턴스 폐기 후에는 외부에 캐시된 TRTCChatSalon 인스턴스를 다시 사용할 수 없으며, 다시 {@link TRTCChatSalon#sharedInstance()}를 호출해 새로운 인스턴스를 획득해야 합니다.
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39803) 이벤트 콜백은 TRTCChatSalonDelegate를 통해 [TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39803)의 다양한 상태 공지를 받아볼 수 있습니다.

```Objective-C
/**
* 모듈 콜백 인터페이스 설정
* 
* TRTCChatSalonDelegate를 통해 TRTCChatSalon의 다양한 상태 공지를 받아볼 수 있습니다.
*
* - parameter delegate 콜백 인터페이스
* - note: TRTCChatSalon의 이벤트 콜백은 기본적으로 Main Queue에서 귀하에게 콜백합니다. 이벤트 콜백이 존재하는 큐를 지정할 경우 {@link TRTCChatSalon#setDelegateQueue(queue)}를 이용할 수 있습니다.
*/
- (void)setDelegate:(id<TRTCChatSalonDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegate는 TRTCChatSalon의 프록시 콜백입니다.   

### setDelegateQueue

이벤트 콜백이 존재하는 스레드 큐를 설정합니다. 기본적으로 메인 스레드 MainQueue로 발송합니다.

```Objective-C
/**
* 이벤트 콜백이 존재하는 큐 설정
*
* - parameter queue입니다. TRTCChatSalon의 다양한 상태 공지를 콜백하며 지정한 queue로 배포합니다.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));
```

매개변수는 다음과 같습니다.

| 매개변수  | 유형             | 의미                                                         |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | TRTCChatSalon의 다양한 상태를 통지하며, 지정한 스레드 큐로 배포합니다. |

   

### login

로그인

```Objective-C
- (void)login:(int)sdkAppID
       userID:(NSString *)userID
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userID:userSig:callback:));

```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int            | TRTC 콘솔>[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | String         | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig  | String         | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |
| callback | ActionCallback | 로그인 콜백이며, 성공 시 code는 0입니다.                                  |

   

### logout

로그아웃

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | 로그아웃 콜백이며, 성공 시 code는 0입니다. |

   

### setSelfProfile

개인 정보 수정

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형           | 의미                                |
| --------- | -------------- | ----------------------------------- |
| userName  | String         | 닉네임                              |
| avatarURL | String         | 프로필 사진 주소                          |
| callback  | ActionCallback | 개인 정보 설정 콜백이며, 성공 시 code는 0입니다. |

   


## 방 관련 인터페이스 함수

### createRoom

방 생성(호스트 호출)

```Objective-C
- (void)createRoom:(int)roomID roomParam:(ChatSalonParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형           | 의미                                                         |
| --------- | -------------- | ------------------------------------------------------------ |
| roomId    | int            | 방 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomID를 1개의 음성 채팅방 리스트로 통합할 수 있으며, Tencent Cloud는 현재 음성 채팅방 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | ChatSalonParam | 방 정보입니다. 방 이름, 마이크 위치 정보, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. |
| callback  | ActionCallback | 방 생성 결과 콜백이며, 성공 시 code는 0입니다.                        |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 

1. 호스트가 `createRoom`을 호출하여 새로운 음성 채팅방을 생성합니다. 이때 방 ID, 마이크를 켤 때 방장 확인 필요 여부 등 방 속성 정보를 전송합니다.
2. 호스트가 방 생성 후 `enterSeat`을 호출하여 자리에 입장합니다.
3. 호스트는 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 공지도 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

   

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |


### enterRoom

방 입장(시청자 호출)

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | 방 식별 번호                            |
| callback | ActionCallback | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |


시청자가 방에 입장하여 시청하는 정상적인 호출 프로세스는 다음과 같습니다. 

1. 시청자는 서버에서 최신 음성 살롱 리스트를 획득하며, 여기에는 여러 음성 살롱의 roomId 및 방 정보가 포함될 수 있습니다.
2. 시청자가 음성 채팅방 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
3. 방 입장 후 모듈의 `onRoomInfoChange` 방 속성 변경 이벤트 공지를 수신합니다. 이때 UI에 방 이름 표시, 마이크를 켤 때 호스트에게 동의 요청 필요 여부 등 방의 속성을 기록할 수 있으며 그에 해당하는 변경이 가능합니다.
4. 방 입장 후, 모듈의 `onEnterRoomSeatListNotify` 현재 방 호스트 정보 콜백을 수신합니다. 이때 마이크 위치 리스트의 정보에 따라 현재 방 호스트의 사용자 정보를 조회하여 UI 인터페이스에 새로 고침합니다.
5. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 공지도 수신합니다.

### exitRoom

방 퇴장

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |

   

### getRoomInfoList

방 리스트의 세부 정보를 획득. 방 이름, 방 썸네일은 호스트가 `createRoom()` 시 roomInfo를 통해 설정할 수 있습니다.

>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(ChatSalonInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형                  | 의미               |
| ---------- | --------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt;   | 방 번호 리스트       |
| callback   | ChatSalonInfoCallback | 방 세부 정보 콜백 |


### getUserInfoList

특정 userId의 사용자 정보 획득

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(ChatSalonUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                      | 의미                                                         |
| ---------------- | ------------------------- | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt;        | 특정 사용자 ID 리스트를 획득합니다. null인 경우 방 안에 있는 모든 사용자 정보를 획득합니다. |
| userlistcallback | ChatSalonUserListCallback | 사용자 세부 정보 콜백                                           |


## 마이크 켜짐/꺼짐 인터페이스

### enterSeat

직접 마이크 켬(시청자와 호스트 모두 호출 가능)

>?마이크가 켜진 후, 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 공지를 수신합니다.

```Objective-C
- (void)enterSeat:(ActionCallback _Nullable)callback
NS_SWIFT_NAME(enterSeat(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 작업 콜백 |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 시청자가 호스트에게 신청해야 하는 시나리오의 경우 먼저 `sendInvitation`을 호출해 호스트에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.

### leaveSeat

직접 마이크 끔(시청자와 호스트 모두 호출 가능)

>? 마이크가 꺼진 후, 방 안에 있는 모든 사용자가 `onAnchorLeaveSeat` 이벤트 공지를 수신합니다.

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 작업 콜백 |

### pickSeat

특정 사용자 마이크 켬(호스트 호출)

>? 호스트가 특정 사용자의 마이크를 켜면 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 공지를 수신합니다.

```Objective-C
- (void)pickSeat:(NSString *)userID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(userID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| userID   | String         | 사용자 ID  |
| callback | ActionCallback | 작업 콜백 |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 호스트가 시청자에게 동의를 얻어야만 마이크를 켤 수 있는 시나리오의 경우 먼저 `sendInvitation`을 호출하여 시청자에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.


### kickSeat

특정 사용자 마이크 끔(호스트 호출)

>? 호스트가 특정 사용자의 마이크를 끄면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 공지를 수신합니다.

```Objective-C
- (void)kickSeat:(NSString *)userID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(userID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                 |
| -------- | -------------- | -------------------- |
| userID   | String         | 마이크를 끌 사용자 id |
| callback | ActionCallback | 작업 콜백           |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 호스트가 시청자에게 동의를 얻어야만 마이크를 켤 수 있는 시나리오의 경우 먼저 `sendInvitation`을 호출하여 시청자에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.

## 로컬 오디오 작업 인터페이스

### startMicrophone

마이크 수집 시작

```Objective-C
- (void)startMicrophone;
```

### stopMicrophone

마이크 수집 종료

```Objective-C
- (void)stopMicrophone;
```

### setAudioQuality

오디오 품질 설정

```Objective-C
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형 | 의미                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 오디오의 품질로, 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참조하십시오. |


### muteLocalAudio

로컬 오디오 음소거/음소거 취소

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | 오디오를 음소거/음소거 취소합니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)를 참조하십시오. |



### setSpeaker

스피커 활성화 설정

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형    | 의미                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true: 스피커, false: 헤드셋 |



### setAudioCaptureVolume

마이크 수집 음량 설정

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 수집 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |


### setAudioPlayoutVolume

재생 음량 설정

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 재생 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |

### muteRemoteAudio

특정 사용자 음소거/음소거 해제

```Objective-C
- (void)muteRemoteAudio:(NSString *)userID mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                              |
| ------ | ------- | --------------------------------- |
| userID | String  | 지정 사용자 ID                   |
| mute   | boolean | true: 음소거, false: 음소거 해제 |

### muteAllRemoteAudio

모든 사용자 음소거/음소거 해제

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true: 음소거, false: 음소거 해제 |

   

## 배경 음악 음향 효과 관련 인터페이스 함수

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## 메시지 발송 관련 인터페이스 함수

### sendRoomTextMsg

방 안에서 텍스트 메시지 발송. 일반적으로 댓글 자막 채팅에 사용합니다.

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미           |
| -------- | -------------- | -------------- |
| message  | String         | 텍스트 메시지     |
| callback | ActionCallback | 발송 결과 콜백 |

   

### sendRoomCustomMsg

사용자 정의 텍스트 메시지 발송

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                               |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | String         | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String         | 텍스트 메시지                                         |
| callback | ActionCallback | 발송 결과 콜백                                     |

   

## 초대 신호 관련 인터페이스

### sendInvitation

사용자에게 초대 발송

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userID:(NSString *)userID
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미             |
| -------- | -------------- | ---------------- |
| cmd      | String         | 서비스의 사용자 정의 명령 |
| userID   | String         | 초대한 사용자 ID  |
| content  | String         | 초대 내용     |
| callback | ActionCallback | 발송 결과 콜백   |

반환값:

| 반환값   | 유형   | 의미                  |
| -------- | ------ | --------------------- |
| inviteId | String | 해당 초대 ID를 식별하는 데 사용 |

### acceptInvitation

초대 수락

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형           | 의미           |
| ---------- | -------------- | -------------- |
| identifier | String         | 초대 ID      |
| callback   | ActionCallback | 발송 결과 콜백 |

### rejectInvitation

초대 거부

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형           | 의미           |
| ---------- | -------------- | -------------- |
| identifier | String         | 초대 ID      |
| callback   | ActionCallback | 발송 결과 콜백 |


### cancelInvitation

초대 취소

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형           | 의미           |
| ---------- | -------------- | -------------- |
| identifier | String         | 초대 ID      |
| callback   | ActionCallback | 발송 결과 콜백 |

## TRTCChatSalonDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백

>? SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 적절한 인터페이스로 사용자에게 안내해야 합니다.

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| code    | int    | 에러 코드   |
| message | String | 오류 정보 |


### onWarning

경고 콜백

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| code    | int    | 에러 코드   |
| message | String | 경고 정보 |

   

### onDebugLog

Log 콜백

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| message | String | 로그 정보 |

   


## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백. 호스트가 방을 종료하면 방 안에 있는 모든 사용자는 해당 공지를 받게 됩니다.

```Objective-C
- (void)onRoomDestroy:(NSString *)message
NS_SWIFT_NAME(onRoomDestroy(message:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미      |
| ------ | ------ | --------- |
| roomId | String | 방 ID |


### onRoomInfoChange

방 입장 후 해당 인터페이스를 콜백합니다. roomInfo의 정보는 방 생성 시의 정보입니다.

```Objective-C
- (void)onRoomInfoChange:(ChatSalonInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형          | 의미       |
| -------- | ------------- | ---------- |
| roomInfo | ChatSalonInfo | 방 정보 |

   

### onUserVolumeUpdate

음량 크기 알림을 활성화하여 모든 참여자의 음량 크기를 통지합니다.

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

매개변수는 다음과 같습니다.

| 매개변수        | 유형                      | 의미               |
| ----------- | ------------------------- | ------------------ |
| userVolumes | NSArray&lt;TRTCVolumeInfo *&gt; | 각 사용자별 음량 정보 |
| totalVolume | int                       | 전체 음량 정보     |


## 마이크 위치 콜백

### onEnterRoomSeatListNotify

방 입장 후 현재 방의 호스트 정보를 콜백

```Objective-C
- (void)onEnterRoomSeatListNotify:(NSArray<ChatSalonSeatInfo *> *)seatInfoList
NS_SWIFT_NAME(onEnterRoomSeatListNotify(seatInfoList:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형                          | 의미                 |
| ------------ | ----------------------------- | -------------------- |
| seatInfoList | List&lt;ChatSalonSeatInfo&gt; | 모든 호스트의 마이크 위치 리스트 |

### onAnchorEnterSeat

사용자 마이크 켜짐(직접 마이크 켬/호스트가 특정 사용자 마이크 켬)

```Objective-C
- (void)onAnchorEnterSeat:(ChatSalonUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(user:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형              | 의미                 |
| ---- | ----------------- | -------------------- |
| user | ChatSalonUserInfo | 마이크가 켜진 사용자의 세부 정보 |

### onAnchorLeaveSeat

사용자 마이크 꺼짐(직접 마이크 끔/호스트가 특정 사용자 마이크 끔)

```Objective-C
- (void)onAnchorLeaveSeat:(ChatSalonUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(user:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형              | 의미                 |
| ---- | ----------------- | -------------------- |
| user | ChatSalonUserInfo | 마이크가 켜진 사용자의 세부 정보 |

### onSeatMute

호스트 마이크 음소거

```Objective-C
- (void)onSeatMute:(NSString *)userID
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(userID:isMute:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                               |
| ------ | ------- | ---------------------------------- |
| userID | String  | 마이크 위치의 사용자 id                     |
| isMute | boolean | true: 음소거, false: 음소거 해제 |

## 시청자 입장/퇴장 이벤트 콜백

### onAudienceEnter

시청자 방 입장 공지 수신

```Objective-C
- (void)onAudienceEnter:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형              | 의미           |
| -------- | ----------------- | -------------- |
| userInfo | ChatSalonUserInfo | 입장한 시청자 정보 |

### onAudienceExit

시청자 방 퇴장 공지 수신

```Objective-C
- (void)onAudienceExit:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형              | 의미           |
| -------- | ----------------- | -------------- |
| userInfo | ChatSalonUserInfo | 퇴장한 시청자 정보 |

   

## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지 수신

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형              | 의미             |
| -------- | ----------------- | ---------------- |
| message  | String            | 텍스트 메시지       |
| userInfo | ChatSalonUserInfo | 발신자 정보 |

   

### onRecvRoomCustomMsg

사용자 정의 메시지 수신

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString *)message
                   userInfo:(ChatSalonUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형              | 의미                                               |
| -------- | ----------------- | -------------------------------------------------- |
| command  | String            | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String            | 텍스트 메시지                                         |
| userInfo | ChatSalonUserInfo | 발신자 정보                                   |

## 초대 신호 이벤트 콜백

### onReceiveNewInvitation

새로운 초대 요청 수신

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(identifier:inviter:cmd:content:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미                               |
| ---------- | ------ | ---------------------------------- |
| identifier | String | 초대 ID                          |
| inviter    | String | 초대한 사용자 ID                  |
| cmd        | String | 서비스에서 지정한 명령어. 개발자가 사용자 정의 |
| content    | String | 서비스에서 지정한 내용                   |

### onInviteeAccepted

초대된 사용자가 초대 수락

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(identifier:invitee:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미                |
| ---------- | ------ | ------------------- |
| identifier | String | 초대 ID           |
| invitee    | String | 초대된 사용자 ID |

### onInviteeRejected

초대된 사용자가 초대 거부

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(identifier:invitee:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미                |
| ---------- | ------ | ------------------- |
| identifier | String | 초대 ID           |
| invitee    | String | 초대된 사용자 ID |

### onInvitationCancelled

초대한 사용자가 초대 취소

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미              |
| ---------- | ------ | ----------------- |
| identifier | String | 초대 ID         |
| inviter    | String | 초대한 사용자 ID |
