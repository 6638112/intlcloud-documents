리소스 레벨 권한이란 사용자가 어떤 리소스에 대해 작업을 실행할 수 있는 기능을 지정할 수 있는 권한을 말합니다. CVM(Cloud Virtual Machine)는 리소스 레벨 권한을 일부 지원합니다. 리소스 레벨 권한의 CVM 작업에 대하여 언제 사용자가 작업을 실행하도록 허락할지 또는 언제 사용자가 사용하는 특정 리소스를 허락할지 제어하는 것을 나타냅니다. 
액세스 관리(Cloud Access Management，CAM)에서 권한을 부여할 수 있는 리소스 유형은 다음과 같습니다.

| 리소스 유형 | 권한 부여 정책 중 리소스 메소드 설명 |
| :-------- | -------------- |
| [CVM 인스턴스 관련 설명](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [CVM 키 관련 설명](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [CVM 미러 이미지 관련 설명](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

[CVM 인스턴스 관련](#CVMCorrelation), [CVM 키 관련](#KeyCorrelation) 및 [CVM 미러 이미지 관련](#ImageCorrelation) 은 각각 현재 지원하는 리소스 레벨 권한의 CVM API 작업과 더불어 각각 작업이 지원하는 리소스 및 조건부 키를 소개합니다. **리소스 경로를 구성할 때,**`$region`、`$account` 등 변수 파라미터를 귀하의 실제 파라미터 정보로 수정합니다. 동시에 경로에서 \* 와일드 카드를 사용하실 수 있습니다. 관련 작업 예시는 [CAM 예시](https://intl.cloud.tencent.com/document/product/213/10312)을 참조하시기 바랍니다.
> 표에서 표시되지 않은 CVM API 작업은 해당 CVM API 작업이 리소스 레벨 권한을 지원하지 않음 의미합니다. 지원하지 않는 리소스 레벨 권한의 CVM API 작업에 대해 사용자가 특정 사용자에게 해당 작업 권한을 부여할 수 있습니다. 정책  구문의 리소스 컴포넌트는 반드시 \*로 지정해야 합니다.
>

<span id="CVMCorrelation"></span>
#### CVM 인스턴스 관련 설명

| API Operation | Resource Path | Condition Key |
| :-------- | :--------| :------ |
|DescribeInstanceInternetBandwidthConfigs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesAttribute](https://intl.cloud.tencent.com/document/product/213/33246)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesProject](https://intl.cloud.tencent.com/document/product/213/33245)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesRenewFlag	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RebootInstances](https://intl.cloud.tencent.com/document/product/213/33243)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RenewInstances	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesInternetMaxBandwidth](https://intl.cloud.tencent.com/document/product/213/33241)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesPassword](https://intl.cloud.tencent.com/document/product/213/33240)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/213/33238)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StopInstances](https://intl.cloud.tencent.com/document/product/213/33235)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|



<span id="KeyCorrelation"></span>
#### CVM 키 관련 설명

| API Operation | Resource Path | Condition Key |
| :-------- | :--------| :------ |
|[AssociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33232)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|[CreateKeyPair](https://intl.cloud.tencent.com/document/product/213/33231)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[DeleteKeyPairs](https://intl.cloud.tencent.com/document/product/213/33230)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[DescribeKeyPairs](https://intl.cloud.tencent.com/document/product/213/33229)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| [DisassociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33228)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[ImportKeyPair](https://intl.cloud.tencent.com/document/product/213/33227)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[ModifyKeyPairAttribute](https://intl.cloud.tencent.com/document/product/213/33226)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|

<span id="ImageCorrelation"></span>
#### CVM 미러 이미지 관련 설명

| API Operation | Resource Path | Condition Key |
| :-------- | :--------| :------ |
| [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://intl.cloud.tencent.com/document/product/213/33275)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33273)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://intl.cloud.tencent.com/document/product/213/33269)|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |








