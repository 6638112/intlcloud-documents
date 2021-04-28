본 문서에서는 브라우저에서 영상 통화를 실행하는 솔루션을 소개하며, 다음과 같이 두 부분으로 나뉘어 있습니다.
- 1. 서비스 활성화 및 Tencent Cloud에서 제공하는 Demo 실행 방법 소개
- 2. TRTCCalling 모듈을 사용한 영상 통화 기능의 빠른 구축 방법 소개

## 환경 요건
최신 버전의 Chrome 브라우저를 사용하십시오. 현재 데스크톱 Chrome 브라우저가 TRTC 데스크톱 브라우저 SDK를 비교적 완벽하게 지원하므로, Chrome 브라우저를 사용한 체험을 권장합니다.

TRTCCalling은 다음 포트에 종속되어 데이터를 전송합니다. 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [공식 홈페이지 Demo]에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
  - TCP 포트: 8687
  - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
  - 도메인: qcloud.rtc.qq.com

현재 해당 솔루션에서 지원하는 플랫폼은 다음과 같습니다.

| 운영 체제 |          브라우저 유형          | 브라우저 최저 버전 요구사항 |
| :------: | :--------------------------: | :----------------: |
|  Mac OS  |     데스크톱 Safari 브라우저     |        11+         |
|  Mac OS  |     데스크톱 Chrome 브라우저     |        56+         |
|  Mac OS  |    데스크톱 Firefox 브라우저     |        56+         |
|  Mac OS  |      데스크톱 Edge 브라우저       |        80+         |
| Windows  |     데스크톱 Chrome 브라우저     |        56+         |
| Windows  | 데스크톱 QQ 브라우저(고속 커널) |       10.4+        |
| Windows  |    데스크톱 Firefox 브라우저     |        56+         |
| Windows  |      데스크톱 Edge 브라우저      |        80+         |

## 테스트 Demo 실행


[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 및 실명 인증이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국대륙 실시간 영상 통화 인스턴스를 구매할 수 없습니다.
2. TRTC 콘솔에 로그인한 후 [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
3. 애플리케이션 이름(예: TestTRTC)을 입력한 후 [생성]을 클릭합니다.


[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:step3)
### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Web/TRTCScenesDemo/trtc-calling-web/public/debug/GenerateTestUserSig.js` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 지향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

[](id:step4)
### 4단계: Demo 실행
1. npm 명령 프롬프트에 다음 명령어를 순서대로 입력합니다.
```
npm install
npm run serve
```
2. Chrome 브라우저에서 `http://localhost:8080/` 링크를 실행합니다. 모두 정상일 경우 Demo 실행 인터페이스는 다음과 같습니다.
3. 사용자 userid를 입력하고 [로그인]을 클릭한 후 [영상 통화]를 선택합니다.
4. 통화할 사용자의 userid를 입력하고 [통화]를 클릭합니다.
5. 영상 통화가 가능합니다.


## 영상 통화 구축
### 1단계: TRTCCalling 모듈 통합

>?
>- v0.6.0부터 종속 [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk), [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk), [tsignaling](https://www.npmjs.com/package/tsignaling)을 수동으로 설치해야 합니다.
>- 액세스 측에서 기존에 사용하고 있는 trtc-js-sdk, tim-js-sdk, tsignaling 버전과의 충돌 방지를 위해 trtc-calling-js.js 용량이 축소되었습니다. 따라서 trtc-calling-js.js에 trtc-js-sdk, tim-js-sdk, tsignaling이 포함되어 있지 않으며, 사용 전 해당 종속을 수동으로 설치해야 합니다.

```
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save



  //script 방식으로 trtc-calling-js를 사용하는 경우 순서에 따라 먼저 수동으로 trtc.js를 가져와야 합니다.
  <script src="./trtc.js"></script>

  // tim-js.js를 수동으로 가져옵니다.
  <script src="./tim-js.js"></script>

  // tsignaling.js를 수동으로 가져옵니다.
  <script src="./tsignaling.js"></script>



  // trtc-calling-js.js를 수동으로 가져옵니다.
  <script src="./trtc-calling-js.js"></script>
```

### 2단계: TRTCCalling 객체 생성
TRTCCalling 객체를 생성하고 SDKAppID 매개변수를 사용자의 SDKAppID로 설정합니다.
```
import TRTCCalling from 'trtc-calling-js';

let options = {
  SDKAppID: 0 // 액세스 시 0을 사용자의 SDKAppID로 대체해야 합니다.
};
const trtcCalling = new TRTCCalling(options);
```

### 3단계: 로그인 완료
login 함수를 호출하여 로그인 작업을 완료합니다. 매개변수에서 userID는 사용자 이름이고, userSig는 사용자 서명입니다. userSig의 계산 방식은 [userSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

```javascript
trtcCalling.login({
  userID,
  userSig,
});
```

### 4단계: 1대1 통화
#### 발신자: 특정 사용자에게 호출
```javascript
trtcCalling.call({
  userID,  //사용자 ID
  type: 2, //통화 유형, 0-알 수 없음, 1-음성 통화, 2-영상 통화
  timeout  //초대 타임아웃 시간, 단위 s(초)
});
```

#### 수신자: 신규 호출 수신
```javascript
// 수신
trtcCalling.accept({
  inviteID, //초대 ID, 초대 1회 식별
  roomID,   //통화방 번호 ID
  callType  //0-알 수 없음, 1-음성 통화, 2-영상 통화
});
// 거부
trtcCalling.reject({ 
  inviteID, //초대 ID, 초대 1회 식별
  isBusy //통화 중 여부, 0-알 수 없음, 1-음성 통화, 2-영상 통화
  })
```

#### 로컬 카메라 켜기
```javascript
trtcCalling.openCamera()
```

#### 원격 영상 통화 화면 표시
```javascript
trtcCalling.startRemoteView({
  userID, //원격 사용자 ID
  videoViewDomID //사용자 데이터는 해당 DOM ID 노드에 렌더링됩니다.
})
```

#### 로컬 미리보기 화면 표시
```javascript
trtcCalling.startLocalView({
  userID, //로컬 사용자 ID
  videoViewDomID //사용자 데이터는 해당 DOM ID 노드에 렌더링됩니다.
})
```

#### 통화 종료
```javascript
trtcCalling.hangup()
```
