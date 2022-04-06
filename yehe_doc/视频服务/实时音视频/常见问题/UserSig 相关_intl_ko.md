[](id:UserSig)
## UserSig는 무엇입니까?

UserSig란 Tencent Cloud가 설계한 일종의 보안 서명으로, 악성 해커가 귀하의 클라우드 서비스 사용권을 도용하는 것을 방지합니다.
현재 Tencent Cloud의 TRTC, IM, MLVB 등의 서비스는 모두 이 보안 메커니즘을 사용하고 있으며, 이러한 서비스를 사용하려면 해당 SDK의 초기화 또는 로그인 함수에 SDKAppID, UserID, UserSig의 주요 정보를 제공해야 합니다.
이 중, SDKAppID는 귀하의 애플리케이션 식별에 사용되고, UserID는 귀사의 사용자 식별에 사용됩니다. UserSig는 이 둘을 기반으로 보안 서명을 계산합니다. UserSig는 **HMAC SHA256** 암호화 알고리즘으로 계산됩니다. 해커가 UserSig를 위조하지 못하는 이상 귀하의 클라우드 서비스 트래픽을 도용할 수 없습니다.
UserSig의 계산 원리는 다음 이미지와 같으며, 그 본질은 SDKAppID, UserID, ExpireTime 등 주요 정보에 대해 해시 암호화를 1회 진행하는 것입니다.
```Cpp
//UserSig 계산 공식, 여기서 secretkey는 usersig 계산용 암호화 키

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
>?
>- 'currtime'은 현재 시스템 시간이고 'expire'는 서명 만료 시간입니다.
>- 상기 개략도는 UserSig의 계산 원리를 설명하기 위한 것으로, UserSig 스플라이싱 코드의 구체적인 구현은 [클라이언트 계산 UserSig](#Client) 및 [서버 계산 UserSig](#Server)를 참고하십시오.

[](id:Key)
## 디버깅 및 실행 단계에서 UserSig를 계산하는 방법은 무엇입니까?
현재 Demo를 빠르게 실행하고 TRTC SDK의 기능에 대해 배우고 싶다면 [클라이언트 샘플 코드](#client) 및 [콘솔](#console) 메소드를 통해 UserSig를 계산하고 얻을 수 있습니다. 다음을 참고하십시오.

>!
>- UserSig를 얻기 위한 위의 두 가지 계산 방식은 디버깅에만 적용할 수 있습니다. 제품 런칭에는 이 방법을 **권장하지 않습니다**. 클라이언트 코드(특히 Web)의 SECRETKEY는 디컴파일로 크래킹되기 쉽습니다. 키가 유출되면 해커는 Tencent Cloud 트래픽을 도용할 수 있습니다.
>- 올바른 방법은 프로젝트 서버에 UserSig 계산 코드를 배포하여 App이 필요할 때마다 실시간 계산된 UserSig를 서버에서 요청할 수 있도록 하는 것입니다. 

[](id:client)
### UserSig를 계산하기 위한 클라이언트 샘플 코드
1. **SDKAPPID 및 키 가져오기**:
    1. **TRTC 콘솔** > **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**에 로그인합니다.
    2. 조회하고자 하는 SDKAppID에 해당하는 **애플리케이션 정보**를 클릭한 후 다시 **퀵 스타트** 탭을 클릭하여 이동합니다.
    3. **2단계: UserSig 발급 키 획득** 탭을 조회하면 UserSig 계산에 사용하는 암호화 키를 획득할 수 있습니다.
    4. **키 복사**를 클릭하면 키를 클립보드에 복사할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/b8575d1c97952ad8b1b28df16d69a8cb.png)

>? 키 조회 시 공개키와 개인키 정보만 얻을 수 있다면 [키 획득 방법](#getusersig)을 참고하십시오.
2. **UserSig 계산:**
클라이언트 사용을 용이하게 하기 위해 각 플랫폼에서 UserSig를 계산하기 위한 소스 파일을 제공합니다. 계산을 직접 다운로드할 수 있습니다.
<table>
<thead><tr><th>적용 플랫폼</th><th>파일 소스 코드</th><th>파일 상대 경로</th></tr></thead>
<tbody><tr>
<td>iOS</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h">Github</a></td>
<td>TRTC-API-Example-OC/Debug/GenerateTestUserSig.h</td>
</tr><tr>
<td>Mac</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Mac/tree/main/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h">Github</a></td>
<td>OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
</tr><tr>
<td>Android</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java">Github</a></td>
<td>TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java</td>
</tr><tr>
<td>Windows（C++）</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C%2B%2B/TRTC-API-Example-Qt/src/Util/defs.h">Github</a></td>
<td>TRTC-API-Example-C++/TRTC-API-Example-Qt/src/Util/defs.h</td>
</tr><tr>
<td>Windows（C#）</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-CSharp/TRTC-API-Example-CSharp/GenerateTestUserSig.cs">Github</a></td>
<td>TRTC-API-Example-CSharp/TRTC-API-Example-CSharp/GenerateTestUserSig.cs</td>
</tr><tr>
<td>Web</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/debug/GenerateTestUserSig.js">Github</a></td>
<td>base-js/js/debug/GenerateTestUserSig.js</td>
</tr><tr>
<td>Flutter</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Flutter/blob/master/TRTC-API-Example/lib/Debug/GenerateTestUserSig.dart">Github</a></td>
<td>TRTC-API-Example/lib/Debug/GenerateTestUserSig.dart</td>
</tr>
</tbody></table>

TRTC SDK의 예시 코드에 `GenerateTestUserSig`라는 오픈 소스 모듈을 제공하였습니다. 이 중 SDKAPPID, EXPIRETIME 및 SECRETKEY 등 3가지 멤버 변수를 자체 설정으로 변경하면 `genTestUserSig()` 함수를 호출하여 계산된 UserSig를 획득해 SDK 관련 기능을 빠르게 실행할 수 있습니다.
![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)

[](id:getusersig)
#### 키 조회 시 공개키와 개인키 정보만 획득할 수 있습니다. 키는 어떻게 획득합니까?
TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있으며, 이미 업데이트한 경우 필요에 따라 기존/신규 알고리즘을 전환하십시오.

**업데이트/전환 작업:**
1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. 왼쪽 사이드바에서 **애플리케이션 관리**를 선택한 후 대상 애플리케이션이 속한 행의 **애플리케이션 정보**를 클릭합니다.
3. **퀵 스타트** 탭을 선택하고 **2단계: UserSig 발급 키 획득**에서 **업데이트**, **비대칭 암호화** 또는 **HMAC-SHA256**을 클릭합니다.
  - 업데이트
  - 기존 버전 알고리즘 ECDSA-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/73ff89d39c00a0925621928de4aa03bf.png)
  - 신규 버전 알고리즘 HMAC-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/98261eaa1fc6d9e4a6796f277a9dcb09.png)


[](id:console)
### 콘솔에서 UserSig 가져오기
1. **TRTC 콘솔**에 로그인하여 **개발 지원** > **[UserSig 생성&검증](https://console.cloud.tencent.com/trtc/usersigtool)**으로 이동합니다.
2. 서명(UserSig) 생성 툴에서 해당 SDKAppID 및 UserID를 선택합니다.
3. **서명 생성(UserSig)**을 클릭하여 해당 UserSig를 계산합니다.


[](id:formal)
## 정식 실행 단계에서 UserSig는 어떻게 계산하나요?

비즈니스의 공식 운영 단계에서 TRTC는 UserSig에 대한 상위 수준의 서버측 계산 솔루션을 제공하여 UserSig 계산용 키가 유출되는 것을 최대한 막을 수 있습니다. 이는 서버를 뚫는 것이 App을 리버스하는 것보다 어렵기 때문입니다. 구체적인 구현 프로세스는 다음과 같습니다.

1. App에서 SDK의 초기화 함수를 호출하기 전에 먼저 서버에 UserSig를 요청합니다.
2. 서버에서 SDKAppID와 UserID에 따라 UserSig를 계산합니다. 계산 소스 코드는 파일 전반부를 참고하십시오.
3. 서버에서 계산된 UserSig를 App에 리턴합니다.
4. App에서 획득한 UserSig를 특정 API를 통해 SDK에 전송합니다.
5. SDK는 `SDKAppID + UserID + UserSig`를 Tencent Cloud 서버에 보내 인증을 진행합니다.
6. Tencent Cloud는 UserSig에 대한 인증을 진행하여 합법 여부를 판단합니다.
7. 인증 통과 후 TRTCSDK에 TRTC 서비스를 제공합니다.

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

과정을 간소화하기 위해 다국어 버전의 UserSig 계산 소스 코드(현재 버전 서명 알고리즘)를 제공합니다.

| 언어 버전 | 서명 알고리즘 | 핵심 함수 | 다운로드 링크 |
| -------- | ----------- | ----------- | ----------- |
| Java     | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [Github](https://github.com/tencentyun/tls-sig-api-v2-java)  |
| GO       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang) |
| PHP      | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-php)  |
| Node.js  | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [Github](https://github.com/tencentyun/tls-sig-api-v2-node)  |
| Python   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
| C#       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### 이전 버전 서명 알고리즘 UserSig 계산 소스 코드
서명 계산 난이도를 낮추고 고객이 더욱 빠르게 Tencent Cloud 서비스를 이용할 수 있도록 하기 위해, TRTC는 2019-07-19부터 새로운 서명 알고리즘을 적용하여, ECDSA-SHA256을 HMAC-SHA256으로 업그레이드 하였습니다. 2019-07-19 이후 생성된 SDKAppID는 새로운 HMAC-SHA256 알고리즘이 적용됩니다.

SDKAppID가 2019-07-19 이전에 생성된 경우 기존 버전의 서명 알고리즘을 계속 사용할 수 있습니다. 알고리즘 소스 코드의 다운로드 링크는 다음과 같습니다.

| 언어 버전 |   서명 알고리즘   |                          다운로드 링크                          |
| :------: | :----------: | :--------------------------------------------------------: |
|   Java   | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-java)  |
|   C++    | ECDSA-SHA256 |    [Github](https://github.com/tencentyun/tls-sig-api)     |
|    GO    | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-golang) |
|   PHP    | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-php)   |
|  Node.js  | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-node)  |
|    C#    | ECDSA-SHA256 |   [Github](https://github.com/tencentyun/tls-sig-api-cs)   |
|  Python  | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-python) |
