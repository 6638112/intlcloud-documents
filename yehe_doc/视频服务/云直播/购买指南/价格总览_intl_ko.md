LVB 요금제는 기본 서비스 요금, 부가 서비스 요금 및 확장 서비스 요금이 포함되며, 요금 구성은 다음 그림과 같습니다.

![img](https://main.qcloudimg.com/raw/67a295effc191c4f710d9e2622fa1b01.png)

- [기본 서비스 요금](#base): LVB 이용 후 발생하는 라이브 방송 소모 비용으로, 트래픽 방식 또는 피크 대역폭 방식 2가지 과금 방식을 제공합니다.
- [부가 서비스 요금](#appreciation): 라이브 방송 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 등 부가 서비스 이용 비용으로, 해당 기능은 기본적으로 꺼져 있으며 사용 시에만 과금됩니다.
- [확장 서비스 요금](#extensions): Tencent Cloud의 기타 제품과 결합하여 함께 제공되는 부가 서비스로, 다른 클라우드 서비스가 각각의 요금 규정에 따라 관련 비용을 청구합니다.


## 기본 서비스 요금
<table>
<tr><th width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td>LVB 트래픽(기본)</td>
<td>과금 방식이 <b>일별 트래픽 과금</b> 방식인 경우, LVB 발생 비용은 <strong>트래픽 소모량에 따라 과금됩니다.</strong></td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">후불 - 일별 과금</a></td>
</tr><tr>
<td>LVB 대역폭 피크</td>
<td>과금 방식이 <b>일별 대역폭 과금</b> 방식인 경우, LVB 발생 비용은 <b>대역폭 피크에 따라 과금됩니다.</b></td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">후불 - 일별 과금</a></td>
</tr></table>


>? 과금 방식을 변경하고 싶은 경우, [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참조하십시오.  



## 부가 서비스 요금

<table>
<tr><th colspan=2 width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td rowspan=2>라이브 방송 트랜스 코딩</td>
<td>LVB 트랜스 코딩</td>
<td>
	<li>라이브 방송에서 표준 트랜스 코딩 시나리오 사용 지원</li>
	<li><a href="https://intl.cloud.tencent.com/document/product/267/31064">워터마크</a> 추가 또는 <a href="https://intl.cloud.tencent.com/document/product/267/37665">클라우드 단 혼합 스트리밍</a> 기능을 활성화 할 경우 표준 트랜스 코딩 비용이 발생하며, 해상도는 전송한 라이브 방송 스트리밍 해상도를 기준으로 합니다.</li>
	<li>트랜스 코딩은 비용이 발생하며 <b>트랜스 코딩 시간에 따라 과금됩니다.</b></li>
</td>
<td>
	<a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding">후불 - 일별 과금</a>
</td>
</tr><tr>
<td>고속 HD 트랜스 코딩</td>
<td>
	<li>라이브 방송에서 고속 HD 트랜스 코딩 시나리오 사용 지원</li>
	<li><a href="https://intl.cloud.tencent.com/document/product/267/31064">워터마크</a> 추가 또는 <a href="https://intl.cloud.tencent.com/document/product/267/37665">클라우드 단 혼합 스트리밍</a> 기능을 활성화할 경우 표준 트랜스 코딩 비용이 발생하며, 해상도는 전송한 라이브 방송 스트리밍 해상도를 기준으로 합니다.</li>
	<li>트랜스 코딩은 비용이 발생하며 <b>트랜스 코딩 시간에 따라 과금됩니다.</b></li></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818#top-speed-codec-transcoding">후불 - 일별 과금</a></td>
</tr><tr>
	<td colspan=2>글로벌 가속</td>
	<td>
		<li>사용자와 전역 가속 원본 서버 연결을 통해 생성되는 다운스트리밍 트래픽과 대역폭입니다.</li>
		<li>2가지 과금 방식 제공: 트래픽 과금 방식, 대역폭 과금 방식</b></li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#global-acceleration">후불 - 일별 과금</a></td>
</tr>
    <tr>
	<td colspan=2>라이브 방송 녹화</td>
	<td>
		<li>라이브 방송 녹화는 녹화 템플릿에 따라 생성되는 녹화 파일로 VOD에 저장됩니다.</li>
		<li>녹화로 인해 발생하는 서비스 비용은 <b>LVB 녹화 동시 피크 채널 수에 따라 과금됩니다.</b></li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-recording">후불 - 월별 과금</a></td>
</tr><tr>
<td colspan=2>라이브 방송 화면 캡처</td>
<td>
	<li>라이브 방송 화면 캡처는 템플릿 예약 시간에 따라 라이브 방송 스트리밍 화면을 캡처하며, 이미지는 COS에 저장됩니다.</li>
	<li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-screencapturing">후불 - 월별 과금</a></td>
</tr><tr>
	<td colspan=2>음란물 감지 화면 캡처</td>
	<td>음란물 감지 화면 캡처는 음란물 감지 비용과 화면 캡처 비용이 모두 발생합니다.
		<li>음란물 감지로 인해 발생하는 서비스 비용은 <b>음란물 감지 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
		<li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#intelligent-porn-detection">후불 - 월별 과금</a></td>
</tr><tr>
</tr><tr>
</tr>
</table>




## 확장 서비스 요금

<table>
<tr><th width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td>녹화 저장</td>
<td>라이브 방송 녹화 파일은 VOD에 저장되어야 하며 비용이 발생합니다. <b>데이터 실제 저장 시간 및 저장량에 따라 과금되며</b> 별도의 VOD 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">비즈니스 매니저에게 신청하기</a></td>
</tr><tr>
<td>화면 캡처 저장</td>
<td>라이브 방송 화면 캡처와 음란물 감지로 생성되는 화면 캡처 파일은 COS에 저장되어야 하며 비용이 발생합니다. <strong>데이터 실제 저장 시간 및 저장량에 따라 과금되며</strong> 별도의 COS 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS - 종량제</a></td>
</tr></table>