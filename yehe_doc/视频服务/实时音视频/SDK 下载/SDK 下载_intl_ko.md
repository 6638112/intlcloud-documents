TRTC는 Tencent Cloud LiteAV 시리즈 제품 중 하나로, LiteAV 체제의 SDK는 모두 동일한 기본 모듈을 사용하기 때문에 프로젝트 중 동시에 두 개 이상의 LiteAV 체제의 SDK를 통합하게 되면 부호 충돌(symbol duplicate) 문제가 발생할 수 있습니다. 따라서 Tencent Cloud에서는 다양한 제품 기능을 통합한 **라이트 버전(TRTC)**, 프로 버전(Professional)**과 **엔터프라이즈 버전(Enterprise)**을 제공하여 사용자가 실제 비즈니스에 적합한 버전을 선택할 수 있습니다.

라이트 버전은 TRTC와 라이브 방송 재생(TXLivePlayer) 기능만 제공하며 App 설치 패키지 용량 증분이 가장 적어 TRTC 관련 기능만 사용하는 사용자에게 적합합니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증량</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_trtc") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_trtc") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar: 546K<br> so(armeabi): 4.5M<br> so(armv7): 4.5M<br>so(arm64): 5.3M</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C++)  </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_cplusplus_trtc") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">12.7M（C++ x86）<br>15.6M（C++ x64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C#) </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_csharp_trtc") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">13.8M（C# x64）<br>13.3M（C# x86）</td>
   </tr>
     <tr>
      <td style="text-align:center">Mac</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_mac_trtc") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35094">DOC</a></td>
      <td style="text-align:center">2.05M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">데스크톱 브라우저</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_web_trtc") href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35607">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35096">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
   <tr>
      <td style="text-align:center">Electron  </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_electron_trtc") href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35089">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35097">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
   <tr>
      <td style="text-align:center">WeChat 미니프로그램</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_wxmini_trtc") href="https://web.sdk.qcloud.com/trtc/miniapp/download/trtc-room.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://cloud.tencent.com/document/product/647/32399">DOC</a></td>
      <td style="text-align:center"><a href="https://cloud.tencent.com/document/product/647/32183">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
	    <tr>
      <td style="text-align:center">Flutter</td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a href="https://github.com/c1avie/trtc_demo">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/39243">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35098">DOC</a></td>
      <td style="text-align:center">13M</td>
   </tr>
<tr>
      <td style="text-align:center">Unity</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_unity_trtc") href="https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/TRTCUnitySDK.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/c1avie/TRTCUnity ">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a href="https://cloud.tencent.com/document/product/647/55153">DOC</a></td>
      <td style="text-align:center"><a href="https://cloud.tencent.com/document/product/647/55834">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
</table>

>? 
> - SDK가 가져오는 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참조하십시오.

<h2 id="Professional">프로 버전(Professional)</h2>

프로 버전은 [Player+](https://intl.cloud.tencent.com/), [MLVB]와 [UGSV] 등 TRTC를 포함한 다양한 멀티미디어 관련 핵심 기능이 통합되어 있습니다. 하위 레이어 모듈을 효율적으로 재사용하여 통합 프로 버전의 증분 용량이 독립적인 SDK 2개를 통합한 용량보다 작으며, 부호 충돌(symbol duplicate) 문제도 방지할 수 있습니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">64비트 지원</td>      
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증량</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_iOS">Github</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3.2M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_Android">Github</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar: 1M<br> so(armeabi): 5.7M<br> so(armv7): 5.7M<br>so(arm64): 6.8M</td>
   </tr>
</table>

>? 
>- Windows와 Mac 버전의 SDK는 현재 하나의 버전밖에 없으며, 라이트 버전, 프로 버전 및 엔터프라이즈 버전의 구분이 없습니다.
>- LiteAV 체제의 SDK는 모두 동일한 기초 모듈을 사용하기 때문에 프로젝트 중 동시에 두 개 이상의 LiteAV 체제의 SDK를 통합하게 되면 부호 충돌(symbol duplicate) 문제가 발생할 수 있습니다. 해결 방법은 프로 버전의 LiteAVSDK로 통합하는 것입니다.
>- SDK가 가져오는 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참조하십시오.


<h2 id="Enterprise">엔터프라이즈 버전(Enterprise)</h2>

엔터프라이즈 버전은 프로 버전의 모든 기능을 포함할 뿐 아니라 AI 뷰티 필터 특수 효과 컴포넌트가 포함되어 큰 눈, 갸름한 얼굴, 메이크업, 움직이는 스티커, 액세서리 등 AI 뷰티 필터 특수 효과 기능을 지원합니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">소속 플랫폼</td>
      <th width="0px" style="text-align:center">ZIP 패키지</td>
      <th width="0px" style="text-align:center">64비트 지원</td>
      <th width="0px" style="text-align:center">Demo 실행 설명</td>
      <th width="0px" style="text-align:center">SDK 통합 가이드</td>
      <th width="0px" style="text-align:center">설치 패키지 증량</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_enterprise") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center"> 5.5M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_enterprise") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">지원</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center"> jar: 2.2M<br>so(armeabi): 9.3M</td>
   </tr>
</table>

>?
>- Windows와 Mac 버전의 SDK는 현재 AI 뷰티 필터 특수 효과 컴포넌트가 없으며, 라이트 버전, 프로 버전 및 엔터프라이즈 버전의 구분이 없습니다.
>- SDK가 가져오는 설치 패키지 용량 증분을 줄여야 할 경우, [설치 패키지 용량 축소 방법](https://intl.cloud.tencent.com/document/product/647/35165)을 참조하십시오.


## 각 버전 차이 대조표

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">기능 모듈</th>
    <th width="100px" style="text-align:center">기능 항목</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1071/38150">라이브 방송 라이트 버전</a><br>LiteAV_Smart</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">UGSV 버전</a><br>LiteAV_UGC</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">TRTC 버전</a><br>LiteAV_TRTC</th>
    <th width="100px" style="text-align:center"><a href="https://cloud.tencent.com/document/product/881/20205">플레이어 버전</a><br>LiteAV_Player</th>
    <th width="100px" style="text-align:center"><a href="#Professional">프로 버전</a><br>Professional</th>
    <th width="100px" style="text-align:center"><a href="#Enterprise">엔터프라이즈 버전</a><br>Enterprise</th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 푸시 스트림</td>
    <td style="text-align:center">카메라 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">녹화 푸시 스트림</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">라이브 방송 재생</td>
    <td style="text-align:center">RTMP 프로토콜</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
     <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD 재생</td>
    <td style="text-align:center">MP4 포맷</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM 암호화</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">뷰티 필터</td>
    <td style="text-align:center">기초 뷰티 필터</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">기초 필터</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">라이브 방송 마이크 연결</td>
    <td style="text-align:center">마이크 연결 인터랙션</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">크로스 룸 PK</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">영상 통화</td>
    <td style="text-align:center">2인 통화</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">화상 회의</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">녹화 및 촬영</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">편집</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">'틱톡' 특수 효과</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">비디오 업로드</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">AI 뷰티 필터 특수 효과</td>
    <td style="text-align:center">큰 눈 & 갸름한 얼굴</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">V라인 & 오똑한 코</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">움직이는 스티커</td>
   <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">그린 스크린 크로마 키</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
</table>


<script>
  var _mtac = {"senseHash":0};
  (function() {
    var mta = document.createElement("script");
    mta.src = "//pingjs.qq.com/h5/stats.js?v2.0.4";
    mta.setAttribute("name", "MTAH5");
    mta.setAttribute("sid", "500695331");
    mta.setAttribute("cid", "500695332");
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(mta, s);
  })();
</script>


