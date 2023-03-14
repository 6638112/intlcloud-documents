## 기능 소개
커뮤니티 모드(엔터테인먼트 협업을 위한 새로운 도구)는 **커뮤니티**-**그룹**-**토픽** 3단계 구조를 지원하고, 메시지를 서로 분리할 수 있으며, 초대형 규모의 참석자를 운영하고, 친구 관계를 공유하며, 또한 참석자를 그룹화하고, 참석자 그룹 보기, 말하기 및 관리 등 권한을 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/012568d737c68249ce61b4ba51f7654a.png)
![](https://qcloudimg.tencent-cloud.cn/raw/b3912b1a206d87c93dc3191d1dd71472.png)

## 적용 시나리오
### 친구 사귀기: 새로운 사용자 증가 모델
- 초대형 동호회 모임을 지원하며 **커뮤니티**-**그룹**-**토픽**을 통해 관심사를 수직적으로 세분화 할 수 있습니다.
- 대규모 공개 커뮤니티에서는 사용자에게 폐쇄적인 작은 토픽을 제공하고, 이러한 편안한 중간 지대는 사용자가 원하는 토픽을 선택해 커뮤니케이션할 수 있어, 참석자의 적극적인 참여를 유도합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/12597e5e5d98fdfa03fa2d719a9bc67c.png)

### 게임 기반 소셜 네트워크: 더 높은 사용자 충성도 및 참여도
다양한 커뮤니티 토픽을 통해 유저는 뉴스에 액세스하고, 팀원을 찾고, 플롯에 대해 토론하고, 팁을 공유할 수 있습니다. 게임을 시작하기 전에 사용자는 조언을 검색할 수 있습니다. 게임 중에 항상 다른 사람과 대화할 수 있으며(채팅방은 항상 온라인 상태), 게임이 끝난 후에도 토픽에 대한 깊이 있는 커뮤니케이션을 계속할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f9a7348eb58a713cc8bfea86b4d1c40a.png)

### 팬 운영: 효율적인 운영 툴 보유
각각의 독립된 그룹(‘선전 사용자 1그룹’ ‘선전 사용자 2그룹’ ‘광저우 사용자 1그룹’ ‘상하이 사용자 1그룹’ 등 여러 그룹 대체)을 운영할 필요 없이 하나의 커뮤니티에서 다양한 토픽을 다룰 수 있기 때문에 더 이상 여러 그룹을 동시에 관리해야 하는 걱정을 할 필요가 없어 팬 운영이 더 쉽고 정확해집니다!
![](https://qcloudimg.tencent-cloud.cn/raw/28b511e5fda1c991f10dec89632236cb.png)

### 조직 관리: 명확한 레이어 커뮤니케이션 구현
조직의 모든 구성원은 동일한 커뮤니티에 가입할 수 있습니다. 커뮤니티 계층 및 권한 설정을 통해 계층적 커뮤니케이션을 구현합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fc983d18421ed11164475d62eb015344.png)

## 기술 경쟁력
### 초대형 규모의 커뮤니티 구성원
Tencent IM 커뮤니티는 용량이 1만 배 가까이 확장되어, 취미 친구 사귀기, 팬 마케팅, 게임 기반 소셜 네트워킹 및 조직 관리와 같은 사용 사례에서 대규모 회원을 수용해야 하는 요구 사항을 완벽하게 충족합니다.
### 메시지 신뢰성
Tencent IM 커뮤니티는 구성원 용량을 대폭 확대하면서 Tencent의 강력한 메시징 능력을 이어받아 20여 년의 기술 축적을 바탕으로 구축한 완벽하고 신뢰할 수 있는 메시징 시스템입니다. 99.99% 이상의 메시지 송수신 성공률 및 서비스 신뢰성을 고객에게 제공하여 고객이 수억 대의 대규모 동시성에 쉽게 대처할 수 있도록 지원합니다.
### 메시지 푸시 성능
Tencent IM 커뮤니티는 ‘빠르고 느린 채널’ + ‘2단계 결합 푸시’의 새로운 메시지 푸시 아키텍처를 채택하여 시간과 공간의 균형을 효과적으로 유지하고, 시스템 푸시 성능을 향상시키며, 단말 성능 소모를 줄이고, 초대형 그룹의 사용자에게도 일반 그룹과 동일한 메시지 인터랙션 경험을 제공할 수 있습니다.

### 메시지 상태 및 사용자 권한 관리
Tencent IM 커뮤니티는 메시지 편집, 회수, 포워딩 등 풍부한 확장 기능을 제공합니다. 음소거, 메시지 방해 금지, 읽지 않음 메시지 수, 프로필 편집 등은 사용자가 전역, 커뮤니티, 토픽 수준을 각각 사용자 정의할 수 있도록 지원합니다.

## 네이티브 SDK 통합 가이드
>!커뮤니티(Community) 토픽(Topic) 기능은 v6.2.2363 이상의 IM 네이티브 SDK 인핸스드 버전 이상에서만 지원됩니다. 이를 사용하려면 [플래그십 버전 구매](https://buy.cloud.tencent.com/avc?from=17182) 및 [구성 변경 요청 티켓](https://www.tencentcloud.com/document/product/1047/44322)의 지침에 따라 활성화를 신청하십시오.

다음은 Android를 예시로 커뮤니티 토픽의 인터페이스 기능을 소개합니다.

### Demo를 다운로드하여 커뮤니티 기능을 빠르게 체험
Android 휴대폰으로 아래 QR코드를 스캔하여 Demo를 다운로드 후 바로 체험할 수 있습니다.
다음은 API 호출의 관점에서 커뮤니티 토픽의 사용을 소개합니다.
<img style="width:518px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/386bd090f3b1e5a904d5eced5b94e758.png" />


### 커뮤니티 토픽의 API 사용
1. 먼저 createGroup 인터페이스를 호출하여 토픽을 지원하는 커뮤니티를 생성하고, [커뮤니티 관리](https://cloud.tencent.com/document/product/269/44494#.E7.A4.BE.E7.BE.A4.E7.AE.A1.E7.90.86) ‘커뮤니티 생성’ 단계를 참고하여 구현할 수 있습니다.
2. 그 다음 getJoinedCommunityList 인터페이스를 호출하여 이러한 유형의 생성 및 가입 커뮤니티 목록을 가져올 수 있습니다.
>!커뮤니티는 그룹 구성원을 관리하는 데 사용되지만 커뮤니티에서 메시지를 주고받을 수는 없습니다. 커뮤니티의 다른 기능에 대해서는 ‘기타 관리 인터페이스’ 목록을 참고하십시오.
>
3. 커뮤니티가 성공적으로 생성되면 커뮤니티에서 createTopicInfoCommunity를 호출하여 여러 개의 토픽을 생성할 수 있습니다. [Topic Management](https://cloud.tencent.com/document/product/269/44494#.E8.AF.9D.E9.A2.98.E7.AE.A1.E7.90.86)의 ‘Creating a topic’ 단계를 참고하십시오.
4. 토픽 관리에는 ‘토픽 삭제’, ‘토픽 정보 수정’, ‘토픽 목록 가져오기’ 및 ‘토픽 콜백 수신’ 기능도 포함됩니다. 동시에 토픽은 사용자가 메시지를 주고받을 수 있는 커뮤니케이션의 장이며, 관련 인터페이스는 [토픽 메시지](https://cloud.tencent.com/document/product/269/44494#.E8.AF.9D.E9.A2.98.E6.B6.88.E6.81.AF) 소개를 참고하십시오.
5. 그룹 커뮤니티 구성원: 그룹 구성원 사용자 정의 필드에 그룹 정보를 지정하여 그룹의 커뮤니티 구성원을 표시할 수 있습니다. 이 효과를 구현하려면 모든 커뮤니티 구성원을 로컬로 끌어와 그룹별로 정렬해야 합니다. 그룹 구성원 수가 많은 경우 서버측에서 구성원 그룹화를 구현하는 것이 좋습니다.

## Web  SDK 통합 가이드
>!커뮤니티(Community) 토픽(Topic) 기능은 v2.19.1 이상의 IM Web SDK에서만 지원됩니다. 사용하려면 [플래그십 에디션을 구매](https://buy.cloud.tencent.com/avc?from=17182)하고 [**콘솔**](https://console.cloud.tencent.com/im/qun-setting)>**그룹 기능 구성**>**커뮤니티** 기능을 활성화하십시오.
>
커뮤니티 토픽의 인터페이스 기능은 다음과 같습니다.
### 빠른 체험을 위한 Demo 소스 코드 다운로드 및 설정
[시작하기](https://www.tencentcloud.com/document/product/1047/45912)를 참고하여 IM 기능을 빠르게 경험할 수 있습니다.
다음은 API 호출의 관점에서 커뮤니티 토픽의 사용을 소개합니다.

### 커뮤니티 토픽의 API 사용
1. 먼저 createGroup 인터페이스를 호출하여 토픽을 지원하는 커뮤니티를 생성하고, [커뮤니티 관리](https://www.tencentcloud.com/document/product/1047/48172#.E7.A4.BE.E7.BE.A4.E7.AE.A1.E7.90.86) ‘커뮤니티 생성’ 단계를 참고하여 구현할 수 있습니다.
2. 그 다음 getJoinedCommunityList 인터페이스를 호출하여 이러한 유형의 생성 및 가입 커뮤니티 목록을 가져올 수 있습니다. 커뮤니티는 그룹 구성원을 관리하는 데 사용되지만 토픽을 지원하는 커뮤니티에서 메시지를 주고 받을 수는 없습니다. 커뮤니티의 다른 기능에 대해서는 일반 그룹 API를 참고하십시오.
3. 커뮤니티가 성공적으로 생성되면 커뮤니티에서 createTopicInfoCommunity를 호출하여 여러 개의 토픽을 생성할 수 있습니다. [Topic Management](https://www.tencentcloud.com/document/product/1047/48172#.E8.AF.9D.E9.A2.98.E7.AE.A1.E7.90.86)의 ‘Creating a topic’ 단계를 참고하십시오.
4. 토픽 관리에는 ‘토픽 삭제’, ‘토픽 정보 수정’, ‘토픽 목록 가져오기’ 및 ‘토픽 콜백 수신’ 기능도 포함됩니다. 동시에 토픽은 사용자가 메시지를 주고받을 수 있는 커뮤니케이션의 장이며, 관련 인터페이스는 [메시지 생성](https://www.tencentcloud.com/document/product/1047/48172#.E8.AF.9D.E9.A2.98.E6.B6.88.E6.81.AF) 소개를 참고하십시오.
5. 그룹 커뮤니티 구성원: 그룹 구성원 사용자 정의 필드에 그룹 정보를 지정하여 그룹의 커뮤니티 구성원을 표시할 수 있습니다. 이 효과를 구현하려면 모든 커뮤니티 구성원을 로컬로 끌어와 그룹별로 정렬해야 합니다. 그룹 구성원 수가 많은 경우 서버측에서 구성원 그룹화를 구현하는 것이 좋습니다.

## 관련 문서
- [그룹 관리](https://intl.cloud.tencent.com/document/product/1047/33530)
- [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK 다운로드](https://intl.cloud.tencent.com/document/product/1047/33996)
- [SDK 매뉴얼](https://web.sdk.qcloud.com/im/doc/en/TIM.html)
- [Android](https://intl.cloud.tencent.com/document/product/1047/34306)
- [SDK Integration (iOS)](https://intl.cloud.tencent.com/document/product/1047/34307)
- [SDK Integration (Web)](https://www.tencentcloud.com/document/product/1047/34309)

## 문의하기
사용에 문제가 있는 경우 [문의하기](https://intl.cloud.tencent.com/document/product/1047/41676)를 통해 문의해 주시기 바랍니다.
