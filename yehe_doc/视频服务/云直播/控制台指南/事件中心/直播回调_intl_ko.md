CSS는 라이브 방송 콜백 기능 및 콘솔을 통한 콜백 템플릿 구성을 지원하며, 각 트리거 이벤트에 대해 관련 콜백 정보를 수신할 경로를 설정합니다. 또한 템플릿을 푸시 도메인에 연결합니다. 연결이 완료된 후, 설정된 템플릿의 이벤트 트리거 콜백 기능을 통해 라이브 방송 중 Tencent Cloud가 자동으로 클라이언트 서버에 요청을 보내며, 클라이언트 서버는 요청에 응답합니다. 인증을 통과하면 이벤트에 해당하는 경로를 통해 콜백 정보의 JSON 데이터 패킷을 획득하게 됩니다.
본 문서는 콘솔을 통해 콜백 설정 템플릿의 생성, 수정 및 삭제하는 방법에 대해 소개합니다. 

** 그 중, 콜백 설정 템플릿을 생성하는 방법으로는 다음과 같이 두 가지 방식이 있습니다. **
- CSS 콘솔을 통해 템플릿을 생성하는 자세한 방법은 [콜백 템플릿 생성](#Callback)을 참조하십시오.
- API를 통한 템플릿 생성과 관련된 자세한 매개변수 및 사례는 [콜백 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30815)을 참조하십시오.


## 주의사항

- 생성 완료 후, 해당 푸시 도메인에서 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31065)을 연결해야 하며, 연결 완료 후 약 5~10분 뒤에 적용됩니다.
- 콜백 설정 중, 콜백 이벤트 수신에 사용되는 콜백 주소 `http` 또는 `https` 서버가 정상적으로 응답을 수신할 수 있어야 합니다.
- 콘솔의 콜백 템플릿은 도메인 차원에서 관리되며, 연결 인터페이스에서 생성된 규칙은 일시적으로 취소할 수 없습니다. 만약 라이브 방송 콜백 관련 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [콜백 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30814)를 참조하여 연결을 해제해야 합니다.
- 라이브 방송 콜백 관련 프로토콜에 대한 정보는 [이벤트 정보 알림 프로토콜](https://intl.cloud.tencent.com/document/product/267/38080)을 참조하십시오.
- 라이브 방송 콜백 메시지 알림 매개변수에 대한 자세한 설명은 다음을 참조하십시오.
 - [푸시 스트리밍 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38081)
 - [스트리밍 중단 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38081)
 - [녹화 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38082)
 - [화면 캡처 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38083)
 - [음란물 감지 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38084)




<span id="Callback"></span>
## 콜백 템플릿 생성

1. [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인합니다.
2. 왼쪽 메뉴에서 [이벤트 센터]>[[라이브 방송 콜백]](https://console.cloud.tencent.com/live/config/callback)을 선택합니다.
3. [콜백 템플릿 생성]을 클릭하여 콜백 설정 팝업창에 콜백 정보를 입력한 뒤 [저장]을 클릭합니다.
![](https://main.qcloudimg.com/raw/bfd1e566f7cbd70419d1dfe66d40cc24.png)
<table>
<thead><tr><th width="17%">설정 항목</th><th>설명</th></tr></thead><tbody><tr>
<td>템플릿 이름</td>
<td>콜백 템플릿 이름은 중국어, 영어, 숫자, _, - 만 지원하며, 30자를 초과할 수 없습니다. </td>
</tr><tr>
<td>템플릿 설명</td>
<td>콜백 템플릿 설명 정보 입력은 중국어, 영어, 숫자, _, -만 지원하며 100자를 초과할 수 없습니다.</td>
</tr><tr>
<td>콜백 보안키</td>
<td>사용자 정의 보안키 <br>알파벳 대소문자와 숫자로 구성되며 최대 32자까지 입력할 수 있습니다. 관련 사용 방법은 <a href="https://intl.cloud.tencent.com/document/product/267/38081#.E5.9B.9E.E8.B0.83.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0">이벤트 정보 알림 공용 매개변수</a>를 참조하십시오. </td>
</tr><tr>
<td>푸시 스트리밍 콜백</td>
<td>푸시 스트리밍 콜백 이벤트를 수신할 수 있는 경로를 입력하십시오. http, https 등의 프로토콜 헤드를 지원합니다. </td>
</tr><tr>
<td>스트리밍 중단 콜백</td>
<td>스트리밍 중단 콜백 이벤트를 수신할 수 있는 경로를 입력하십시오. http, https 등의 프로토콜 헤드를 지원합니다. </td>
</tr><tr>
<td>녹화 콜백</td>
<td>녹화 콜백 이벤트를 수신할 수 있는 경로를 입력하십시오. http, https 등의 프로토콜 헤드를 지원합니다. </td>
</tr><tr>
<td>화면 캡처 콜백</td>
<td>화면 캡처 콜백 이벤트를 수신할 수 있는 경로를 입력하십시오. http, https 등의 프로토콜 헤드를 지원합니다. </td>
</tr><tr>
<td>화면 캡처 및 음란물 감지 콜백</td>
<td>화면 캡처 및 음란물 감지 콜백 이벤트를 수신할 수 있는 경로를 입력하십시오. http, https 등의 프로토콜 헤드를 지원합니다. </td>
</tr>
</tbody></table>


<span id="change"></span>
## 템플릿 수정

1. [이벤트 센터]>[[라이브 방송 콜백]](https://console.cloud.tencent.com/live/config/callback) 페이지로 이동합니다.
2. 생성된 콜백 설정 템플릿을 선택하고 오른쪽에 있는 [편집]을 클릭하면 템플릿 정보 수정 페이지로 이동합니다.
3. [저장]을 클릭합니다.

![](https://main.qcloudimg.com/raw/cf99965236bdaa56a96998e3a83e1e60.png)

<span id="delete"></span>

## 템플릿 삭제

템플릿이 연결되어 있는 경우, 바인딩 해제 후 삭제 가능합니다. 자세한 바인딩 해제 작업 방식은 [바인딩 해제 콜백 설정](https://intl.cloud.tencent.com/document/product/267/31065#untie)을 참조하십시오.

1. [이벤트 센터]>[[라이브 방송 콜백]](https://console.cloud.tencent.com/live/config/callback) 페이지로 이동합니다.
2. 생성된 콜백 설정 템플릿을 선택하고 오른쪽의 [삭제] 버튼을 클릭합니다.
3. 현재 화면 캡처 및 음란물 감지 설정 템플릿의 삭제 여부를 확인하고 [확인]을 클릭하면 삭제가 완료됩니다.

![](https://main.qcloudimg.com/raw/6e1b311ecfb7107ded005745291be1e5.png)

