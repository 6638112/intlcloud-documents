VOD는 서버에서 동영상을 업로드할 수 있는 PHP용 SDK를 제공합니다. 업로드 프로세스에 대한 자세한 내용은 [가이드](https://intl.cloud.tencent.com/document/product/266/33912)를 참고하십시오.

## 통합 방식

### Composer를 사용하여 가져오기
```json
{
    "require": {
        "qcloud/vod-sdk-v5": "v2.4.0"
    }
}
```

### 소스 패키지를 통해 설치
1. 프로젝트에서 종속성 관리를 위해 composer 툴을 사용하지 않는 경우, [Github에서 액세스](https://github.com/tencentyun/vod-php-sdk-v5)에서 직접 소스 코드를 다운로드하여 프로젝트에서 사용할 수 있도록 가져올 수 있습니다.
2. vod-sdk.zip 파일을 프로젝트에 압축 해제하고 autoload.php 파일을 가져옵니다.

##  비디오 간편 업로드
### 업로드 객체 초기화
Tencent Cloud API 키로 VodUploadClient 인스턴스를 초기화합니다.

**Composer를 사용하여 가져오기**
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```


**소스 코드를 사용하여 가져오기**
```php
<?php
require 'vod-sdk-v5/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```

### 업로드 요청 객체 생성
```
use Vod\Model\VodUploadRequest;

$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
```

### 업로드 메소드 호출
업로드 메소드를 호출하고 액세스 포인트 리전과 업로드 요청을 전달합니다.
```
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

>?업로드 방법은 파일 크기에 따라 일반 업로드 또는 멀티파트 업로드를 자동으로 선택하므로 멀티파트 업로드의 각 단계를 처리할 필요가 없습니다.

## 고급 기능
### 커버 업로드
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->CoverFilePath = "/data/videos/Wildlife-Cover.png";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
    echo "CoverUrl -> ". $rsp->CoverUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

### 태스크 플로우 지정
먼저 [태스크 플로우 템플릿 생성](https://intl.cloud.tencent.com/document/product/266/14058) 완료 후 이름을 지정합니다. 태스크 플로우를 시작할 때 태스크 플로우 템플릿 이름으로 `Procedure` 매개변수를 설정할 수 있으며, 업로드 성공 시 태스크 플로우가 자동으로 실행됩니다.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->Procedure = "Your Procedure Name";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

### 서브 애플리케이션에 업로드
[서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID를 전달합니다. 업로드 성공 후 리소스는 지정된 서브 애플리케이션에만 속하게 됩니다.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->SubAppId = 101;
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

### 스토리지 리전 지정
[콘솔](https://console.cloud.tencent.com/vod)에서 대상 스토리지 리전이 활성화되었는지 확인하고, 활성화되지 않은 경우 [스토리지 설정 업로드](https://intl.cloud.tencent.com/document/product/266/18874)에 따라 수행한 다음, `StorageRegion` 속성을 통해 스토리지 리전의 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/9760)을 설정할 수 있습니다.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->StorageRegion = "ap-chongqing";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

### 임시 자격 증명으로 업로드
임시 자격 증명의 관련 키 정보를 전달하여 인증 및 업로드에 임시 자격 증명을 사용합니다.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```


### 업로드 프록시 설정
업로드 프록시를 설정하면 관련된 프로토콜과 데이터가 프록시에 의해 처리되므로 프록시를 사용하여 회사의 내부망을 통해 Tencent Cloud에 파일을 업로드할 수 있습니다.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;
use Vod\Model\VodUploadHttpProfile;

$client = new VodUploadClient("your secretId", "your secretKey");
$uploadHttpProfile = new VodUploadHttpProfile("your proxy addr");
$client->setHttpProfile($uploadHttpProfile);
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

### 어댑티브 비트스트림 파일 업로드

이 SDK가 업로드용으로 지원하는 어댑티브 비트스트림 형식에는 HLS 및 DASH가 포함되며, manifest(M3U8 또는 MPD)에서 참고하는 미디어 파일은 상대 경로여야 하고(즉, URL 및 절대 경로는 사용할 수 없음), manifest의 동일 레벨 디렉터리 또는 서브 디렉터리(예: `../`는 사용할 수 없음)에 위치해야 합니다. SDK의 업로드 API를 호출할 때 `MediaFilePath` 매개변수로 manifest 경로를 입력하면 SDK가 관련 미디어 파일 목록을 파싱하여 함께 업로드합니다.

```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/prog_index.m3u8";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // 업로드 예외 처리
    echo $e;
}
```

## API 설명
업로드 클라이언트 클래스 `VodUploadClient`

| 속성 이름      | 속성 설명                   | 유형      | 필수 입력   |
| --------- | ---------------------- | ------- | ---- |
| secretId   | Tencent Cloud API 키 ID.        | String | Yes    |
| secretKey | Tencent Cloud API Key. | String  | Yes    |

업로드 요청 클래스 `VodUploadRequest`

| 속성 이름      | 속성 설명                   | 유형      | 필수 입력   |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath   | 업로드할 미디어 파일의 경로로, 로컬 경로여야 하며 URL을 지원하지 않습니다.| String | Yes    |
| MediaType   | 업로드할 미디어 파일의 유형입니다. 유효한 값은 [미디어 업로드 개요](https://intl.cloud.tencent.com/document/product/266/9760)를 참고하십시오. MediaFilePath 경로에 파일 확장자가 포함된 경우 이 매개변수를 비워 둘 수 있습니다.        | String | No    |
| MediaName   | 업로드된 미디어 파일의 이름입니다. 이 매개변수를 비워 두면 기본적으로 MediaFilePath의 파일 이름이 사용됩니다.      | String | No    |
| CoverFilePath   | 업로드할 커버 파일의 경로로, URL을 지원하지 않는 로컬 경로여야 합니다.| String | No    |
| CoverType   | 업로드할 커버 파일의 유형입니다. 유효 값은 [미디어 업로드 개요](https://intl.cloud.tencent.com/document/product/266/9760)를 참고하십시오. CoverFilePath 경로에 파일 확장자가 포함되어 있으면 이 매개변수를 비워 둘 수 있습니다.        | String | No    |
| Procedure   | 업로드 완료 후 자동으로 실행될 태스크 플로우의 이름으로, 태스크 플로우([API 방식](https://intl.cloud.tencent.com/document/product/266/34167) 또는 [콘솔 방식](https://console.cloud.tencent.com/vod/video-process/taskflow))를 생성할 때 지정하는 매개변수입니다. 자세한 내용은 [태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 참고하십시오.       | String | No    |
| ExpireTime   | ISO 8601 형식의 미디어 파일 만료 시간으로, 자세한 내용은 [ISO 날짜 형식](https://intl.cloud.tencent.com/document/product/266/11732)을 참고하십시오.        | String | No    |
| ClassId   | 관리할 미디어를 분류하는 데 사용되는 클래스 ID로, [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API를 사용하여 클래스를 생성하고, 클래스 ID를 얻을 수 있습니다.        | Integer | No    |
| SourceContext   | 최대 250자의 소스 컨텍스트로, 사용자 요청 정보를 전달하는 데 사용되며 업로드 콜백 API에서 반환됩니다.      | String | No    |
| SubAppId   | VOD의 [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID입니다. 서브 애플리케이션의 리소스에 액세스하려면 이 필드에 서브 애플리케이션 ID를 입력하고, 그렇지 않으면 비워 둡니다.        | Integer | No    |
| StorageRegion   | 파일을 저장할 스토리지 리전입니다. 이 필드는 리전 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/9760)을 입력합니다.        | String | No    |

업로드 응답 클래스 `VodUploadResponse` 

| 속성 이름      | 속성 설명                   | 유형      |
| --------- | ---------------------- | ------- |
| FileId   | 미디어 파일의 고유 ID입니다.        | String |
| MediaUrl | 미디어 재생 주소입니다. | String  |
| CoverUrl | 미디어 커버 주소입니다. | String  |
| RequestId | 요청의 고유 ID입니다. 각 요청은 고유 ID를 반환합니다. RequestId는 문제를 해결하는 데 필요합니다. | String  |

업로드 메소드 `VodUploadClient.upload(String region, VodUploadRequest request)`

| 매개변수 이름     | 매개변수 설명                   | 유형     | 필수 입력 |
| --------- | ---------------------- | ------- | ---- |
| region   | VOD 서버를 요청하는 액세스 포인트 리전으로 스토리지 리전과 다릅니다. 자세한 내용은 [지원 리전 리스트](https://intl.cloud.tencent.com/document/product/266/34113)를 참고하십시오.        | String | Yes    |
| request   | 업로드 요청.        | VodUploadRequest | Yes    |

## 오류 코드
| 상태 코드         | 의미               |
| ----------- | ----------------- |
| InternalError       | 내부 오류.  |
| InvalidParameter.ExpireTime       | 잘못된 매개변수 값: 만료 시간.  |
| InvalidParameterValue.CoverType       | 잘못된 매개변수 값: 커버 유형.     |
| InvalidParameterValue.MediaType       | 잘못된 매개변수 값: 미디어 유형.           |
| InvalidParameterValue.SubAppId       | 잘못된 매개변수 값: 서브 애플리케이션 ID.              |
| InvalidParameterValue.VodSessionKey       | 잘못된 매개변수 값: VOD 세션.              |
| ResourceNotFound       | 리소스가 존재하지 않음.              |

