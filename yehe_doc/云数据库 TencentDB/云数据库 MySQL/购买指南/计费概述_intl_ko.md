>?해당 제품은 유동적인 가격 조회 및 비용 예산을 제공합니다. 이와 관련한 자세한 정보는 [가격 센터](https://intl.cloud.tencent.com/pricing/cdb)에 방문하여 관련 비용을 조회 및 예산을 측정해 보십시오.

## 과금 방식

TencentDB for MySQL 글로벌 포털에 정액 과금제가 추가되었습니다. 기존 글로벌 포털 종량제 가격은 변동 없이 유지됩니다.



TencentDB for MySQL은 메모리와 디스크의 개별 과금 방식을 지원하며 사용자가 효율적으로 조합하여 사용할 수 있도록 더 다양한 과금 방식을 제공합니다.

인스턴스 가격 계산 공식: 인스턴스 가격=메모리 사양 요금+스토리지 용량 요금






## 고급 기능

### 백업 용량

백업 용량은 정액 과금제를 지원하지 않으므로 종량제 과금을 참조 바랍니다.

**인스턴스 연장 관리**

연장 관리 페이지에서는 인스턴스에 대한 일괄 연장, 자동 연장, 만료일 통일, 연장 안 함 표기 등의 기능을 제공합니다.



**인스턴스 업그레이드 알고리즘**

인스턴스의 만료 기간이 T일이고, 업그레이드한 타깃 구성과 기존 구성의 월간 선불금 차액이 C라고 했을 때, 업그레이드 총비용의 계산 공식은 T/30C입니다.

예시, 만료 기간이 15일 남아 있는 1코어 1000MB 메모리 100G 디스크 인스턴스(선불금 24.511달러/월)를 1코어 1000MB 메모리 200G 디스크(선불금 34.653달러/월)로 업그레이드하는 경우, 업그레이드 총비용은 15/30(34.653-24.511)=5.071달러입니다.



**인스턴스 디스크 용량 제한 초과 설명**

비즈니스의 정상적인 수행을 유지하기 위해 디스크 용량을 모두 사용하기 전에 미리 데이터베이스 인스턴스 사양을 업그레이드하거나 디스크 용량을 구매하시기 바랍니다.

인스턴스 스토리지의 데이터양이 인스턴스를 초과하면 인스턴스가 잠겨 데이터를 읽을 수만 있고 입력할 수 없게 되므로, 스케일링하거나 콘솔에서 일부 DB 테이블을 삭제하여 읽기 전용 모드를 해제할 수 있습니다.

데이터베이스가 잠기는 현상이 반복되지 않도록 하려면, 인스턴스의 남은 용량이 20% 이상 혹은 50G 이상(둘 중 하나만 해당하면 됨)으로 유지하면 인스턴스의 잠금 상태가 해제되고, 정상적인 읽기 및 쓰기 기능으로 복구할 수 있습니다.



**재해 복구 인스턴스 동기화 트래픽 요금**

프로모션 기간에는 TencentDB for MySQL 재해 복구 동기화 트래픽 요금이 발생하지 않습니다.

상업화 후 요금 부과 시 별도로 공지합니다.

## 종량제

종량제는 사용한 시간에 따라 총 세 단계로 구분합니다.

| 사용 시간 | 차등 가격 |
|---------|---------|
| 0시간＜사용 시간 ≤ 96시간 | 종량제 1단계 가격 |
| 96시간＜사용 시간 ≤ 360시간 | 종량제 2단계 가격 |
| 사용 시간＞360시간 | 종량제 3단계 가격 |

### 인스턴스 가격

#### 과금 공식
**총비용 = 메모리 사양 요금 + 스토리지 용량 요금 + 백업 용량 요금 + 트래픽 요금(현재 무료)**

#### 과금 항목
<table>
<thead>
<tr>
<th width="15%">과금 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>메모리 사양 요금<br></td>
<td>구매 페이지에서 선택한 인스턴스 사양의 요금은 종량제 차등 요금제를 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>스토리지 용량 요금</td>
<td>구매 페이지에서 선택한 디스크 크기의 요금은 종량제 차등 요금제를 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>백업 용량 요금</td>
<td>TencentDB for MySQL은 리전에 따라 일정 금액의 무료 백업 용량을 제공합니다. 무료 백업 용량의 크기는 상응하는 리전에 있는 모든 고가용 인스턴스(마스터 인스턴스, 재해 복구 인스턴스 포함) 스토리지 용량의 합입니다. <br>무료 백업 용량에서 초과한 부분의 요금은 <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">백업 용량 요금 설명</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>트래픽 요금</td>
<td>공용 네트워크 트래픽 요금은 현재 무료입니다.</td>
</tr>
</tbody></table>

#### 종량제 가격

##### 고가용성 버전
<table >
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(달러/GB/시간)</td>
  <td rowspan=2 >디스크(달러/GB/시간)</td>
 </tr>
 <tr>
  <td >1단계</td>
  <td>2단계</td>
  <td>3단계</td>
 </tr>
 <tr>
  <td >광저우</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>칭위안</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>상하이</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>베이징</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>청두</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>충칭</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>중국홍콩</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>타이베이</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>싱가포르</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>방콕</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>뭄바이</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>서울</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>도쿄</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>버지니아주</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>토론토</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>모스크바</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### 읽기 전용 인스턴스

<table>
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(달러/GB/시간)</td>
  <td rowspan=2 >디스크(달러/GB/시간)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>1단계</td>
  <td class=xl1529815>2단계</td>
  <td class=xl1529815>3단계</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>광저우</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>칭위안</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>상하이</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>베이징</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>청두</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>충칭</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>중국홍콩</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>타이베이</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>싱가포르</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>방콕</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>뭄바이</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>서울</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>도쿄</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>버지니아주</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>토론토</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>모스크바</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## 과금 예시
>? 다음 제시되는 가격은 예시이며, 실제 가격은 리전, 이벤트, 정책 등에 따라 변동되니 공식 홈페이지의 실제 가격을 참조하십시오.
>

### 정액 과금제
광저우 리전의 예시:
- 광저우 3존에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스(고가용성 버전) 1개를 정액 과금제로 1달간 구매한 경우.
- 광저우 4존에서 4코어 8000MB 메모리, 200GB 디스크의 TencentDB for MySQL 인스턴스(고가용성 버전) 1개를 정액 과금제로 1달간 구매한 경우.

총비용 = 메모리 사양 요금 + 스토리지 용량 요금 + 백업 용량 요금

##### 메모리 사양 요금 + 스토리지 용량 요금
요금 계산은 아래와 같습니다.
메모리 사양 요금 + 스토리지 용량 요금 = 2 × 114.93달러/월 + (500GB + 200GB) × 0.1014달러/GB/월 × 1개월 = 300.84달러

##### 백업 용량 요금
광저우 3존에서 실행 중인 고가용성 버전 인스턴스에서 구매한 데이터베이스 스토리지 용량이 월 500GB이고, 광저우 4존에서 실행 중인 고가용성 버전 인스턴스에서 구매한 데이터베이스 스토리지 용량이 월 200GB라면, 광저우 리전에서는 매월 700GB의 무료 백업 용량이 제공됩니다.

광저우 리전의 총 백업 용량이 700GB를 초과할 경우, 초과부분에 대해서  별도로 과금됩니다. 예를 들어, 데이터 백업이 800GB에 이르고 로그 백업이 100GB에 달하면, 해당 시간당 과금 용량은 200GB(800 + 100 - 700 = 200GB)이며, 초과분의 과금은 이런 방식으로 계속 이어집니다.

백업 용량 부과 요금(시간당) = 200GB (초과한 백업 용량은 실제 시나리오에 따라 지속 변동될 수 있음) × 0.000127달러/GB/시간

### 종량제
광저우 리전에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스 1개를 종량제로 400시간 구매한 경우.
1단계 요금: (0.0250달러/GB/시간×8GB+500GB × 0.0003)×96시간=33.6달러
2단계 요금: (0.0200달러/GB/시간×8GB+500GB × 0.0003)×264시간=81.84달러
3단계 요금: (0.0150달러/GB/시간×8GB+500GB × 0.0003)×40시간=10.8달러
인스턴스 요금 = 1단계 요금 + 2단계 요금 + 3단계 요금 = 126.24달러

## 이슈 질문
#### 정액 과금제 인스턴스를 사용 중인데, 다른 요금이 추가로 차감되는 이유는 무엇인가요?
백업 용량이 무료 한도를 초과했는지 확인해주시기 바랍니다. 무료 한도를 초과한 백업 용량에 대해서는 요금이 부과될 수 있습니다.
사용한 백업 용량에 대한 정보는 [MySQL 콘솔](https://console.cloud.tencent.com/cdb/backup)의 데이터베이스 백업 페이지에서 확인할 수 있으며, 자세한 백업 용량 요금 정보는 [백업 용량 부과 요금 설명](https://cloud.tencent.com/document/product/236/36263)을 참조 바랍니다.

#### 종량제 인스턴스를 사용하지 않을 경우 요금이 부과되나요?
종량제 인스턴스는 요금이 계속 차감되며, 인스턴스를 사용하지 않을 때는 요금 차감이 지속되지 않도록 즉시 폐기하실 수 있습니다.

## 관련 문서
- TencentDB for MySQL은 콘솔과 API에서 인스턴스를 구매할 수 있습니다. 자세한 내용은 [구매 방법](https://intl.cloud.tencent.com/document/product/236/5160)을 참조하십시오.
- TencentDB for MySQL은 만료 이전부터 리소스 릴리스까지의 기간 동안 사용자에게 알람 정보를 발송합니다. 자세한 내용은 [연체 설명](https://intl.cloud.tencent.com/document/product/236/5159)을 참조하십시오.
- TencentDB for MySQL은 콘솔에서 반환 및 환불 신청을 할 수 있습니다. 자세한 내용은 [환불 설명](https://intl.cloud.tencent.com/document/product/236/14618)을 참조하십시오.
- TencentDB for MySQL은 인스턴스 사양의 업그레이드 또는 다운그레이드가 가능합니다. 자세한 내용은 [인스턴스 비용 조정 설명](https://intl.cloud.tencent.com/document/product/236/32345)을 참조하십시오. 
