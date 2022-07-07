### Version 10.0 @ 2022.05.17

**기능 최적화:** 

- 모든 플랫폼: 호스트 방 입장 및 퇴장에 대한 콜백([onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) / [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28)) 속도를 높였습니다.
- Windows: 화면 공유를 최적화하여 창 필터링 기능을 사용하지 않을 때 성능이 2배로 향상되었습니다.

**오류 수정:** 

- iOS 및 macOS: 배경 음악 시작 시 간헐적으로 발생하는 [onComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html#a08ab9a6d9100f133420e44ae5eb99ee6) 콜백 오류가 수정되었습니다.
- Android: 네트워크 모듈로 인한 충돌 문제가 수정되었습니다.
- 모든 플랫폼: SEI 전송 오류가 수정되었습니다.


### Version 9.9 @ 2022.05.06

**기능 최적화:** 
- Windows: 비디오 전송을 최적화하여 오버헤드를 줄였습니다.
- Windows: 듀얼 채널 효과를 유지하면서 Systemloopback 캡처 사전 처리를 최적화했습니다.
- macOS: 캡처 볼륨이 너무 높을 때 오디오가 깨지는 문제를 수정하여 오디오 경험을 개선했습니다.
- macOS: 화면 공유(서브 스트림)의 비디오 품질을 개선했습니다.
- Android: 캡처 지연 시간을 줄여 인이어 모니터링 경험을 개선했습니다.

**오류 수정:** 
- Android: 방 ID에 대해 21억보다 큰 숫자에 대한 지원이 추가되었습니다.


### Version 9.8 @ 2022.04.21

**새로운 기능:**
- Windows: ‘헤비 메탈’ 및 ‘어린 소녀’와 같은 오디오 효과용 API를 추가했습니다. 자세한 내용은 `ITXAudioEffectManager.setVoiceChangerType`을 참고하십시오.
- Windows: 로컬 비디오가 일시 중지될 때 이미지 표시에 대한 지원이 추가되었습니다.

**기능 최적화:** 

모든 플랫폼: 비디오 시나리오에서 SDK 성능이 향상되었습니다.

**오류 수정:** 
- Mac: 내장 사운드 카드의 오디오 녹음 시 드라이버 설치에 실패하는 현상이 수정되었습니다.
- 모든 플랫폼: 로컬 화면이 (서브스트림을 통해) 공유될 때 사용자 지정 렌더링 오류가 수정되었습니다.


### Version 9.7 @ 2022.04.06

**기능 최적화:** 
- iOS&Android: Music 모드의 오디오 품질이 향상되었습니다.
<dx-alert infotype="explain" title="Tips：">
[TRTCCloud.startLocalAudio (TRTCAudioQualityMusic)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) API를 사용하여 모든 플랫폼에서 Music 모드를 활성화할 수 있습니다.
</dx-alert>
- Windows: Music 모드에서 오디오 품질이 향상되고 오디오 손실이 감소했습니다.
- Windows: 고급 사운드 카드와의 호환성이 향상되어 오디오 품질이 향상되었습니다.
- Windows: 더 많은 시나리오를 위해 3rd party 프로세스와 오디오 믹싱을 최적화했습니다.

**오류 수정:**
- 모든 플랫폼: CDN 재생 중 간헐적으로 화면이 흐릿해지는 문제를 수정했습니다.
- iOS&Android: 라이브 스트림을 재생할 때 수신기와 스피커 간에 전환하지 못하는 문제를 수정했습니다.
- iOS&Android: Music 모드를 활성화하기 위해 API를 호출한 후 오디오 품질이 기대에 미치지 못하는 문제가 수정되었습니다.
- iOS: 소프트웨어 인코딩 중 간헐적으로 발생하는 메모리 유출을 수정했습니다.
- iOS: 가끔 로컬 비디오 렌더링을 위한 첫 번째 프레임 콜백이 수신되지 않는 문제가 수정되었습니다.
- Windows: 화면 공유 중에 마우스 커서가 캡처될 때 SDK가 충돌하는 가끔 문제가 수정되었습니다.
- Windows: Music 모드에서 스피커가 제대로 작동하지 않는 현상이 수정되었습니다.
- Windows: startCameraDeviceTest API가 호출될 때 일부 카메라가 켜지지 않는 문제를 수정했습니다.


### Version 9.6 @ 2022.03.24

**주요 변화:**

- 모든 플랫폼: 중국 본토 안팎의 규정을 준수하는 향상된 3rd party 라이브러리.
- 모든 플랫폼: SDK 저장소 공간을 줄였습니다. 자세한 내용은 아래 표를 참고하십시오.
<table>
<thead>
<tr>
<th>플랫폼</th>
<th><strong>전</strong></th>
<th><strong>후</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Android</td>
<td>armv7：6.95M<br>arm64：7.94M</td>
<td>armv7：4.32M<br>arm64：4.85M</td>
</tr>
<tr>
<td>iOS</td>
<td>arm64：3.23M</td>
<td>arm64：3.15M</td>
</tr>
<tr>
<td>Windows</td>
<td>Win32：21.3M<br>Win64：26.9M</td>
<td>Win32：15.0M<br>Win64：17.2M</td>
</tr>
<tr>
<td>Mac</td>
<td>x86_64：18.1M</td>
<td>x86_64：15.8M</td>
</tr>
</tbody></table>

**장애 수정:**

모든 플랫폼: 알려진 문제를 수정하여 안정성을 개선했습니다.

**기능 최적화:**
- iOS: 필 라이트를 사용할 때 간헐적으로 과다 노출되는 문제를 수정했습니다.
- Mac: 텍스처 업로드를 최적화했습니다.
- Android: 뷰티 필터 및 기타 기능에 대한 개선된 전처리 방법, 저가형 장치에서 캡처 끊김 현상을 수정했습니다.
- Windows: Live 스트리밍 컴포넌트를 Live V1에서 V2 API로 업데이트하여 안정성을 개선했습니다.
- Windows: 저가형 장치의 GPU와의 호환성이 향상되었습니다.



### Version 9.5 @ 2022.01.11

**장애 수정:**
- 모든 플랫폼: 사용자가 사용자 지정 비디오 렌더링을 활성화하기 위해 특정 순서로 API를 요청하면 검은색 화면이 표시되는 문제가 수정되었습니다.
- Windows: 화면 공유 수집 영역이 불완전한 문제가 수정되었습니다.
- iOS: [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) 호출 후, 방 퇴장하고 다음 방 입장 시 스트림 상태가 푸시되지 않는 문제가 수정되었습니다.
- iOS: 혼합 스트림 설정의 배경 이미지가 유효하지 않은 문제를 수정되었습니다.

**기능 최적화:**
- 모든 플랫폼: 약한 네트워크 환경에서의 통화 원활성이 최적화되었습니다.
- Windows: 카메라 호환성을 최적화하여 일부 장치의 캡처 프레임 레이트가 설정 값과 일치하지 않거나 활성화되지 않는 문제를 해결했습니다.
- iOS: cocos2D와 같은 다른 렌더링 모듈과 공유할 때 호환성을 향상하고 충돌을 줄였습니다.
- Android: 카메라를 껐다가 켰을 때, 재생 종료 전 마지막 프레임을 표시한 후 정상적으로 표시되는 문제를 복구했습니다.

### Version 9.4 @ 2021.12.08

**새로운 기능:**
- 전체 플랫폼: 새롭게 추가된 음성 추적 기능은 대규모 음성 마이크 연결 시나리오에 적합하며, 여러 사용자가 동시에 마이크를 켜는 노이즈 환경에서도 여전히 주요 사용자의 음성에 집중할 수 있습니다. [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b) API를 통해 설정할 수 있습니다.
- Mac: 시스템 사운드 수집에 [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) 듀얼 사운드 채널 지원이 추가되었습니다.
- iOS: 24 비트 wav 형식의 배경 음악 파일에 대한 지원이 추가되었습니다.
- Android&iOS: 이 버전은 국가 개인 정보 및 보안 규정의 조항을 준수하며 많은 Tencent 제품에 의해 검증되었습니다.

**문제 수정:**
- 전체 플랫폼: [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9)을 빠르게 호출하면 방 전환 실패가 발생하는 문제가 수정되었습니다.
- iOS: 애플리케이션에서 화면 녹화 [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) 프로세스 중 [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) 설정 오류 문제가 수정되었습니다.
- iOS: 시스템 화면 녹화 [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) 중 간헐적으로 발생하는 메모리 증가 문제가 수정되었습니다.

**기능 최적화:**
- 전체 플랫폼: 방 입장 속도를 높이고 방 입장 소요 시간의 변동폭을 줄였습니다.
- Mac: 화면 캡처 과정에서 마우스 캡처를 켜면 높은 CPU 및 메모리를 점유하는 문제를 해결했습니다.
- Android: 화면 공유 시 화면 캡처 해상도를 조정하여 항상 화면 해상도와 일치하도록 하고 공유 화면 검은 테두리 등 문제를 방지하였습니다.
- Android: 비디오 하드웨어 솔루션의 호환성을 개선하여 일부 휴대폰의 비디오 해상도 변경 시 발생 가능한 블랙 스크린 문제를 해결했습니다.
- Windows: 게인 알고리즘을 최적화하여 일부 장치의 과도한 게인으로 인한 노이즈 문제를 해결했습니다.

### Version 9.3 @ 2021.11.03

**장애 복구**
- 전체 플랫폼: point2PointDelay를 간헐적으로 사용할 수 없고 값이 0인 문제가 수정되었습니다.
- 전체 플랫폼: 리졸브 실패 시 간헐적으로 SEI 메시지가 누락되는 문제가 수정되었습니다.
- Mac: MacOS 12 beta에서 카메라가 프레임으로 나오지 않는 현상이 수정되었습니다.
- iOS&Mac: 특정 순서로 미리 startRemoteView를 호출하여 화면이 보이지 않는 현상이 수정되었습니다.
- Windows: 세로 화면 인코딩 사용 및 뷰티필터 활성화 시 화면이 들쭉날쭉하게 나오는 현상이 수정되었습니다.
- Windows: 3rd party 뷰티필터 활성화 상태에서 해상도를 전환한 후 사용자 정의 렌더링이 콜백되지 않는 문제가 수정되었습니다.

**기능 최적화**
- 전체 플랫폼: 네트워크가 약한 상황에서 동영상 바로 재생 속도가 최적화되었습니다.
- 전체 플랫폼: 약한 네트워크 제어 정책을 최적화하여 원활성을 개선하였습니다.
- 전체 플랫폼: 속도 측정 기능을 최적화하고 현재 네트워크 대역폭의 점검을 지원합니다.
- 전체 플랫폼: 복잡한 네트워크 환경에 더 잘 대처할 수 있도록 TCP 전송 프로토콜에 대한 지원을 최적화했습니다.

### Version 9.2 @ 2021.09.23

**새로운 기능**
- Android&iOS: Socks5 프록시를 지원합니다.
- Windows: TRTCAudioQualityMusic은 고음질 시나리오를 위한 어댑티브 에코 제거 기능을 추가하여 음질과 에코 제거 강도 균형을 자동으로 조정합니다.
- 전체 플랫폼: 음성 톤 설정 기능이 추가되었습니다.

**장애 복구**
- Windows: Mac에 Windows가 설치된 환경에서 일부 카메라가 데이터를 내보내지 않는 문제가 수정되었습니다.
- Android: CDN/TRTC CDN/TRTC 전환 후 간헐적으로 업스트림 오디오가 들리지 않는 문제가 수정되었습니다.
- iOS: Web측 화면 공유 시 iOS 수신측에서 사용자 정의 렌더링 화면 출력 오류 문제가 수정되었습니다.

**기능 최적화**
- Android: 하드 디코딩 시 발생하는 ANR 문제가 최적화되었습니다.
- Android: 카메라의 로컬 미리보기 각도 호환 문제가 최적화되었습니다.
- Android: 첫 프레임의 바로 재생 속도가 최적화되었습니다.
- Android&iOS: 합창 모드의 3A 정책이 최적되었습니다.
- Windows: AGC 알고리즘을 최적화해 소리가 너무 작거나 소리가 너무 큰 문제가 발생할 확률을 낮췄습니다.
- 전체 플랫폼: 약한 네트워크 환경에서 지터 방지 알고리즘을 최적화하여 동영상 재생이 더 원활해졌습니다.

### Version 9.1 @ 2021.09.04

**새로운 기능**
- 전체 플랫폼: C++ 인터페이스에서 오디오 프레임 콜백 형식 설정을 지원합니다.
- Windows: ac3 형식 VOD 파일 재생에 대한 지원이 추가되었습니다. 
- Windows: 카메라 정보의 지원되는 해상도 목록 가져오기가 지원됩니다. 자세한 내용은 [ITXDeviceCollection.getDeviceProperties](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450)를 참고하십시오.
- Windows: Nvidia, Intel, AMD 하드웨어 디코딩을 지원합니다.
- Mac: 로컬 미디어 녹화에 대한 지원이 추가되었습니다.

**문제 수정**
- 전체 플랫폼: 간헐적으로 발생하는 방 입장 실패 문제가 수정되었습니다.
- Mac: 화면 공유 중 해상도 전환 시 미리보기가 깜박이는 현상이 수정되었습니다.
- Android: 서브 룸에서 메인 룸으로 전환 시 서브스트림 비디오의 표시 오류를 해결했습니다.
- Android: 일부 시나리오에서 간헐적으로 프레임 레이트 설정이 적용되지 않는 문제가 수정되었습니다.
- Windows: 시청자의 CDN 재생 전환 후 풀 스트리밍 실패 문제가 수정되었습니다.
- Windows: 특정 형식의 VOD 파일 재생 시 이미지가 사라지는 현상이 수정되었습니다.

**품질 최적화**
- 전체 플랫폼: 약한 네트워크 조건에서 향상된 경험을 제공합니다.
- Android: 방 퇴장 시 오디오 상태 관리가 최적화되었습니다.
- Android: 오디오 캡처 실행 실패 후 복구 로직을 최적화하여 성공률을 높였습니다.
- Android: 특정 조건에서의 영상 화면 과다 노출 문제가 최적화되었습니다.

### Version 9.0 @ 2021.08.06

**새로운 기능**
- 시스템 수집 볼륨 설정을 지원합니다. 자세한 내용은 [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae)을 참고하십시오.
- 전체 플랫폼: 사용자 정의 오디오 트랙의 볼륨 설정을 지원합니다. 자세한 내용은 [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418)을 참고하십시오.
- 전체 플랫폼: 상태 콜백으로 오디오와 비디오의 패킷 손실률을 구분할 수 있습니다. 자세한 내용은 [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics)를 참고하십시오.

**품질 최적화**
- 전체 플랫폼: 구독 프로세스를 최적화하여 수동 구독의 바로 재생 속도를 개선했습니다.
- 전체 플랫폼: 특정 시나리오에서의 onExitRoom 콜백 중복 문제를 수정했습니다.

**문제 수정**
- Android: 사용자 정의 수집의 비트 레이트 및 프레임 레이트 동적 설정이 적용되지 않는 문제가 수정되었습니다.
- iOS: 사용자가 먼저 화면 공유 서브스트림을 활성화한 다음 카메라를 켜면 푸시 스트림이 실패되는 문제가 수정되었습니다.
- iOS: 로컬 비디오 녹화 화면이 흐릿한 문제가 수정되었습니다.
- iOS: 몇 가지 안정성 문제가 수정되었습니다.
- Winodws: 화면 공유 시 수집 프레임 레이트 예외 문제가 수정되었습니다.
- Windows: 화면 공유 중 타깃 전환 시, 시청자에게 이전 프레임 화면이 표시되는 문제가 수정되었습니다.

### Version 8.9 @ 2021.07.15

**새로운 기능** 
- Android: 사용자 정의 렌더링의 외부 GLContext 지정을 지원하여 OpenGL 환경을 보다 효율적으로 사용할 수 있습니다.
- Windows: 시스템 오디오 수집 [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e)을 위한 스피커 지정을 지원합니다.
- Windows: NVIDIA 플랫폼 하드 코딩을 지원하여 스트리밍 성능을 개선하였습니다.
- 전체 플랫폼: 회사 방화벽 내부 환경 보안 설정에 보다 친화적인 클라우드 프록시 지원이 추가되었습니다.
- 전체 플랫폼: [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) 및 [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) 인터페이스에 스트림 유형 매개변수를 추가했습니다.
- 전체 플랫폼: 통계 상태 콜백 [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9)에 사용자가 WiFi 공유기의 네트워크 품질을 판단하는데 사용되는 로컬 게이트웨이 지연에 대한 통계 gatewayRtt를 새롭게 추가했습니다.
- 전체 플랫폼: 오디오 녹음 인터페이스 [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677)은 더 많은 오디오 형식을 지원합니다.

**품질 최적화**
- 전체 플랫폼: 특정 시나리오에서 소리가 떨리는 문제가 최적화되었습니다.
- Android: 화면 바로 재생 속도가 최적화되었습니다.
- Android: 오디오 전처리 알고리즘을 업그레이드하여 통화 소리가 더 선명하게 들립니다.

**문제 수정**
- Windows: VODPlayer를 사용하여 VOD 파일 재생 시 녹화된 로컬 비디오의 에코 문제가 수정되었습니다.
- Windows: 높은 DPI 디스플레이에서 화면을 공유하는 동안 창 필터링 기능이 활성화된 경우 crash가 발생하는 문제가 수정되었습니다.
- iOS: 서브 스트림 푸시에 가로 모드 설정이 적용되지 않는 문제가 수정되었습니다.
- iOS: 사용자 정의 렌더링이 원격 비디오에 대해서만 활성화되고, RGBA 형식이 사용 시 발생하는 메모리 누수 문제가 수정되었습니다.
- 전체 플랫폼: 간혹 발생하는 방 입장 실패 문제가 수정되었습니다.

### Version 8.8 @ 2021.06.21

**새로운 기능**
Android&Mac&iOS: 주변 장치를 통한 오디오 재생을 지원합니다. 자세한 내용은 [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803) API를 참고하십시오.

**품질 최적화**
- 전체 플랫폼: mixExternalAudioFrame의 사용 편의성이 최적화되어 더 이상 호출 타이밍을 완벽하게 제어할 필요가 없습니다.
- Mac: 화면 공유 마우스 커서 캡처 활성화 시 CPU 사용량을 줄였습니다.
- Windows: AGC 사운드 증대 효과를 최적화하여 보다 빠르고 신속하게 조정됩니다.
- Windows: 창 필터링 활성화 시 화면 공유의 성능 부하가 최적화되었습니다.

**문제 수정**
- iOS: AAC 형식의 로컬 오디오 파일 재생 시 전체 길이가 정확하지 않은 문제가 수정되었습니다.
- Android: SDK 백그라운드 전환 후 일부 장치에서 오디오가 끊기는 문제가 수정되었습니다.

### Version 8.7 @ 2021.5.25
**새로운 기능**
- 전체 플랫폼: 외부 연결 오디오 기기에 대한 이상 검증이 추가되었습니다. onStatistics 콜백 등록 후, [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics)의 audioCaptureState로 장시간 음소거, 파음, 이상 끊김 문제를 실시간으로 검증할 수 있습니다.
- Windows: 사용자 정의 수집은 RGBA 포맷의 비디오 데이터 입력을 지원합니다.

**품질 최적화**
- 전체 플랫폼: BGM 리소스 관리를 최적화하여 메모리 점유율을 즉시 릴리스합니다.
- 전체 플랫폼: 푸시 스트리밍측에서 백그라운드 퇴장 후 비디오 업스트림을 일시 중지하면 재생측에서 [onUserVideoAvailable(false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) 공지를 즉시 수신할 수 있습니다.
- Mac: 화면 공유 시 마우스의 CPU 및 메모리 점유율이 최적화되었습니다.

**문제 수정**
- Android : setRemoteViewFillMode 일부 모델에 간혹 적용되지 않는 문제가 수정되었습니다.
- iOS/Mac: 사용자 정의 뷰티 필터 중지 시 메모리 리소스가 릴리스되는 문제가 수정되었습니다.

### Version 8.6 @ 2021.05.08
- 전체 플랫폼: 네트워크 트래픽 제어 알고리즘이 최적화되어 멀티미디어 전송 품질이 더욱 향상되었습니다.
- 전체 플랫폼: 역할 전환으로 마이크 켜짐/꺼짐 시 원활하게 오디오가 재생되도록 최적화되었습니다.
- iOS&Mac&Windows: 오디오 처리 모듈이 최적화되어 SPEECH 모드와 DEFAULT 모드의 음성 품질이 향상되었습니다.
- iOS&Mac: 높은 CPU 시나리오에서 사용자 정의 오디오 수집 맞춤성이 최적화되었습니다.
- iOS&Android: 비디오 녹화 시 서브 채널을 통한 공유로 데스크톱 버전 정렬을 지원합니다.
- Mac: Apple M1 아키텍처에 대한 네이티브 지원이 추가되었습니다.
- Windows: 메모리 할당 로직이 최적화되어 안정성이 향상되었습니다.


### Version 8.5 @ 2021.03.24
**새로운 기능**
-  Mac: 스크린 공유 기능을 최적화하여 타깃 창을 공유하면서 다른 창을 지정하여 함께 공유할 수 있습니다. 이와 관련한 내용은 API [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233)를 참고하십시오.
-  전체 플랫폼: 재생 기능을 추가하여 [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#classcom_1_1tencent_1_1rtmp_1_1TXVodPlayer)를 사용해 TRTCCloud와 바인딩하고, VOD가 현재 재생중인 콘텐츠를 TRTC의 우회 푸시 스트림을 통해 공유합니다.
-  전체 플랫폼: 우회 사용자 정의 수집 기능을 추가하였습니다. 이와 관련한 내용은 [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629) API를 참고하십시오.
-  전체 플랫폼: 사용자 정의 오디오 믹싱 기능을 추가하여 사용자의 사운드 트랙을 SDK의 오디오 처리 프로세스에 혼입할 수 있으며, SDK는 먼저 두 개 사운드 트랙을 믹싱한 뒤 배포합니다. 이와 관련한 내용은 API [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f)을 참고하십시오.
-  전체 플랫폼: 지정된 퓨어 비디오의 혼합 스트림을 지원하며, 더욱 유연한 혼합 스트림 제어가 가능합니다.

**품질 최적화**
- Mac: startSystemAudioLoopback으로 듀얼 사운드 채널을 지원합니다.
- Windows: 슬라이드 쇼 창을 선택하여 스크린 공유 시 슬라이드 쇼 창으로의 자동 전환을 지원합니다.
- 전체 플랫폼: 상태 콜백으로 end-to-end 딜레이를 증가시킵니다.

**문제 수정**
- iOS: 일부 장치에서 간혹 백그라운드 OpenGL 렌더링 중 발생하는 crash 문제가 수정되었습니다.
- iOS: 스크린 화면 정지 시 재생 중인 스크린 공유를 재생할 수 없는 문제가 수정되었습니다.


### Version 8.4 @ 2021.02.08
**새로운 기능**
- Mac: Windows와 동일하게 Mac 운영 체제의 출력 사운드를 수집하는 기능인 SystemLoopback 기능을 지원합니다. 이 기능은 SDK가 현재 시스템의 사운드를 수집할 수 있도록 하는 기능으로, 기능을 활성화하면 호스트가 손쉽게 다른 사용자에게 음악이나 영화 파일 라이브 방송을 할 수 있습니다.
-  Mac: 화면 공유 시 로컬 미리보기 기능을 지원합니다. 미니 창을 통해 공유할 화면 콘텐츠를 미리 볼 수 있습니다.
-  Windows: 프로세스 볼륨 조절 기능이 추가되었습니다. [setApplicationPlayVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1)을 통해 시스템 볼륨 믹서의 볼륨을 조절할 수 있습니다.
-  전체 플랫폼: 로컬 멀티미디어 녹화 기능이 추가되었습니다. 호스트는 푸시 스트림 중에 로컬 오디오 및 비디오를 mp4 파일로 녹음 및 녹화할 수 있습니다. 이와 관련한 내용은 [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b)을 참고하십시오.

**품질 최적화**
- 전체 플랫폼: cloubhouse와 같은 음성 라이브 방송 시나리오에 더욱 적합하도록 [Music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) 모드에서의 음질이 최적화되었습니다.
-  전체 플랫폼: 멀티미디어 링크의 네트워크 저항력을 최적화하여 극단적인 네트워크 검색 상황(70%)에서도 멀티미디어가 비교적 원활하게 재생됩니다.
-  Windows: 일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소되었습니다.
-  Windows: 성능 최적화를 통해 일부 사용 시나리오에서 구버전 대비 성능이 20% - 30% 향상되었습니다.

**문제 수정**
-  Windows: Windows Server 2019 Datacenter x64 시스템에서 데스크톱 공유 실행 시 발생하는 crash 문제가 수정되었습니다.
-  Windows: 창 공유와 동시에 타깃 창의 크기를 변경할 때 간혹 공유가 중지되는 BUG가 수정되었습니다.
-  Windows: 일부 모델의 카메라에서 화면을 수집하지 못하는 문제가 수정되었습니다.
-  iOS: snapvideoshot로 인해 CAAnimation 애니메이션 랙이 발생하는 문제가 수정되었습니다.
-  iOS&Mac: 동일한 View에서 카메라와 스크린 공유 화면을 번갈아 표시할 때 스크린 공유 화면의 블랙 스크린 문제가 수정되었습니다.
-  iOS: iPhone 6s에서 3rd party 뷰티 필터 컴포넌트 사용 시 화면이 뿌옇게 되는 문제가 수정되었습니다.
-  iOS: VOD와 TRTC 동시 사용 시 VOD 재생을 중단했을 때 간혹 발생하는 crash 문제가 수정되었습니다.
-  Android: 블루투스 이어폰 사용 중에 전화가 와서 연결이 끊어졌을 시, 전화 수신 거부 후 음성이 마이크를 통해 재생되는 문제가 수정되었습니다.

### Version 8.3 @ 2021.01.15

**새로운 기능**

이 버전에서는 사용자 정의 샘플링 관련 비즈니스 로직이 중점적으로 개선되었습니다.
- iOS & Android & Mac: 오디오 모듈 최적화를 통해 [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d)로 캡처한 음성 데이터를 SDK에 전송하여 처리할 때 SDK가 에코 억제 및 노이즈 감소 효과를 유지할 수 있도록 하였습니다.
- iOS & Android: TRTC SDK를 기반으로 오디오 특수효과 및 처리 로직을 지속적으로 강화해야 할 경우, 8.3버전을 사용하십시오. [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86)과 같은 인터페이스를 통해 오디오 데이터의 콜백 포맷(오디오 샘플링 레이트, 오디오 채널 수, 샘플링 포인트 등)을 설정하여 사용자가 선호하는 음성 포맷으로 오디오 데이터를 처리할 수 있습니다.
- 전체 플랫폼: 비디오 데이터를 자체 수집하고 TRTC SDK 자체 오디오 모듈을 사용해야 할 경우 오디오-비디오 동기화가 이루어지지 않는 문제가 발생할 수 있습니다. 이는 SDK 내부 타임라인의 자체 제어 로직으로 인해 발생하는 것으로, 이 문제에 대한 대응책으로 [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) 인터페이스가 제공됩니다. 비디오 화면을 수집할 때 이 인터페이스를 사용해서 현재 PTS(타임스탬프)를 기록한 다음 [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831)를 호출할 때 이 타임스탬프를 적용하면 오디오-비디오 동기화를 유지할 수 있습니다.
- Windows: 버전 SDK에 도메인 포맷에 대한 Socks5 프록시 지원이 추가되었습니다.

**문제 수정**
- 전체 플랫폼: 간혹 오디오 데이터의 타임스탬프에 오류가 발생하여 녹화된 부분에서 오디오-비디오 동기화가 유지되지 않는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 창 공유 호환성이 개선되었습니다.
- Windows: 공유할 수 있는 창 목록을 가져올 때 최소화된 창을 추가합니다. 최소화된 창의 축소 이미지는 해당 프로세스의 아이콘으로 표시됩니다.
- Windows: SDK 실행 시 불필요한 DXGI 점유 문제가 수정되었습니다.
- iOS: 수동 포커스 설정을 할 경우 ANR이 발생하는 문제가 수정되었습니다.
- iOS: 간혹 전환 전후로 카메라가 인식되지 않는 문제가 수정되었습니다.
- iOS: VODPlayer 감속 재생 시 크래시 발생 문제가 수정되었습니다.
- iOS: 간혹 방에 입장한 후 헤드셋에서 오디오가 재생되는 문제가 수정되었습니다.
- iOS & Android: 에코 제거 및 잡음 억제 효과가 개선되었으며, 인이어 모니터링에서도 잔향 효과를 들을 수 있게 되었습니다.
- Android: 간혹 하드웨어 디코딩 시 화면 출력 오류가 나타나는 문제가 수정되었습니다.
- Mac: 창 공유 및 고휘도 모드 활성화 시 창 프레임이 반짝이는 문제가 수정되었습니다.
- Mac: 렌더링 투시도 이동 시 블랙 스크린이 발생하는 문제가 수정되었습니다.


### Version 8.2 @ 2020.12.23

**새로운 기능**
- iOS & Android: 로컬 샘플링과 재생된 모든 오디오 데이터의 혼합 콜백이 추가되어 로컬 오디오가 더욱 편리해졌습니다.
- Android: 비디오 렌더링 컴포넌트 TXCloudVideoView가 `addVideoView(new TextureView(getApplicationContext()))` 인터페이스를 지원하여 TextureView를 로컬 렌더링에 사용합니다.
- Android: 사용자 정의 렌더링 콜백이 RGBA 포맷의 비디오 데이터를 지원합니다.
- Windows: 로컬 카메라 수집과 원격 비디오 스트림 캡처 재생을 지원합니다. [ITRTCCloud.snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96)를 참고하십시오.
- Windows: 화면 공유가 addExcludedShareWindow와 addIncludedShareWindow 인터페이스를 통해 지정된 창의 제외 또는 강제 포함 기능을 지원하여 보다 유연한 화면 공유 기능을 제공합니다.
- Mac & iOS: 사용자 정의 렌더링 모드에서도 TRTCCloud.snapshotVideo로 추출한 비디오 이미지 플로우를 호출할 수 있습니다.

**품질 최적화**
- Android: 온라인 라이브 방송 코딩 품질이 개선되어 더욱 선명한 영상을 제공합니다.
- Windows: 에코 제거 알고리즘이 개선되어 에코 제거 효과가 향상되었습니다.

**문제 수정**
- iOS: VODPlayer와 TRTC를 동시에 사용할 경우 간혹 오디오 재생 오류가 발생하는 문제가 수정되었습니다.
- Android: 사용자 정의 뷰티 필터가 로컬 렌더링 블랙 스크린을 발생시키는 문제가 수정되었습니다.
- Windows: 간혹 진행 중인 프로세스를 종료할 수 없는 문제가 수정되었습니다.


### Version 8.1 @ 2020.12.03

**새로운 기능**
-전체 플랫폼: 통계 정보(onStatistics)에 원격 비디오 랙과 관련된 통계 지표가 추가되었습니다.
-전체 플랫폼: 음량 조절 인터페이스 setAudioPlayoutVolume(100-150)를 통해 오디오 부스터 효과를 적용할 수 있게 되었습니다.
- iOS & Android: setLocalVideoProcessListener 인터페이스가 추가되어 서드파티 뷰티 필터 SDK 통합 지원 기능이 향상되었습니다.
- C#: 최신 버전의 API 인터페이스로 업데이트되었습니다.

**품질 최적화**
- 전체 플랫폼: 이어폰 착용 시 음성 처리 알고리즘이 개선되어 오디오 품질이 향상되었습니다.
- Android: 오디오 전처리 알고리즘이 개선되어 3A 알고리즘이 음질에 미치는 영향이 감소되었습니다.

**문제 수정**
- iOS: 간혹 App 강제 종료 시 크래시가 발생하는 문제가 수정되었습니다.
- Android: 프레임 레이트 샘플링이 높을 경우 뷰티 필터 효과에 오류가 발생하는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 화면 공유 시 간혹 크래시가 발생하는 문제가 수정되었습니다.


### Version 8.0 @ 2020.11.13

**새로운 기능**
- 전체 플랫폼에 C++ 통합 API가 추가되었습니다. cpp_interface/[ITRTCCloud.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html)를 참고하십시오.
- 전체 플랫폼이 문자열 방 번호를 지원합니다. TRTCParams.strRoomId를 참고 바랍니다.
- 전체 플랫폼에 TXDeviceManager 장치 관리 유형이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.switchRoom이 추가되어 샘플링을 정지하지 않고도 방을 바꿀 수 있게 되었습니다.
- 전체 플랫폼에 API TRTCCloud.startRemoteView 렌더링 원격 비디오 화면 시작 기능이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.stopRemoteView 렌더링 원격 비디오 화면 중지 기능이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.getDeviceManager 장치 관리 유형 획득 기능이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.startLocalAudio 활성화 로컬 오디오의 샘플링과 업스트림이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.setRemoteRenderParams 원격 이미지 설정의 렌더링 설정이 추가되었습니다.
- 전체 플랫폼에 API TRTCCloud.setLocalRenderParams 원격 이미지 설정의 렌더링 설정이 추가되었습니다.

**최적화**
- Android에서 소프트웨어/하드웨어 디코딩 전환 로직이 개선되었습니다.
- Windows에서 System loopback 오디오 샘플링 음질 및 에코 제거 효과가 개선되었습니다.
- Windows에서 오디오 디바이스 선택 로직이 개선되어 Silent rate가 감소했습니다.
- Windows: 이중 대화 시나리오에서 오디오 손실이 감소했습니다.
- 전체 플랫폼에서 수동 수신 모드에서 역할 전환 시 발생하는 바로 재생 효과가 개선되었습니다.
- 전체 플랫폼에서 오디오 수신 로직이 개선되어 오디오 효과가 향상되었습니다.
- 전체 플랫폼에서 sendCustomCmdMsg 신뢰성이 개선되었습니다.

**오류 수정**
- iOS에서 muteLocalVideo 호출 시 로컬 비디오 렌더링이 중지되는 문제가 수정되었습니다.
- iOS에서 프론트엔드/백엔드 전환 시 호출 시스템 컴포넌트에서 크래시가 발생하는 문제가 수정되었습니다.
- iOS에서 오디오 활성화 시 인이어 모니터링 오디오가 계속 끊기는 문제가 수정되었습니다.
- Android에서 통화 음량 효과음 재생을 중단시켰을 때 통화가 끊겼을 경우, 효과음이 계속해서 재생되는 문제가 수정되었습니다.
- Android에서 간혹 오디오 샘플링 활성화가 실패하는 문제가 수정되었습니다.
- Windows에서 간혹 로컬 비디오 렌더링 시 블랙 스크린이 발생하는 문제가 수정되었습니다.
- Windows에서 프로세스 종료 시 간혹 크래시가 발생하는 문제가 수정되었습니다.
- Windows에서 블루투스 이어폰 지원이 개선되어 블루투스 이어폰에서 소리가 나지 않는 문제가 수정되었습니다.
- Windows에서 화면 공유 종료 시 포커스 상실 문제가 수정되었습니다.
- 전체 플랫폼에서 상태 콜백 패킷 손실률 통계 오류가 수정되었습니다.



### Version 7.9 @ 2020.10.27
**새로운 기능**
- Mac: 화면 공유가 선택된 창의 필터링 기능을 지원합니다. 공유하고 싶지 않은 창을 제거함으로서 보다 개선된 사생활 보호를 제공합니다.
- Windows: 화면 공유의 ‘공유 중’ 알림창 프레임 색상과 프레임 크기 설정 기능을 지원합니다.
- Windows: 화면 공유 기능으로 전체 화면을 공유할 때 고성능 모드를 지원합니다.
- 전체 플랫폼: 사용자 정의 암호 추가 기능을 지원하여 편집이 완료된 오디오/비디오 데이터를 노출된 C 인터페이스를 통해 2차 처리할 수 있게 되었습니다.
- 전체 플랫폼: TRTCRemoteStatistics에 오디오 정보 콜백 `audioTotalBlockTime`과 `audioBlockRate`가 추가되었습니다.

**최적화**
- iOS: 오디오 모듈의 실행 속도가 개선되어 첫 번째 오디오 프레임을 더 빨리 샘플링하여 전송할 수 있게 되었습니다.
- Windows: 시스템 루프의 에코 제거 알고리즘이 개선되어 시스템 루프백(SystemLoopback) 활성화 시 에코 제거 능력이 강화되었습니다.
- Windows: 화면 공유 기능의 창 샘플링 차폐 방지 능력이 개선되어 창 필터 설정 기능을 지원합니다.
- Android: 대부분의 Android 기종에서 인이어 모니터링 효과가 개선되어 인이어 모니터링 딜레이가 적정 수준까지 감소되었습니다.
- Android: Music 모드(startLocalAudio일 시에 지정)에서의 P2P 딜레이가 개선되었습니다.
- 전체 플랫폼: 수동 구독 모드에서 관객과 호스트 역 전환 시의 음성 원활성이 개선되었습니다.
- 전체 플랫폼: 음성/영상 통화에서 약한 네트워크에 대한 저항성이 개선되어 네트워크 환경이 좋지 않은 상황에서의 오디오 유연성이 향상되었습니다.

**오류 수정**
- iOS: 일부 시나리오에서 간혹 비디오 화면이 렌더링되지 않는 문제가 수정되었습니다.
- iOS: 사용자가 이어폰을 착용한 상태에서 음질이 Default일 경우 간혹 잡음이 발생하는 문제가 수정되었습니다.
- iOS: 현재 알려져 있는 메모리 누수 문제 중 일부가 수정되었습니다.
- iOS: 간혹 replaykit 확장 녹화 종료 시 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 시뮬레이터 환경에서의 편집 문제가 해결되었습니다.
- Android: 일부 모바일 기기가 App에서 장기간 백엔드로 전환된 이후에 다시 프론트엔드로 전환될 경우 간혹 오디오-비디오 동기화가 이루어지지 않는 문제가 수정되었습니다.
- Android: 백엔드 전환 이후 마이크 릴리스가 되지 않는 문제가 수정되었습니다.
- Android: SDK 내부의 일부 OpenGL 리소스가 제때 릴리스되지 않는 문제가 수정되었습니다.
- Windows: 개별 시나리오에서 간혹 잡음이 발생하는 문제가 수정되었습니다.
- 전체 플랫폼: 간혹 발생하는 크래시 문제 중 일부가 해결되어 SDK 안정성이 향상되었습니다.

### Version 7.8 @ 2020.09.29
**새로운 기능**
- Mac: 시스템 음량 변화 콜백이 추가되었습니다. 세부 사항은 [TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f)를 참고하십시오.
- Windows: 크로스 스크린을 지원하여 지정된 영역에 화면을 공유하는 기능이 추가되었습니다.
- Windows: 창 공유가 필터 기능을 지원하여 지정된 창에 대한 차폐 방지 기능이 추가되었습니다. 세부 사항은 [TRTCCloud.addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06) 및 [TRTCCloud.removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2)를 참고하십시오.
- Windows: 시스템 음량 변화 콜백이 추가되었습니다. 세부 사항은 [ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12)를 참고하십시오.

**최적화**
- iOS: VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
- iOS & Mac: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2)를 참고하십시오.
- Android: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d)를 참고하십시오.
- Android: 오디오 라우팅 정책이 개선되어 이어폰 착용 시 오디오가 이어폰으로만 재생되는 기능이 지원됩니다.
- Android: 일부 시스템에서 저지연 샘플링 재생을 지원하여 Android 시스템의 통화 딜레이가 감소되었습니다.
- Android: VODPlayer 와 trtc 동시 사용 및 에코 제거를 지원합니다.
- Windows: 가상 카메라 e2eSoft Vacm가 호환됩니다.
- Windows: startLocalPreview 과 startCameraDeviceTest 동시 호출이 지원됩니다.
- Windows: 화면 공유가 주 경로를 이용하는 동시에, startLocalPreview 호출 시 로컬 미리보기를 활성화합니다.
- Windows: SDK 내부 재생 버퍼로 인한 오디오 딜레이가 커지는 문제가 감소했습니다.
- Windows: 오디오 실행 로직이 개선되어 재생 상황에 한정하여 마이크를 점용하지 않습니다.



**오류 수정**
- iOS: iPhone SE에서 오디오 재생 음량이 작은 문제가 수정되었습니다.
- iOS: 서브 방(TRTCCloud.createSubCloud)에서 muteRemoteAudio 호출 시 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 간혹 렌더링 중 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 프론트엔드/백엔드 전환 시 일부 iPad에서 비디오 랜더링 중 간혹 메인 스레드가 크래시되는 문제가 수정되었습니다.
- iOS: 알려진 메모리 누수 문제가 수정되었습니다.
- iOS: iOS14에서 ‘로컬 네트워크에 있는 장치를 찾아 연결하기’ 알림이 뜨는 문제가 수정되었습니다.
- Mac: getCurrentCameraDevice가 계속 nil을 반환하는 문제가 수정되었습니다.
- Mac: 일부 USB 카메라를 열 수 없는 문제가 수정되었습니다.
- Mac: 화면 공유의 지정 영역 면적이 0일 경우 크래시가 발생하는 문제가 수정되었습니다.
- Android: READ_PHONE_STATE 권한이 설정되지 않았을 경우 Android5.0 기기에서 크래시가 발생하는 문제가 수정되었습니다.
- Android: 블루투스 이어폰을 제거한 후 재연결했을 때, 오디오 샘플링 및 재생 시 오류가 발생하는 문제가 수정되었습니다.
- Android: 알려진 크래시 문제가 수정되었습니다.
- Windows: 64비트 SDK에서 화면 공유 기능을 여러 번 활성화할 경우 크래시가 발생하는 문제가 수정되었습니다.
- Windows: 일부 시스템에서 OpenGL을 사용할 경우 크래시가 발생하는 문제가 수정되었습니다.


### Version 7.7 @ 2020.09.08

**최적화**

- 전체 플랫폼: 보조 경로(화면 공유)의 실행 속도가 향상되었습니다.
- iOS: 내부 스레드 모델이 개선되어 30번 경로 이상에서 동시 재생 시나리오의 실행 안정성이 향상되었습니다.
- iOS & Android: Audio 모듈 성능이 개선되어 SOF의 샘플링 딜레이가 향상되었습니다. 신규 버전에서는 첫 번째 오디오 프레임을 더 빨리 획득할 수 있습니다.
- iOS & Android: VOD 플레이어와 TRTC를 동시에 사용할 경우의 음량 크기 및 음질이 향상되었습니다.
- iOS & Android: wav 오디오 포맷의 배경 음악과 효과음 파일 지원이 추가되었습니다.
- Windows: 일부 저가형 카메라의 지나치게 높은 CPU 사용률 문제가 최적화되었습니다.
- Windows: 멀티 USB 카메라와 마이크에 대한 호환성 최적화로 디바이스의 실행 성공률이 향상되었습니다.
- Windows: 카메라와 마이크 디바이스 선택 정책 최적화로 카메라 또는 마이크 사용 중 소켓으로 인한 샘플링 오류 문제를 방지하였습니다.

**오류 수정**

- 전체 플랫폼: 네크워크가 약한 경우, muteLocalVideo 및 muteLocalAudio 인터페이스 호출 시 간혹 재생 오류가 발생하는 버그가 수정되었습니다.
- iOS: 저가형 iPhone 또는 iPad에서 오디오 재생 시 간혹 재생에 실패하는 버그가 수정되었습니다.
- iOS: iPad Pro에서 화면 공유 기능으로 인해 공유된 화면이 늘어나는 문제가 수정되었습니다.
- iOS: 사용자가 권한을 거절했음에도 App 내부 화면 기여가 계속해서 화면 녹화 권한을 요청하는 문제가 수정되었습니다.
- Windows: 노트북 또는 데스크톱이 장기간 휴면 상태일 때, 나가기 [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) 이벤트 알림이 콜백되지 않는 문제가 수정되었습니다.
- Windows: Music 음질 모듈에서 시스템 오디오 루프백 [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23)을 활성화하면 에코가 누출되는 문제가 수정되었습니다.
- Windows: enterRoom과 exitRoom을 빠르게 호출하여 방 입장/퇴장을 할 경우 간혹 소리가 들리지 않는 버그가 수정되었습니다.
- Windows: Visual Stuido 2010 프로젝트에서 SDK의 편집 호환성 문제가 수정되었습니다.
- Windows: 수동 수신 모드(즉, [setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5))에서 onUserVideoAvailable 이벤트 콜백이 중복 수신되는 문제가 수정되었습니다.


### Version 7.6 @ 2020.08.21
**새로운 기능**

- Windows: HWND 유형의 렌더링 창의 실시간 조정을 보다 쉽게 최적화할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299)와 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e) 인터페이스를 추가하였습니다.
- Windows: 현재 Windows PC가 음소거로 설정되어 있는지를 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스를 추가하였습니다.
- Windows: 현재 Windows PC를 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스를 추가하였습니다.
- Mac: View 렌더링 영역의 실시간 조정을 더 쉽게 최적화할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) 및 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스를 추가하였습니다.
- Mac: 현재 Mac이 음소거로 설정되어 있는지 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) 인터페이스를 추가하였습니다.
- Mac: 현재 Mac을 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) 인터페이스를 추가하였습니다.
- iOS: View 렌더링 영역의 실시간 조정을 더 쉽게 최적화할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) 및 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스를 추가하였습니다.
- iOS: TRTCCloudDelegate에 [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) 콜백을 추가하고, 몇몇 콜백 함수의 이름을 변경했습니다. 변경된 이름은 각각 순서대로 [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a), [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e)입니다.
- Android: TRTCCloudListener에 [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) 콜백을 추가하고, 몇몇 콜백 함수의 이름을 변경했습니다. 변경된 이름은 각각 순서대로 [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902), [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7)입니다.

**최적화**

- 전체 플랫폼: enterRoom의 프로토콜 정책이 개선되어 방 입장 속도와 성공률이 향상되었습니다.
- 전체 플랫폼: 다수의 오디오를 구독할 경우에 발생하는 전반적 성능 소모와 랙 문제가 개선되었습니다.
- Mac: 화면 공유에 지정된 창의 지정된 영역 공유 기능이 지원됩니다.

**오류 수정**

- 전체 플랫폼: 방에서 퇴장하지 않은 상태에서 다른 방에 입장할 경우 SDK에서 onEnterRoom이 트리거되지 않는 버그가 수정되었습니다.
- 전체 플랫폼: 블랙 스크린을 유발할 수 있는 몇몇 내부 버그가 수정되었습니다.
- 전체 플랫폼: startRemoteSubStreamView 사전 호출 시 공유된 화면이 정상적으로 표시되지 않는 문제가 수정되었습니다.
- Windows: 알려진 몇몇 핸들 및 GDI 누락이 수정되었습니다.
- Windows: 알려진 크래시 문제 다수가 수정되었습니다.
- Windows: 카메라와 마이크를 뺀 후 다시 꽂았을 때 자동으로 장치가 활성화되지 않는 문제가 수정되었습니다.
- iOS: iOS 10에서 배경음악 인터페이스를 특정 규칙의 파일 경로로 이동했을 때 크래시가 발생하는 버그가 수정되었습니다.
- Android: 빈번하고 빠른 enterRoom 및 exitRoom 이후 간혹 소리가 들리지 않는 문제가 수정되었습니다.
- Android: 간혹 녹화 시 화면 흐림 현상이 나타나는 문제가 수정되었습니다.


