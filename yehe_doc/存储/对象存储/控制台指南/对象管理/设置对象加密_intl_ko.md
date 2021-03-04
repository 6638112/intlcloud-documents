## 소개

COS 콘솔을 통해 버킷에 보관 중인 객체에 암호화 설정을 하여 정보 유출을 방지합니다. 암호화에 대한 자세한 정보는 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참조하십시오. 다음은 객체 암호화 설정 방법에 대한 상세 소개입니다.

>
> - 이 작업은 아카이브 유형의 객체 암호화 설정은 지원하지 않습니다. 암호화가 필요할 경우 먼저 객체 [복구 작업](https://intl.cloud.tencent.com/document/product/436/30961)을 진행하고 복구 완료 후 표준 스토리지나 표준IA 스토리지 유형으로 수정한 후 암호화 설정을 진행하십시오.
> - 액세스 암호화 객체와 액세스 비암호화 객체는 실제로 별 차이가 없지만 두 객체 모두 액세스 권한 소유가 전제 조건입니다.
> - 서버 암호화는 객체 데이터 암호화만 지원하며 객체 메타데이터 암호화는 지원하지 않습니다. 서버로 암호화한 객체의 경우에는 반드시 익명 사용자가 아닌 유효한 서명으로 액세스해야 합니다.
> - 버킷의 객체를 나열할 때 객체의 암호화 여부와 관계없이 리스트는 모든 객체의 리스트를 반환합니다.

## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 [버킷 리스트]를 클릭합니다.
3. 버킷 정책 추가가 필요한 버킷을 선택하여 버킷에 있는 상세 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/5d2fdd122fd896764e0f03fc31d7e58b.png)
4. [파일 리스트]를 클릭하여 암호화를 설정할 객체를 찾아 오른쪽 작업 바에서 [자세히]를 클릭합니다.
![](https://main.qcloudimg.com/raw/05c7a0e867badbd56242b93f6425561d.png)
5. 아래 페이지에서 [서버 암호화] 설정 페이지를 찾아 알맞는 암호화 방식을 선택합니다. 현재는 아래 암호화 방식을 지원합니다.
 - SSE-COS: COS에서 호스팅하는 키를 통한 서버 암호화 방식입니다. SSE-COS 정보에 관한 자세한 내용은 [서버 암호화 개요: SSE-COS](https://intl.cloud.tencent.com/document/product/436/18145)를 참조하십시오.
 - SSE-KMS: Tencent Cloud 키 관리 시스템 KMS에서 호스팅하는 키를 통한 서버암호화 방식이며 기본 키나 자체 구축 키를 사용할 수 있습니다. 암호화에 대한 자세한 사항은 [KMS 키 생성](https://cloud.tencent.com/document/product/573/8875)을 참조하십시오. SSE-KMS에 대한 자세한 내용은 [서버 암호화 개요: [SSE-KMS](https://intl.cloud.tencent.com/document/product/436/18145)를 참조하십시오.
![](https://main.qcloudimg.com/raw/48c8b3a3d32170db7172397398c8a883.png)
6. 마지막으로 [저장]을 클릭합니다.
7. 여러 객체의 암호화 설정을 해야 할 경우 여러 객체를 선택한 후 [더 많은 조작]에서 [암호화 방식 수정]을 선택하십시오.
![](https://main.qcloudimg.com/raw/539f0f91d94effe782c5615259ceaa51.png)

>
> - SSE-KMS 암호화를 처음 사용한다면 [KMS 서비스 활성화](https://buy.cloud.tencent.com/kms)가 필요합니다.
> - 현재 SSE-KMS 암호화는 베이징, 상하이, 광저우 리전에서만 지원합니다.
