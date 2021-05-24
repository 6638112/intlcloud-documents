## 기능 설명
COS Migration은 COS의 데이터 마이그레이션 기능을 결합한 통합형 툴입니다. 간단한 설정만으로 원본 주소의 데이터를 COS로 빠르게 마이그레이션할 수 있습니다. 특징은 다음과 같습니다.
- 다양한 데이터 소스:
   - 로컬 데이터: 로컬에 저장되어 있는 데이터를 COS로 마이그레이션합니다.
   - 기타 클라우드 스토리지: 현재 AWS S3, Alibaba Cloud OSS, Qiniu 스토리지를 COS로 마이그레이션할 수 있으며, 앞으로 지속해서 확장될 예정입니다.
   - URL 리스트: 지정한 URL 다운로드 리스트에 따라 COS에 다운로드 및 마이그레이션합니다.
   - Bucket 상호 복사: COS의 Bucket 데이터 상호 복사는 계정 및 리전 간의 데이터 복사를 지원합니다.
- 중단된 시점부터 이어 올리기: 툴에서는 업로드 시 중단된 시점부터 이어 올리기를 지원합니다. 용량이 큰 파일의 경우 중도에 종료되거나 서비스 장애가 발생하면 다시 툴을 실행하여 업로드가 완료되지 않은 파일을 계속해서 업로드할 수 있습니다.
- 멀티파트 업로드: 객체를 멀티파트 방식으로 COS에 업로드합니다.
- 병렬 업로드: 여러 객체 동시 업로드를 지원합니다.
- 마이그레이션 검증: 객체를 마이그레이션한 후 검증합니다.

>!
>- COS Migration의 인코딩 포맷은 UTF-8 포맷만 지원합니다.
>- 해당 툴을 사용해 동일한 이름의 파일을 업로드하면 더 오래된 파일을 덮어쓰며, 동일한 이름의 파일 존재 여부 대조는 지원하지 않습니다.

## 사용 환경
#### 시스템 환경
Windows, Linux, macOS 시스템

#### 소프트웨어 종속
- JDK 1.8 X64 이상. JDK 관련 설치 및 설정은 [Java 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10865)을 참조하십시오.
- Linux 환경에서는 IFUNC 지원이 필요합니다. 실행 환경에서 binutils 2.20 버전 이상을 유지하십시오.

## 사용 방법
### 1. 툴 획득
[COS Migration 툴](https://github.com/tencentyun/cos_migrate_tool_v5)을 다운로드합니다.

### 2. 툴 패키지 압축 해제
#### Windows
 압축을 해제하고 다음과 같이 특정 디렉터리에 저장합니다.
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
압축을 해제하고 특정 디렉터리에 저장합니다.
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### 마이그레이션 툴 구조
올바로 압축 해제된 COS Migration 툴 디렉터리 구조는 다음과 같습니다.
<pre>
COS_Migrate_tool
|——conf  #구성 파일이 위치한 디렉터리
|   |——config.ini  #구성 파일 마이그레이션
|——db    #마이그레이션 성공 기록 저장
|——dep   #프로그램 메인 로직 컴파일로 생성되는 JAR 패키지
|——log   #툴 실행 중 생성되는 로그
|——opbin #컴파일에 사용되는 스크립트
|——src   #툴 소스 코드
|——tmp   #임시 파일 저장 디렉터리
|——pom.xml #프로젝트 구성 파일
|——README  #설명 문서
|——start_migrate.sh  #Linux에서 마이그레이션 실행 스크립트
|——start_migrate.bat #Windows에서 마이그레이션 실행 스크립트
</pre>

>?
 - db 디렉터리는 툴 마이그레이션 성공을 기록하는 문서 표식으로, 마이그레이션 작업 시마다 먼저 db의 기록을 비교하여 현재 파일 표식에 기록이 되어 있는 경우 해당 파일을 건너뛰고, 그렇지 않으면 파일을 마이그레이션합니다.
 - log 디렉터리에는 툴 마이그레이션 시의 모든 로그가 기록되어 있습니다. 마이그레이션 과정에서 오류가 발생한 경우 먼저 해당 디렉터리의 error.log를 확인하십시오.

### 3. config.ini 구성 파일 수정
마이그레이션 실행 스크립트를 실행하기 전에 config.ini 구성 파일(경로: `./conf/config.ini`)을 수정해야 하며, config.ini 내용은 다음과 같이 몇 부분으로 나뉘어 있습니다.

#### 3.1 마이그레이션 유형 설정
type은 마이그레이션 유형을 의미합니다. 사용자가 마이그레이션 요건에 따라 해당 표식을 작성합니다. 예를 들어, 로컬 데이터를 COS에 마이그레이션하는 경우 `[migrateType]`의 설정 내용은 `type=migrateLocal`이 됩니다.
<pre>[migrateType]
type=migrateLocal
</pre>

현재 지원하는 마이그레이션 유형은 다음과 같습니다.

| migrateType | 설명 |
| ------| ------ |
| migrateLocal| 로컬에서 COS로 마이그레이션 |
| migrateAws| AWS S3에서 COS로 마이그레이션 |
| migrateAli| Alibaba OSS에서 COS로 마이그레이션 |
| migrateQiniu| Qiniu에서 COS로 마이그레이션 |
| migrateUrl| 다운로드 URL에서 COS로 마이그레이션 |
| migrateBucketCopy| 원본 Bucket에서 타깃 Bucket으로 복사|
|migrateUpyun  | Upyun에서 COS로 마이그레이션 |

#### 3.2 마이그레이션 작업 설정
실제 마이그레이션 요건에 따라 관련 설정을 진행하며, 주로 마이그레이션할 타깃 COS의 정보 설정 및 마이그레이션 작업 관련 설정이 포함됩니다.
<pre>
# 마이그레이션 툴의 일반 설정 섹션에는 마이그레이션할 타깃 COS의 계정 정보가 포함됩니다.
[common]
secretId=COS_SECRETID
secretKey=COS_SECRETKEY
bucketName=examplebucket-1250000000
region=ap-guangzhou
storageClass=Standard
cosPath=/
https=off
tmpFolder=./tmp
smallFileThreshold=5242880
smallFileExecutorNum=64
bigFileExecutorNum=8
entireFileMd5Attached=on
daemonMode=off
daemonModeInterVal=60
executeTimeWindow=00:00,24:00
encryptionType=sse-cos
</pre>

| 이름 | 설명 |기본값|
| ------| ------ |----- |
| secretId| 사용자 보안키 SecretId. `COS_SECRETID`를 사용자의 실제 키 정보로 변경합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 조회하여 획득할 수 있습니다. |-|
| secretKey| 사용자 보안키 SecretKey. `COS_SECRETKEY`를 사용자의 실제 키 정보로 변경합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 조회하여 획득할 수 있습니다.|-|
| bucketName| 타깃 Bucket의 이름. `<BucketName-APPID>` 포맷으로 이름이 생성됩니다. 즉, Bucket 이름에는 반드시 APPID가 포함됩니다. 예: examplebucket-1250000000 |-|
| region| 타깃 Bucket의 Region 정보. COS의 리전 약칭은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. |-|
| storageClass|스토리지 유형: Standard(표준 스토리지), Standard_IA(표준IA 스토리지), Archive(CAS) |Standard|
| cosPath|마이그레이션할 COS 경로. `/`는 Bucket의 루트 경로에 마이그레이션하는 것을 의미하며, `/folder/doc/`는 Bucket의 `/folder/doc/`에 마이그레이션하는 것을 의미합니다. `/folder/doc/`가 존재하지 않는 경우 자동으로 경로를 생성합니다.|/|
| https| HTTPS를 사용한 전송 여부: on - 활성화, off - 비활성화. 활성화할 경우 전송 속도가 비교적 느리며, 전송 보안 요건이 높은 시나리오에 적합합니다.|off|
| tmpFolder|기타 클라우드 스토리지에서 COS로 마이그레이션 시 임시 파일을 저장하는 디렉터리로 마이그레이션 완료 후에는 삭제됩니다. 필요한 포맷은 절대 경로입니다.<br>Linux에서 세퍼레이터는 싱글 슬래시입니다(예: `/a/b/c`). <br>Windows에서 세퍼레이터는 더블 역슬래시입니다(예: `E:\\a\\b\\c`).<br>기본적으로 툴 경로 아래의 tmp 디렉터리입니다.|./tmp|
| smallFileThreshold| 저용량 파일의 임계값 바이트. 이 임계값 이상이면 멀티파트 업로드를 사용하며, 그렇지 않으면 간편 업로드를 사용합니다. 기본값: 5MB |5242880|
| smallFileExecutorNum|저용량 파일(smallFileThreshold보다 작은 파일)의 동시 접속 수이며, 간편 업로드를 사용합니다. 공인 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.|64|
| bigFileExecutorNum| 대용량 파일(smallFileThreshold 이상의 파일)의 동시 접속 수이며, 멀티파트 업로드를 사용합니다. 공인 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.|8|
| entireFileMd5Attached|마이그레이션 툴에서 전체 텍스트의 MD5를 계산한 후 파일의 사용자 정의 헤더 x-cos-meta-md5에 저장해 이후 검증에 사용합니다. COS에 멀티파트 업로드하는 대용량 파일의 etag는 전체 텍스트의 MD5가 아니기 때문입니다.|on|
| daemonMode|daemon 모드 활성화 여부: on - 활성화, off - 비활성화. daemon은 프로그램을 중단하지 않고 순환적으로 동기화를 실행한다는 의미입니다. 각 동기화 간격은 daemonModeInterVal 매개변수에서 설정합니다.|off|
| daemonModeInterVal|각 동기화 완료 후 다음 동기화를 실행할 시간. 단위: 초 |60|
| executeTimeWindow|시간 창 실행. 시간 단위: 분. 해당 매개변수로 마이그레이션 툴이 매일 실행되는 시간대를 정의합니다. 예:<br>매개변수가 03:30,21:00인 경우, 새벽 03:30부터 저녁 21:00 사이에 작업을 실행한다는 의미이며, 다른 시간에는 휴면 상태가 됩니다. 휴면 상태에서는 마이그레이션을 일시 중지하고 다음 시간 창이 자동으로 이어서 실행할 때까지 마이그레이션 진행률을 유지합니다.|00:00,24:00|
| encryptionType  |  sse-cos 서버를 사용해 암호화    |     기본적으로 작성하지 않으며, 서버 암호화가 필요한 경우에 작성합니다.       |

#### 3.3 데이터 소스 정보 설정
`[migrateType]`의 마이그레이션 유형에 따라 해당 섹션을 설정합니다. 예를 들어, `[migrateType]`을 `type=migrateLocal`로 설정한 경우 `[migrateLocal]` 섹션만 설정하면 됩니다.

**3.3.1 로컬 데이터 소스 migrateLocal 설정**

로컬에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
<pre>
# 로컬에서 COS로 마이그레이션 시 설정 섹션
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
excludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| 설정 항목 | 설명 |
| ------| ------ |
|localPath|로컬 디렉터리. 필요한 포맷은 절대 경로입니다.<br><li>Linux에서 세퍼레이터는 싱글 슬래시입니다(예: `/a/b/c`). <br><li>Windows에서 세퍼레이터는 더블 역슬래시입니다(예: `E:\\a\\b\\c`).|
|excludes| 제외할 디렉터리 또는 파일의 절대 경로. localPath 아래에 있는 특정 디렉터리 또는 파일은 마이그레이션하지 않는다는 의미이며, 여러 절대 경로 사이는 세미콜론으로 구분합니다. 작성하지 않으면 localPath 아래 전체를 마이그레이션합니다.|
|ignoreModifiedTimeLessThanSeconds| 업데이트 시간과 현재 시간의 차이가 일정 시간 이하인 파일 제외. 단위: 초. 기본적으로 설정하지 않으며, lastmodified 시간에 따라 필터링하지 않음을 의미합니다. 클라이언트에서 파일 업데이트와 동시에 마이그레이션 툴을 실행할 때 사용하며, 현재 업데이트 중인 파일은 COS에 마이그레이션하지 않습니다. 예를 들어, 300으로 설정하면 업데이트한 지 5분 이상 지난 파일만 업로드합니다.|

**3.3.2 Alibaba OSS 데이터 소스 migrateAli 설정**

Alibaba Cloud OSS에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
<pre># Alibaba OSS에서 COS로 마이그레이션 시 설정 섹션
[migrateAli]
bucket=bucket-aliyun
accessKeyId=yourAccessKeyId
accessKeySecret=yourAccessKeySecret
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 항목 | 설명 |
| ------| ------ |
|bucket|Alibaba Cloud OSS Bucket 이름|
|accessKeyId|yourAccessKeyId를 사용자 키로 변경 |
|accessKeySecret| yourAccessKeySecret을 사용자 키로 변경|
|endPoint|Alibaba Cloud endpoint 주소|
|prefix|마이그레이션할 경로의 접두사. Bucket 아래에 있는 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|
|proxyHost|프록시를 사용해 액세스할 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

**3.3.3 AWS 데이터 소스 migrateAws 설정**

AWS에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
<pre># AWS에서 COS로 마이그레이션 시 설정 섹션
[migrateAws]
bucket=bucket-aws
accessKeyId=AccessKeyId
accessKeySecret=SecretAccessKey
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 항목 | 설명 |
| ------| ------ |
|bucket| AWS 객체 스토리지 Bucket 이름|
|accessKeyId|AccessKeyId를 사용자 키로 변경|
|accessKeySecret| SecretAccessKey를 사용자 키로 변경|
|endPoint|AWS의 endpoint 주소. 반드시 도메인을 사용해야 하며 region은 사용할 수 없습니다.|
|prefix|마이그레이션할 경로의 접두사. Bucket 아래에 있는 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|
|proxyHost|프록시를 사용해 액세스할 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

 
**3.3.4 Qiniu 데이터 소스 migrateQiniu 설정**

Qiniu에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
<pre># Qiniu에서 COS로 마이그레이션 시 설정 섹션
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=AccessKey
accessKeySecret=SecretKey
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 항목 | 설명 |
| ------| ------ |
|bucket|Qiniu 객체 스토리지 Bucket 이름|
|accessKeyId|AccessKey를 사용자 키로 변경 |
|accessKeySecret| SecretKey를 사용자 키로 변경|
|endPoint|Qiniu 다운로드 주소. downloadDomain에 해당합니다.|
|prefix|마이그레이션할 경로의 접두사. Bucket 아래에 있는 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|
|proxyHost|프록시를 사용해 액세스할 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

 
**3.3.5 URL 리스트 데이터 소스 migrateUrl 설정**

지정한 URL 리스트에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
<pre>
# URL 리스트에서 COS로 다운로드 및 마이그레이션 시 설정 섹션
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>
     
| 설정 항목 | 설명 |
| ------| ------ |
|urllistPath|URL 리스트의 주소. URL 텍스트로 한 행당 URL 원시 주소를 작성합니다(예: `http://aaa.bbb.com/yyy/zzz.txt`, 큰따옴표 또는 기타 부호 추가할 필요 없음). URL 리스트의 주소는 절대 경로여야 합니다. <br><li>Linux에서 세퍼레이터는 싱글 슬래시입니다(예: `/a/b/c.txt`). <br><li>Windows에서 세퍼레이터는 더블 역슬래시입니다(예: `E:\\a\\b\\c.txt`).<br>디렉터리를 작성한 경우 해당 디렉터리 아래의 모든 파일을 urllist 파일로 간주하여 스캐닝 및 마이그레이션합니다.|

 
**3.3.6 Bucket 상호 복사 migrateBucketCopy 설정**

COS의 지정 Bucket에서 다른 Bucket으로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.
>!마이그레이션을 요청하는 계정은 원본 읽기 권한 및 타깃 쓰기 권한을 가지고 있어야 합니다.

<pre>
# 원본 Bucket에서 타깃 Bucket으로 마이그레이션 시 설정 섹션
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId=COS_SECRETID
srcSecretKey=COS_SECRETKEY
srcCosPath=/
</pre>

| 설정 항목 | 설명 |
| ------| ------ |
|srcRegion|원본 Bucket의 Region 정보. [가용 리전](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.|
|srcBucketName|원본 Bucket의 이름. `<BucketName-APPID>`포맷으로 이름이 생성됩니다. 즉, Bucket 이름에는 반드시 APPID가 포함됩니다. 예: examplebucket-1250000000|
|srcSecretId|원본 Bucket이 종속된 사용자의 키 SecretId. [Tencent Cloud API 키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터인 경우 srcSecretId와 common의 SecretId가 동일하며, 그렇지 않은 경우 계정 간 Bucket 복사입니다.|
|srcSecretKey|원본 Bucket이 종속된 사용자의 키 secret_key. [Tencent Cloud API 키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터인 경우 srcSecretKey와 common의 secretKey가 동일하며, 그렇지 않은 경우 계정 간 Bucket 복사입니다.|
|srcCosPath|마이그레이션할 COS 경로. 해당 경로 아래에 있는 파일을 타깃 Bucket에 마이그레이션합니다.|

**3.3.7 Upyun 데이터 소스 migrateUpyun 설정**
Upyun에서 COS로 마이그레이션하는 경우 해당 부분을 설정합니다. 구체적인 설정 항목 및 설명은 다음과 같습니다.

```
[migrateUpyun]
# Upyun에서 마이그레이션
bucket=xxx
#Upyun 작업자 ID
accessKeyId=xxx
#Upyun 작업자 비밀번호     
accessKeySecret=xxx       
prefix=

#Upyun sdk 제한. 해당 proxy는 전역 proxy로 설정됩니다.
proxyHost=
proxyPort=
```

| 설정 항목 | 설명 |
| ------| ------ |
|bucket|Upyun USS Bucket 이름|
|accessKeyId|Upyun 작업자 ID로 변경|
|accessKeySecret| Upyun 작업자 비밀번호로 변경|
|prefix|마이그레이션할 경로의 접두사. Bucket 아래에 있는 모든 데이터를 마이그레이션할 경우 prefix는 비워둡니다.|
|proxyHost|프록시를 사용해 액세스할 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

### 4. 마이그레이션 툴 실행
#### Windows
**start_migrate.bat**을 더블 클릭하면 실행됩니다.

#### Linux
1.config.ini 구성 파일에서 설정을 읽어오는 실행 명령어는 다음과 같습니다.
<pre>
sh start_migrate.sh
</pre>
2. 일부 매개변수는 명령 라인에서 설정을 읽어오며, 실행 명령어는 다음과 같습니다.
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>?
> - 툴에서 설정 항목을 읽어오는 방식: 명령 라인에서 읽어오기, 구성 파일에서 읽어오기
> - 명령 라인의 우선순위가 구성 파일보다 높습니다. 즉, 동일한 설정 항목의 경우 명령 라인의 매개변수를 우선 채택합니다.
> - 명령 라인에서 설정 항목을 읽어오는 방식은 서로 다른 마이그레이션 작업을 동시에 실행할 때 편리합니다. 단, Bucket 이름, COS 경로, 마이그레이션할 원본 경로 등과 같은 두 작업의 주요 설정 항목이 일치하지 않아야 합니다. 서로 다른 마이그레이션 작업에서 쓰는 db 디렉터리가 다르면, 동시 마이그레이션을 보장할 수 있습니다. 본 문서의 툴 구조에서 db 정보를 참조하십시오.
> - 설정 항목은 **-D{sectionName}.{sectionKey}={sectionValue}** 형식으로 구성됩니다. 여기서 sectionName은 구성 파일의 섹션 이름, sectionKey는 섹션의 설정 항목 이름, sectionValue는 섹션의 설정 항목 값을 의미합니다. 마이그레이션할 COS 경로를 설정할 경우 **-Dcommon.cosPath=/bbb/ddd**로 표시합니다.

## 마이그레이션 메커니즘 및 프로세스
### 마이그레이션 메커니즘 원리

COS 마이그레이션 툴은 스테이트풀이며, 이미 마이그레이션 완료한 정보를 db 디렉터리에 기록해 KV 형식으로 leveldb 파일에 저장합니다. 마이그레이션할 때마다 마이그레이션 경로가 먼저 db에 존재하는지 확인하고, 존재할 경우 속성이 db와 일치하면 마이그레이션을 건너뜁니다. 일치하지 않을 경우 마이그레이션을 진행합니다. 여기서 속성은 마이그레이션 유형에 따라 다릅니다. 로컬 마이그레이션은 mtime을 판단하며, 기타 클라우드 스토리지 마이그레이션과 Bucket 복사는 원본 파일의 etag 및 길이가 db와 동일한지 판단합니다. 이에 따라 db를 참조하여 마이그레이션을 완료한 기록이 있는지 확인하며 COS에서는 확인하지 않습니다. 마이그레이션 툴이 아닌 다른 방식(예: COSCMD 또는 콘솔)으로 파일을 삭제 및 수정하고 마이그레이션 툴을 실행할 경우 이러한 변화를 감지하지 못해 새로 마이그레이션하지 않습니다.

### 마이그레이션 프로세스 순서

1. 구성 파일을 읽어 마이그레이션 type에 따라 해당 설정 섹션을 읽어오고 매개변수 검사를 실행합니다.
2. 지정한 마이그레이션 유형에 따라 db에서 마이그레이션할 모든 파일의 표식을 스캔 및 대조하고 업로드 허용 여부를 판단합니다.
3. 마이그레이션 실행 과정에서 실행 결과를 출력합니다. 여기서 inprogress는 마이그레이션 중, skip은 건너뜀, fail은 실패, ok는 성공, condition_not_match는 마이그레이션 조건을 충족하지 못해 건너뛴 파일(예: lastmodifed 및 excludes)을 의미합니다. 실패에 대한 세부 정보는 log의 error 로그에서 확인할 수 있으며, 실행 과정 순서도는 다음 이미지와 같습니다.
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. 전체 마이그레이션 종료 후 누적 마이그레이션 성공 수, 실패 수, 건너뛴 수, 소모 시간을 포함한 통계 정보를 출력합니다. 실패 상황에 대해서는 error 로그를 확인하거나 다시 실행하십시오. 마이그레이션 툴은 이미 마이그레이션 완료한 파일은 건너뛰므로 마이그레이션에 성공하지 못한 파일을 다시 마이그레이션합니다. 실행 완료 결과 순서도는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQ
COS Migration 툴 사용 중 마이그레이션 실패, 실행 오류 등의 이상 상황이 발생하는 경우 [COS Migration 툴 관련 FAQ](https://intl.cloud.tencent.com/document/product/436/30585)를 통해 해결할 수 있습니다.