### Version 7.5 @ 2020.07.31

**새로운 기능**

- 더블 스택 IPV6와 IPV6 only에 대한 지원이 추가되었습니다.
- 특급 소형 수업 지원에 사용되는 다수 방에서의 풀 스트림 능력이 향상되었습니다.
- 클라우드 MCU 혼합 스트림에 배경 이미지(모니터링 필요에 따라 이미지는 TRTC 콘솔에 먼저 업로드해야 함) 설정 기능이 추가되었습니다.
- 클라우드 MCU 혼합 스트림에 A+B=>C와 A+B=>A 모드가 추가로 지원됩니다.
- 실시간 상태 콜백 onStatistics에 재생 버퍼 시간 필드 jitterBufferDelay가 추가되었습니다.

**최적화**

- 클라이언트간 마이크 연결 딜레이가 감소되었습니다. 7.5버전 클라이언트간 통화 및 마이크 연결 딜레이가 7.4버전 기준 40% 감소되었습니다.
- 모바일 디바이스의 인이어 모니터링 딜레이가 감소되었으며, 인이어 모니터링에 변성 및 잔향과 같은 음향 효과 설정이 지원됩니다.
- 클라이언트 네트워크 지터 평가 알고리즘이 개선되어 재생 딜레이가 감소되었습니다.
- Android SDK의 클라이언트간 마이크 연결 통화 딜레이가 감소되었습니다.
- 인이어 모니터링 딜레이 문제가 한층 더 개선되었습니다.
- 재생 view 동적 전환 시 블랙 스크린이 발생하는 문제가 개선되었습니다.

