Live Event Broadcasting(LEB)은 LVB의 초저지연 라이브 방송 시나리오 확장판으로, 기존 라이브 방송 프로토콜보다 딜레이 시간이 짧아 시청자에게 밀리초 단위의 고품질 **라이브 방송 시청 경험**을 제공합니다.
혼동을 방지하기 위해 LEB 서비스를 이용하기 전 [LEB 서비스 요금](https://intl.cloud.tencent.com/document/product/267/39969)을 미리 읽어보시고 청구 항목 및 가격을 알아보시기 바랍니다.

> ! LEB는 WebRTC 프로토콜의 저지연 기능을 사용하기 때문에 B-프레임은 기본적으로 지원하지 않으며 오디오 코덱은 opus 코덱입니다. LEB 스트림 재생을 보장하기 위해, 푸시 스트림이 B-프레임을 수반하거나 오디오 인코딩이 opus 인코딩이 아닐 경우, CSS 백엔드는 자동으로 B-프레임을 opus 인코딩으로 트랜스 코딩합니다. 이로 인해 [표준 트랜스 코딩 비용](https://intl.cloud.tencent.com/document/product/267/39604)이 발생합니다.

[](id:app)
## App 액세스
### 관련 설명
iOS 및 Android의 애플리케이션에 라이브 SDK를 통합하여 App에서의 라이브 방송 푸시 스트림/재생 기능을 구현할 수 있습니다.

- **App 라이브 방송 푸시 스트림**: 카메라 화면 수집 또는 휴대폰 인터페이스 수집을 지원하며, RTMP 프로토콜을 통해 CSS에 스트림을 빠르게 푸시할 수 있습니다. 자세한 내용은 [카메라 푸시 스트림](https://www.tencentcloud.com/document/product/1071/38157) 및 [화면 녹화 푸시 스트림](https://www.tencentcloud.com/document/product/1071/41878)을 참고하십시오.
- **App 라이브 방송 재생**: WebRTC 재생 프로토콜을 지원하며, LEB와 연동하여 저지연 라이브 방송 경험을 빠르게 구현합니다. 자세한 내용은 [LEB 풀 스트림](https://www.tencentcloud.com/document/product/1071/41875)을 참고하십시오.

>?  라이브 SDK는 CSS, IM, TRTC 및 기타 서비스를 통해 다중 사용자 멀티미디어 저지연 상호 연결 및 통신 효과를 구현합니다. 다중 인터렉티브 마이크 연결 효과를 제공하며, 마이크를 연결하지 않는 시청자도 라이브 방송 서비스를 통해 시청할 수 있습니다. 자세한 내용은 [Mic Connect](https://www.tencentcloud.com/document/product/1071/42210)를 참고하십시오.

### Demo 체험
TCToolkit은 Tencent Cloud에서 개발한 오픈 소스 종합 오디오/비디오 솔루션입니다. 이를 사용하여 LEB의 밀리초 수준의 저지연 라이브 스트림 재생 기능을 체험해 볼 수 있습니다.
<table>
  <tr>
    <th><div align="center">개발측</div></th>
    <th><div align="center">데모</div></th>
    <th><div align="center">푸시 스트림 예시(Android)</div></th>
    <th><div align="center">재생 예시(Android)</div></th>
  </tr>
  <tr>
    <td >Android</td>
    <td style="text-align:center"><img width="150" src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png"> </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200" src="https://main.qcloudimg.com/raw/dca4b24bc363d25c9ea45e60859a2f6d.png"/>
      </div>
    </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200"  src="https://main.qcloudimg.com/raw/6dd7c02dc2381d84225c2f2f286e7358.png"/>
      </div>
    </td>
  </tr>
  <tr>
      <td >iOS</td>
    <td style="text-align:center">점검 중</td>
  </tr>
</table>



[](id:web)
## Web 액세스
### 관련 설명
라이브 방송 푸시 스트림 및 재생이 필요한 웹 사이트가 있는 경우 다음 방법을 통해 액세스할 것을 권장합니다.

- **Web 라이브 방송 푸시 스트림**: 브라우저의 범용 WebRTC 표준을 기반으로 설계 및 캡슐화되었으며, 코드 스니펫을 도입하여 브라우저에서 라이브 방송 푸시 스트림을 구현할 수 있습니다. 자세한 내용은 [WebRTC 프로토콜 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/41620)을 참고하십시오.
>! 
>- WebRTC 푸시 스트림 오디오 인코딩은 opus 인코딩만 지원합니다. LVB의 재생 프로토콜(RTMP, FLV, HLS)을 사용하여 재생하는 경우, 정상적인 시청을 보장하기 위해 CSS 백엔드는 자동으로 오디오 트랜스 코딩을 aac 인코딩으로 전환합니다. 이로 인해 오디오 트랜스 코딩 요금이 발생되며, 자세한 내용은 [오디오 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/267/39604#a_trans)을 참고하십시오. (LEB만 사용하는 경우 오디오 트랜스 코딩이 시작되지 않습니다.)
>- WebRTC 프로토콜을 사용하여 스트림을 푸시하며 각 푸시 도메인의 동시 푸시 스트림 수는 기본적으로 **1000개** 로 제한됩니다. 제한 확장은 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청할 수 있습니다. 

- **Web에서 라이브 재생**: 모바일 및 PC 브라우저에서 WebRTC 스트림 재생을 지원하고 기존 라이브 스트리밍 프로토콜을 사용하여 재생하는 것보다 훨씬 낮은 밀리초 대기 시간으로 뛰어난 스트리밍 경험을 제공하는 웹 플레이어 SDK [TCPlayerLite](https://www.tencentcloud.com/document/product/266/33977)를 사용하는 것이 좋습니다.
>! WebRTC를 지원하지 않는 브라우저 환경에서 플레이어에 전달된 WebRTC 주소는 정상적인 미디어 재생을 위해 자동 변환됩니다. 모바일 브라우저는 기본적으로 HLS로, PC 브라우저는 기본적으로 FLV로 변환됩니다.

### Demo 체험

- **Web에서 라이브 푸시**: **CSS 콘솔**>[Web 푸시 툴](https://console.cloud.tencent.com/live/tools/webpush)을 통해 Web 푸시 기능을 테스트할 수 있습니다.
- **Web에서 실시간 재생**: [TCPlayer](https://tcplayer.vcube.tencent.com/)를 사용하여 웹에서 재생을 테스트할 수 있습니다.
>?
>- Web 라이브 방송 푸시 스트림 및 풀 스트림은 모두 표준 WebRTC 프로토콜을 사용합니다. Web 푸시 스트림에 B-프레임이 포함되지 않고 오디오가 OPUS 오디오 형식으로 인코딩된 경우, 오디오 트랜스 코딩 및 B-프레임 트랜스 코딩 비용이 발생하지 않습니다.
>- WebRTC Live Demo는 다중 해상도 기능을 지원합니다. CSS 콘솔의 **기능 설정** > [**라이브 방송 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)에서 HD, SD 트랜스 코딩 템플릿을 설정할 수 있습니다. 트랜스 코딩 템플릿이 있는 WebRTC 스트림 주소를 Demo의 해당 열에 입력한 다음 재생을 테스트합니다(이 기능을 테스트할 필요가 없는 경우, Demo에 WebRTC 원본 스트림 하나만 입력하면 됩니다).
>- 라이브 방송 트랜스 코딩 운영 가이드 및 트랜스 코딩 과금 관련 내용은 [라이브 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/31071) 문서를 참고하십시오.


[](id:obs)
## OBS WebRTC Push 액세스
WebRTC 푸시 프로토콜은 주로 비디오 클라우드의 LEB(초저지연 라이브 스트리밍) 푸시 스트림에 사용되며, 수집된 멀티미디어 화면 혹은 비디오 파일을 WebRTC 프로토콜을 통해 라이브 방송 서버로 보내는 역할을 합니다. 다음 내용은 주로 OBS 툴을 사용하여 webRTC 프로토콜의 푸시 스트림 기능을 구현하는 방법을 소개합니다.

### 주의 사항
- OBS 버전은 26버전 또는 그 이후 버전이어야 합니다.
- WebRTC 프로토콜 푸시 스트림은 현재 OBS용 Windows 플러그 인만 있습니다. mac에서 WebRTC 푸시를 구현하려면 [Web 액세스](https://intl.cloud.tencent.com/document/product/267/42131)를 사용할 수 있습니다.

[](id:set)
### OBS 플러그 인 설정
1. **플러그 인 데이터 설정**.
	1. [OBS 플러그 인](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20220509.zip)을 다운로드하고, `services.json`, `package.json` 2개의 데이터 파일을 **data > obs-plugins > rtmp-services** 디렉터리로 이동하여 덮어씁니다. (`obs-studio`는 기본적으로 C 드라이브에 설치되며 해당 디렉터리는 `C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`입니다. 실제 상황에 맞게 설정하십시오.)
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
	2. 위의 두 JSON 파일을 사용하여 `C:\Users\<컴퓨터 이름>\AppData\Roaming\obs-studio\plugin_config\rtmp-services`에 있는 파일을 덮어씁니다. (`<컴퓨터 이름>`은 실제 상황에 따라 입력합니다.)
2. **플러그 인 동적 라이브러리 설정**.
`obs-plugins\64bit`에 있는 dll 파일을 **obs-studio** > **obs-plugins** > **64bit** 디렉터리로 이동합니다. (기본적으로 `obs-studio`는 C 드라이브에 설치되어 있으며, 해당 디렉터리는 `C:\Program Files\obs-studio\obs-plugins\64bit`입니다. 실제 상황에 맞게 설정하십시오.)<br>
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### 푸시 스트림 링크 설정
[](id:push)
1. **WebRTC 푸시 스트림 주소 생성**.
  1. Tencent Cloud 라이브 방송 콘솔 로그인 후, **라이브 방송 툴 박스** > **[주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**에서 푸시 스트림 주소를 생성합니다. 구체적인 작업은 [주소 생성기](https://intl.cloud.tencent.com/document/product/267/31084)를 참고하십시오.
  2. 생성된 `rtmp` 접두사를 `webrtc`로 수정합니다. 구체적인 사용 설명은 [라이브 방송 URL 직접 조합](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.

 ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **OBS 푸시 스트림 서비스 설정**.[](id:set_obs)
  1. OBS를 열고 하단 툴 바의 **컨트롤러** > **설정** 버튼을 눌러 설정 인터페이스로 이동합니다.
  2. **푸시 스트림**을 클릭하여 스트림 설정 탭으로 이동한 후, 서비스 유형을 'Tenent webrtc'로, 서버를 'Default'로 선택한 후, 이전에 생성한 [WebRTC 푸시 스트림 주소](#push)를 스트림 키에 입력하고, 뒤에 `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`을 스티칭합니다.
**스트림 키 예시:**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
참고 이미지:
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### LEB 풀 스트림 재생
풀 스트림 재생을 위한 LEB SDK를 통합합니다. 자세한 내용은 [LEB 풀 스트림](www.tencentcloud.com/document/product/1071/41875)을 참고하십시오.
