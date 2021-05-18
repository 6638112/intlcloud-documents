Referer 링크 도용 방지 설정을 통해 사용자 정의 Referer 블랙/화이트리스트 및 규칙 내용을 설정하여 재생 요청을 수락 또는 거부함으로써 라이브 방송 콘텐츠를 보호할 수 있습니다. 또한 CSS는 사용자가 빈 Referer의 액세스 허용 여부를 선택할 수 있도록 지원합니다.

## 설정 원리

Referer 링크 도용 방지는 HTTP 프로토콜이 지원하는 Referer 매커니즘을 기반으로 하여 HTTP request에 포함된 Referer 필드를 통해 요청의 출처를 식별하고 액세스의 합법성을 검증하며, 이를 기준으로 라이브 방송 콘텐츠의 요청을 수락하거나 거부합니다.

## 주의 사항
- Referer 정보는 HTTP에 포함되어 있습니다. 설정을 활성화한 뒤에는 RTMP를 재생할 수 없으며 LEB 스트림은 Referer 설정에 대한 검증을 진행하지 않습니다. Referer를 설정해야 하는 경우, FLV나 HLS로 재생하는 것을 권장합니다.
- Referer 링크 도용 방지 설정을 활성화, 비활성화 및 수정한 뒤 약 15-20분 후 적용되며 스트림을 다시 푸시하지 않아도 됩니다.

## 전제 조건

- CSS 서비스가 활성화되어 있고 [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 합니다.
- [재생 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)가 완료되어 있어야 합니다.


[](id:open)
## Referer 링크 도용 방지 활성화

1.   [[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)]를 선택하고 Referer 링크 도용 방지를 설정할 **재생 도메인**또는 오른쪽의 [관리]를 클릭하여 도메인 관리 페이지로 이동합니다.
2.   [액세스 제어]>[Referer 링크 도용 방지 설정]에서 [편집]을 클릭하여 Referer 링크 도용 방지 설정 페이지로 이동합니다.
 ![](https://main.qcloudimg.com/raw/32461edf0353c2c95925b74d80dc25b3.png)
3.   ![](https://main.qcloudimg.com/raw/c032c517e25867ff592f128424154688.png)버튼을 클릭해 Referer 링크 도용 방지 활성화를 선택하고 다음과 같이 설정합니다.
 ![](https://main.qcloudimg.com/raw/551044de4acd79683ae69cf106a87c0b.png)
<table id="setmess">
<tr><th width="14%">설정 항목</th><th>설명</th>
</tr><tr>
<td>링크 도용 방지 유형</td>
<td>클릭하여 Referer<b>블랙리스트</b> 또는 <b>화이트리스트</b>설정 선택:
<ul style="margin:0">
<li>블랙리스트와 화이트리스트는 서로 배척하므로 동시에 적용할 수 없습니다. </li>
<li>Referer 화이트리스트가 설정되면 화이트리스트에 있는 사용자의 액세스가 허용되고 라이브 방송 콘텐츠를 요청할 수 있습니다. 반대로 화이트리스트에 없는 사용자의 액세스는 거부되며 라이브 방송 콘텐츠도 요청할 수 없습니다. </li>
<li>Referer 블랙리스트가 설정되면 블랙리스트에 있는 사용자의 액세스가 거부되고 라이브 방송 콘텐츠를 요청할 수 없게 됩니다. 반대로 블랙리스트에 없는 사용자의 액세스는 허용되며 라이브 방송 콘텐츠도 요청할 수 있습니다. </li>
</ul></td>
</tr><tr>
<td>빈 Referer 허용</td>
<td><ul style="margin:0">
<li>허용을 선택하면 Referer 필드가 비어있거나 없는 HTTP 요청의 액세스가 허용되며, 브라우저를 통해 직접 라이브 방송 URL에 액세스할 수 있습니다. </li>
<li>미허용을 선택하면 빈 Referer의 액세스가 거부됩니다. </li>
</ul></td>
</tr><tr>
<td>링크 도용 방지 규칙</td>
<td><ul style="margin:0">
<li>최대<b>100</b>개의 규칙을 설정할 수 있으며, 줄 바꿈으로 구분하십시오. </li>
<li><b>IP</b>와 <b>도메인</b>의 2가지 포맷 입력을 지원하며, 실제 매칭 시 경로 접두사 매칭(도메인과 IP)과 와일드카드 매칭(와일드카드 서브도메인)을 지원합니다. 예: <ul>
<li/><code>101.1.0.1</code>과 <code>www.test.com</code>을 설정하면, <code>101.1.0.1/157</code>과 <code>www.test.com/tencent</code>에 모두 적용됩니다.
<li/><code>*.test.com</code>을 설정하면, <code>www.test.com</code>과 <code>a.test.com</code>에 모두 적용됩니다. </ul></li>
<li>규칙 내용이 공란인 경우 블랙리스트와 화이트리스트 모두 미설정 상태임을 의미합니다. </li>
</ul></td>
</tr></table>
4. [Save]을 클릭하여 설정을 저장합니다.


[](id:change)
## Referer 링크 도용 방지 수정
1.   [[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)]를 선택하고 Referer 링크 도용 방지 설정을 수정할 **재생 도메인** 또는 오른쪽의 [관리]를 클릭하여 도메인 관리 페이지로 이동합니다.
2.   [액세스 제어]>[Referer 링크 도용 방지 설정]에서 [편집]을 클릭하여 Referer 링크 도용 방지 설정 페이지로 이동합니다.
3.   사용자의 니즈에 따라 [설정 항목](#setmess) 정보를 수정하고 [저장]을 클릭하면 수정이 완료됩니다.

![](https://main.qcloudimg.com/raw/a8c79376ed22b4e47f35e69411c6df10.png)

[](id:close)
## Referer 링크 도용 방지 비활성화
[Referer 링크 도용 방지 활성화](#open) 후 다음과 같은 방법으로 해당 기능을 비활성화할 수 있습니다.

1.   [[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)]를 선택하고 Referer 링크 도용 방지 설정을 비활성화할 **재생 도메인** 또는 오른쪽의 [관리]를 클릭하여 도메인 관리 페이지로 이동합니다.
2.   [액세스 제어]>[Referer 링크 도용 방지 설정]에서 [편집]을 클릭하여 Referer 링크 도용 방지 설정 페이지로 이동합니다.
3.   ![](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) 버튼을 클릭해 Referer 링크 도용 방지 비활성화를 선택합니다.
4. [저장]을 클릭합니다.

![](https://main.qcloudimg.com/raw/eb36bc40cca9f19e198fc742256fed21.png)