**오류 수정**

- 하나의 함수에서 연속으로 playBGM과 pauseBGM을 호출하면 재생이 되지 않는 문제가 수정되었습니다.
- 간혹 방에서 나간 이후에도 onEnterRoom 콜백을 수신할 수 있는 문제가 수정되었습니다.
- 일부 모델에서 초저해상도 인코딩 및 복구가 되지 않는 문제가 수정되었습니다. 

###  Version 7.4 @ 2020.06.24 

**최적화**

인이어 모니터링이 음량 설정을 지원합니다.

**오류 수정**

- Android 버전에서 가로세로 화면 전환 시 로컬 화면이 깜빡이는 문제가 수정되었습니다.
- 일부 Android 핸드폰에서 사용자 정의 비디오를 전송하면 정상적으로 인코딩이 진행되지 않는 문제가 수정되었습니다.
- 오디오 처리 시 간혹 데이터 패키지에서 크래시가 발생하는 문제가 수정되었습니다.



###  Version 7.3 @ 2020.06.01

**새로운 기능**

- 기존 인터페이스가 호환되는 상황에서 신규 음향 효과 관리 인터페이스 TXAudioEffectManager가 추가되었습니다. 해당 기능은 더욱 빠르고 다양한 음향 효과 편집을 지원합니다.
- 비디오 편집 매개변수 setVideoEncoderParam에 minVideoBitrate 옵션이 추가되었습니다. 화질 요구사항이 높은 생방송 클라이언트에게 추천합니다.

**최적화**

- 오디오에 순간 노이즈 감소 기능이 지원됩니다. setAudioQuality(TRTCAudioQualitySpeech)를 통해 활성화할 수 있습니다.
- 음향 효과 파일이 asset 팩 음향 효과 파일을 지원합니다.
- 로컬 비디오 해상도가 향상되었습니다.
- 사용자 정의 렌더링 재생에 텍스쳐 매핑 방식이 지원되어 성능 저하 문제가 개선되었습니다.
- 카메라 샘플링 해상도 선택 로직이 개선되어 시각 효과가 향상되었습니다.
- 에코 처리 효과가 향상되었습니다.
- 모든 링크에서 128kbps 고음질 입체 음성을 지원합니다. setAudioQuality(TRTCAudioQualityMusic) 인터페이스를 통해 설정할 수 있습니다.
- SPEECH 음성 모드를 지원합니다. 회의장에서 사용되는 음성 통화에 적합합니다. 더 강력한 노이즈 감소(ANS) 효과를 원하실 경우 setAudioQuality(TRTCAudioQualitySpeech)에서 설정하실 수 있습니다.
- 다중 배경음악 병행 재생 기능이 지원됩니다. 보컬과 서브보컬이 분리된 노래방 시나리오 지원에 사용됩니다. 배경음악 순환 재생도 함께 지원됩니다.
- muteLocalVideo 호출 후 startLocalPreview를 호출함으로써 ‘미리보기만 하고 푸시 스트림은 하지 않는’ 효과를 지원합니다. enterRoom 전 startLocalPreview 호출로 해당 기능을 실행하실 수 있습니다.

**오류 수정**

- 사용자 정의 비디오 샘플링 시 간혹 SDK 내부 OpenGL 컨텍스트 오류 크래시가 발생하는 문제가 수정되었습니다.
- 방 입장 전 setLocalVideoRenderListener 사용자 정의 렌더링 콜백이 트리거되지 않는 문제가 수정되었습니다.
- 가로 화면 모드에서 전/후 카메라로 전환 시 재생 화면이 거꾸로 표시되는 문제가 수정되었습니다.
- 방 입장 전 startLocalPreview을 호출하면 방 입장 후에 간혹 화면 출력 오류가 나타나는 문제가 수정되었습니다.
- 하드 코더에서 간혹 크래시가 발생하는 문제가 수정되었습니다.
- 로컬 오디오 녹화 시 간혹 끊김 현상이 발생하는 버그가 수정되었습니다.
- 푸시 스트림 중지(muteLocalVideo, muteLocalAudio) 시 강제 종료 또는 크래시 후 다시 방에 입장하면 오디오/비디오가 자동 재생되지 않는 문제가 수정되었습니다.



###  Version 7.2 @ 2020.04.16 

**새로운 기능**

Android에 핸드폰 녹화 기능이 추가되었습니다. 해당 기능은 핸드폰을 사용한 생방송을 지원합니다.

**최적화**

- 통화 시나리오에서 중저가 Android 핸드폰의 성능 소모량이 개선되어 통화 품질이 향상되었습니다.
- 필터, 그린 스크린과 같은 시각 효과 인터페이스를 개선하고 TXCBeautyManager에 통합하여 통일된 호출 방식을 구현했습니다.

**오류 수정**

역할 전환 시 사용자 정의 ID가 간혹 제때 적용되지 않는 문제가 수정되었습니다.



###  Version 7.1 @ 2020.03.27 

**최적화**

- C++ STL 기초 라이브러리의 완전 정적 편집
- 통화 음량이 기본적으로 ANS, AGC를 활성화하여 통화 모드에서의 음질이 향상되었습니다.
- 혼합 스트림 사전 설정 템플릿 활용성이 개선되었습니다.
- 혼합 스트림이 개선되어 성공률이 향상되었습니다.

**오류 수정**

- 방에 입장한 이후 AGC를 반복해서 활성/비활성화할 경우 처리한 오디오가 전부 0이 되는 문제가 수정되었습니다.
- 속도 측정 시 다른 API 호출의 응답이 느려지는 문제가 수정되었습니다.
- 시스템에 의해 전화가 중단된 이후 음량이 2배로 증가하고 노이즈가 섞이는 문제가 수정되었습니다.
- 방 입장 시 자동으로 릴레이를 하는 문제가 수정되었습니다.



###  Version 7.0 @ 2020.03.09 

- 3A 활성화 정책이 개선되었습니다.
- mcu 혼합 스트림 활용성이 향상되었습니다.
- 약한 네트워크에서의 지터 방지 능력이 향상되어 네트워크가 약한 환경에서 오디오가 보다 원활해졌습니다.
- 여러 차례 교대로 방 입장과 퇴장을 반복할 경우 메모리 누수가 발생하는 문제가 해결되었습니다.



###  Version 6.9 @ 2020.01.14 

**새로운 기능**

- Android 10.0 시스템에 대한 지원이 추가되었습니다.
- API: snapshotVideo()가 추가되어 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.
- API: pauseAudioEffect, resumeAudioEffect 음향 효과가 추가되어 일시정지/복구 제어 기능을 지원합니다.
- API: setBGMPlayoutVolume, setBGMPublishVolume, BGM이 추가되어 로컬 재생과 푸시 스트림 오디오 믹싱을 지원합니다.
- API: setRemoteSubStreamViewRotation 우회 비디오 재생이 추가되어 렌더링 각도 회전 조정을 지원합니다.
- 전역 음량 형식 모드: setSystemVolumeType(TRTCSystemVolumeTypeVOIP)이 추가되어 계속적인 통화 음량 사용을 지원합니다. 블루투스 이어폰의 자체 마이크에서 발생하는 샘플링 전환 문제 해결에 사용됩니다.
- enterRoom 매개변수 TRTCParams에 streamId 속성이 추가됩니다. 현재 사용자의 CDN 라이브 방송 스트리밍 ID 설정에 사용되어 CDN 라이브 방송 바인딩을 편리하게 할 수 있도록 합니다.
- enterRoom 매개변수 TRTCParams에 cloudRecordFileName 속성이 추가됩니다. 클라우드에 녹화되는 라이브 방송의 파일명을 설정할 수 있습니다.
- 시나리오 TRTCAppSceneAudioCall이 추가되었습니다. enterRoom 시 설정할 수 있습니다. 해당 시나리오에서 음성 통화와 관련된 TRTC SDK에 대한 전반적 개선이 이루어졌습니다.
- 시나리오 TRTCAppSceneVoiceChatRoom이 추가되었습니다. enterRoom 시 설정할 수 있으며, TRTC SDK를 활성화하면 음성 채팅방 시나리오를 최적화할 수 있습니다.

**최적화**

- 비디오 스트리밍 중 중단에 대한 녹화 서비스의 저항력을 강화하여 원거리 녹화 파일의 완전성을 확보했습니다.
- 일부 기종에서 하드웨어 디코딩 시 오디오/비디오 동기화가 이루어지지 않는 문제가 개선되었습니다.
- 비디오 화면이 1080P 고해상도 샘플링을 지원하여 핸드폰 라이브 방송을 PC로 시청하는 시나리오에서의 화면 해상도가 향상되었습니다.
- 에러 코드 개선 및 방 입장 에러 코드가 간소화되었습니다.
- 파일이 간혹 몇 초씩 느리게 열리던 문제가 수정되었습니다.

**오류 수정**

- 간혹 HTTP 컴포넌트에서 크래시가 발생하는 문제가 수정되었습니다.
- 음향 효과 재생 시 간혹 콜백이 완료되지 않는 문제가 수정되었습니다.
- 간혹 방 입장 실패 이후 복구가 되지 않는 문제가 수정되었습니다.



###  Version 6.8 @ 2019.11.15 

**새로운 기능**

- 인이어 모니터링 기능이 추가되었습니다.
- 방 입장 시 수동 풀 스트림을 지정할 수 있게 되었습니다.
- 인터페이스 getBeautyManager 추가 및 뷰티 필터와 포토샵 동적 효과 인터페이스 통합이 이루어졌습니다.
- 엔터프라이즈 버전에 피부 미백, 치아 미백, 주름 개선, 하안검 제거 등과 같은 신규 포토샵 기능이 추가되었습니다.
- onRemoteUserEnterRoom / onRemoteUserLeaveRoom 콜백이 추가되었습니다. 마이크가 없는 사용자의 라이브 방송 입장/퇴장 알림을 지원합니다.

**최적화**

- pts 생성 메커니즘이 개선되었습니다.
- 네트워크 전환 이후 자동으로 더 나은 액세스 포인트를 선택하도록 개선되었습니다.
- startRemoteView가 사전 호출을 지원합니다.

**오류 수정**

알려진 크래시 문제 등 안정성 문제가 수정되었습니다.



###  Version 6.7 @ 2019.09.30 

**새로운 기능**

- AAR 패키지에 권한 획득 설정이 추가되었습니다.
- Android 8.0 이상 시스템의 CPU 점용 평가가 추가되었습니다.

**최적화**

- 푸시 소모 시간이 최적화되었습니다.
- 단일 사용자가 재생 음량을 독립적으로 조절할 수 있는 기능을 지원합니다.

### Version 6.6 @ 2019.08.02 

**새로운 기능**

- 오디오 로컬 녹화 기능이 추가되었습니다.
- 첫 프레임 오디오, 비디오 발송 콜백 인터페이스가 추가되었습니다.
- 시스템 음량 유형 설정 인터페이스가 추가되었습니다.
- 음향 효과 인터페이스가 추가되었습니다. 짧은 음향 효과 재생을 지원합니다.
- 오디오 사용자 정의 콜백 인터페이스가 출력한 데이터를 수정할 수 있게 되었습니다.

**최적화**

- 방 입장이 개선되어 입장 소모 시간이 감소하고, 입장 성공률이 향상되었습니다.
- 원격 비디오 인터페이스 mute가 지원됩니다.
- 방 입장 오류 코드가 통일됩니다. onEnterRoom 콜백을 통해 result&lt;0 방 입장 오류가 표시됩니다.
- Demo가 개선되었으며 저지연 대형 방 지원이 추가되었습니다.
- 플레이어에 음량 설정 인터페이스와 음량 크기 콜백 인터페이스가 추가되었습니다.
- 사용자 정의 발송 비디오가 로컬 렌더링을 지원합니다.
- 사용자 정의 샘플링 발송 비디오가 1080P를 지원합니다.
- 로컬 및 원격 렌더링이 SurfaceView 방식을 지원합니다.

**오류 수정**

- 릴레이 혼합 스트림 관련 문제가 수정되었습니다.
- 로컬 미리보기 각도가 맞지 않는 문제가 수정되었습니다.



###  Version 6.5 @ 2019.06.12 

**새로운 기능**

라이브 방송 모드(TRTCAppSceneLIVE)에 ‘저지연 대형 방’ 기능이 추가되었습니다.

- 오디오/비디오 최적화를 위한 UDP 프로토콜을 채용함으로써 약한 네트워크에 대한 저항 능력이 강화되었습니다.
- 평균 시청 딜레이를 1초로 만들어 시청자와 호스트간 적극적인 상호작용이 가능해졌습니다.
- 하나의 방에 최대 10만 명이 입장할 수 있게 되었습니다.

**최적화**

- 약한 네트워크 환경에서의 오디오-비디오 동기화가 이루어지지 않는 버그가 개선되었습니다.
- onStatistics 상태 콜백이 개선되었습니다. 콜백이 존재하는 스트림에 한합니다.
- 라이브 방송 TXLivePlayer 재생 버퍼 로직이 개선되어 랙 비율이 감소했습니다.
- 먼저 muteLocalVideo한 후 재생 취소 시 화면 복구 속도가 개선되었습니다.
- 딜레이와 패킷 손실률이 높은 네트워크 환경에서의 QoE 알고리즘이 개선되어 약한 네트워크에 대한 저항력이 강화되었습니다.
- 디코더 성능을 개선하여 초저가형 Android 핸드폰에서 딜레이가 점차 증가하는 버그를 해결했습니다.
- 오디오 평가 알고리즘(enableAudioVolumeEvaluation)이 개선되어 음량 평가가 더욱 빠르게 이루어집니다.
- 영상 통화(TRTCAppSceneVideoCall) 모드에서의 QoE 알고리즘이 개선되어 1v1 통화 모드의 경우 약한 네트워크 환경에서의 원활함이 더욱 향상되었습니다.

  

**오류 수정**

- 간혹 enterRoom 시 콜백이 오지 않는 버그가 수정되었습니다.
- 오디오 샘플링 중지 이후 재생을 해도 소리가 들리지 않는 버그가 수정되었습니다.
- 로컬 렌더링 view를 삭제한 이후 다시 추가했을 때 그린 스크린이 발생하는 버그가 수정되었습니다.
- 사용자 정의 렌더링 콜백(setRemoteVideoRenderDelegate)과 관련해 원격 화면 해상도가 540P 이상일 경우 콜백을 10회만 하는 버그가 수정되었습니다.



###  Version 6.4 @ 2019.04.25 

**새로운 기능**

- 로컬 표시 이미지와 인코더 출력 이미지 인터페이스가 추가되었습니다.
- 혼합 스트림 setMixTranscodingConfig API의 설정 콜백 함수가 추가되었습니다.
- 엔터프라이즈 버전에 눈 확대, 안면 축소, V자 턱 및 모션 행거 기능이 추가되었습니다.

**최적화**

- 약한 네트워크 환경에서의 원활성이 향상되었습니다.
- 음량 크기 콜백 알고리즘이 개선되어 음량 콜백 수치가 더욱 합리적으로 변경되었습니다.
- 사용자 정의 오디오, 비디오 데이터 발송 시 외부 지정 데이터 프레임 타임스탬프가 지원됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 roomID 매개변수를 지원합니다. 각 방 간 마이크 연결 스트리밍에 사용됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 pureAudio 매개변수를 지원합니다. 음성 통화 전용 시나리오에서의 음성 혼합 스트림 및 녹화에 사용됩니다.
- 저가형 Android 기기에서의 720p 비디오 디코딩 성능 문제가 개선되었습니다.

**오류 수정**
- 음성 핸즈프리 전환이 이루어지지 않는 버그가 수정되었습니다.
- 라이브 방송(TXLivePlayer) 딜레이가 증가한 이후에 복구되지 않는 버그가 수정되었습니다.
- 라이브 방송 시나리오 setVideoEncoderRotation이 적용되지 않는 버그가 수정되었습니다.
- Android에서 마이크 권한을 금지한 이후 오류 콜백이 오지 않는 버그가 수정되었습니다.
- Android 9.0 시스템에서 Demo를 열었을 때 창이 팝업되는 문제가 수정되었습니다.
- 음량 조절 버튼으로 시청자 측 음성을 조절할 수 없는 문제가 수정되었습니다.



### Version 6.3 @ 2019.04.02 

**새로운 기능**

- Android 플랫폼 64비트 지원이 추가되었습니다.
- 사용자 정의 비디오 샘플링 인터페이스: TRTCCloud >> sendCustomVideoData가 추가되었습니다.
- 사용자 정의 비디오 샘플링 인터페이스: TRTCCloud >> sendCustomAudioData가 추가되었습니다.
- 사용자 정의 비디오 렌더링 인터페이스: TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다.
- 사용자 정의 오디오 데이터 콜백 인터페이스: TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다. 다음을 지원합니다.
  - 마이크 샘플링 데이터 반환: TRTCAudioFrameDelegate >> onCapturedAudioFrame.
  - 각 원격 사용자의 오디오 데이터 반환: TRTCAudioFrameDelegate >> onPlayAudioFrame.
  - 혼합 이후 스피커로 재생한 오디오 데이터 반환: TRTCAudioFrameDelegate >>onMixedPlayAudioFrame.





###  Version 6.2 @ 2019.03.08 

**새로운 기능**
- 필터 농도 설정 인터페이스 setFilterConcentration()이 추가되었습니다.
- sendSEIMsg() 인터페이스가 추가되었습니다. 비디오 프레임의 SEI 헤드 정보가 사용자 정의 메시지를 발송하는 것을 지원합니다. 비디오 스트리밍 중 타임스탬프 정보 삽입에 사용됩니다.
- 라이브 룸 간 통화 기능인 connectOtherRoom이 추가되었습니다. 이미 존재하는 두 개의 TRTC 방을 서로 연결하는 기능으로, 라이브 방송 중 호스트 PK에 사용됩니다.

**최적화**
- CPU 사용률 및 안정성이 개선되었습니다.
- 약한 네트워크(연결 상태가 좋지 않은 네트워크 환경)에서의 화면 해상도가 향상되었습니다.
- TRTCCloud의 다중 인스턴스 기능을 취소하고 생성 모드를 단일 인스턴스 모드로 변경하여 다수의 TRTCCloud 인스턴스가 서로의 네트워크 리소스를 점유하는 일이 없도록 하였습니다.

**오류 수정**

음성 통화 전용 시나리오(예: 마피아 게임)에서 릴레이 푸시 스트림 기능을 복구하려면 TRTCParam의 bussInfo 필드를 함께 사용해야 합니다.



###  Version 6.1 @ 2019.01.31 

**최적화**

- 화면 공유 스트리밍 관전 기능을 지원합니다.
- 사용자 정의 비디오 데이터 발송을 지원합니다.
- CDN 푸시와 혼합 스트림 구현이 개선됩니다.
- 방 입장이 라이브 방송과 영상 통화 시나리오로 구분됩니다.
- 안정성이 개선되고, 간혹 발생하는 크래시 문제가 해결되었습니다.
- 트레픽 제어가 개선되어 약한 네트워크 환경에서의 성능이 향상되었습니다.



###  Version 6.0 @ 2019.01.18 

**최적화**

- 아키텍처가 LiteAV 커널로 업데이트되었습니다.
- 새로운 QoS 알고리즘을 채용하여 렉 발생률이 감소하고 원활성이 향상되었습니다.
- 새로운 Audio 모듈을 채용하여 각종 네트워크 상황에서의 오디오 품질이 대폭 향상되었습니다.
- 대형/소형 스트리밍 듀얼 채널 인코딩 기능을 지원합니다(Windows와 Mac 기기에서만 활성화할 것을 추천).
- CDN 푸시와 혼합 스트림 기능을 지원합니다.
