## 소개

본 문서는 객체의 고급 인터페이스, 간단한 작업, 멀티파트 작업 관련 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업명                   | 작업 설명                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회                 |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551?) | 객체 및 지난 버전 리스트 조회 | 버킷의 일부 또는 모든 객체와 이전 버전 정보 조회 |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편한 객체 업로드             | 버킷에 객체 업로드                           |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회           | 객체 메타데이터 정보 조회                           |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드                 | 하나의 객체를 로컬에 다운로드                             |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정             | 파일을 타깃 경로에 복사                             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제 | 버킷에서 지정 객체 삭제                         |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제             | 버킷에서 다수의 객체 삭제                         |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구             | 아카이브 유형의 객체 검색 및 액세스                       |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 객체 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 객체의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업 중지 및 업로드된 파트 삭제 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

지정 버킷의 모든 객체를 조회합니다(List Objects).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### 요청 예시

#### 예시1: 접두사와 시작 객체가 지정된 객체 리스트 조회

[//]: # ".cssg-snippet-get-bucket-comp"

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'Marker' => 'doc/picture.jpg',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름     | 유형   | 설명                                                         | 필수 입력 여부 |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket       | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Delimiter    | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 폴더 시뮬레이션)                | 아니오       |
| EncodingType | String | 기본 인코딩이 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | 아니오       |
| Marker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시 | 아니오       |
| Prefix       | String | 기본값 null. 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭 | 아니오       |
| MaxKeys      | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                    | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [Marker] => doc/picture.jpg
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextMarker] => doc/exampleobject
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject
                            [LastModified] => 2019-02-14T12:20:40.000Z
                            [ETag] => "e37b429559d82e852af0b2f5b4d078ab72b90208"
                            [Size] => 6532594
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [LastModified] => 2019-03-04T06:34:43.000Z
                            [ETag] => "988f9f28e68eba9b8c1f5f98ccce0a3c"
                            [Size] => 28
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )
                )
            [RequestId] => NWNhMzM0MmZfOWUxYzBiMDlfOTk2YV83ZWE3ODE=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                                                         | 부모 노드   |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Name         | String | 버킷 이름. 포맷은 BucketName-APPID                           | 없음       |
| Delimiter    | String | 세퍼레이터 설정(예시: `/`을 설정해 폴더 시뮬레이션)                          | 없음       |
| EncodingType | String | 반환값의 인코딩 방식 규정                                         | 없음       |
| Marker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시 | 없음       |
| Prefix       | String | 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭  | 없음       |
| MaxKeys      | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                 | 없음       |
| IsTruncated  | Int    | 반환된 객체의 차단 여부 표시                                  | 없음       |
| Contents     | Array  | 반환된 객체 리스트                                               | 없음       |
| Content      | Array  | 반환된 객체 속성으로, 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' 등의 정보를 담은 모든 객체의 메타데이터를 포함한 리스트 | Contents |

### 객체 및 이전 버전 리스트 조회 

#### 기능 설명

버킷의 일부 또는 모든 객체와 이전 버전 정보를 조회합니다.

#### 방법 모델

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### 요청 예시

#### 예시1: 이전 객체 리스트 조회

[//]: # ".cssg-snippet-list-object-versioning"

```php
try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'KeyMarker' => 'doc/picture.jpg',
        'VersionIdMarker' => 'MTg0NDUxODMyMTE2ODY0OTExOTk3W',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름        | 유형   | 설명                                                         | 필수 입력 여부 |
| --------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket          | String | 버킷 이름은 BucketName-APPID로 구성                         | 예       |
| Prefix          | String | 기본값 null. 객체 키를 필터링해 prefix로 시작하는 객체와 매칭   | 아니오       |
| Delimiter       | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 폴더 시뮬레이션)                | 아니오       |
| KeyMarker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 key 시작 위치 표시 | 아니오       |
| VersionIdMarker | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시 | 아니오       |
| MaxKeys         | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                         | 아니오       |
| EncodingType    | String | 기본 인코딩이 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [KeyMarker] => string
            [VersionIdMarker] => string
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextKeyMarker] => string
            [NextVersionIdMarker] => string
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject1
                            [VersionId] => null
                            [IsLatest] => 1
                            [LastModified] => 2019-06-13T09:24:52.000Z
                            [ETag] => "96e79218965eb72c92a549dd5a330112"
                            [Size] => 6
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1251668577
                                )
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
                            [IsLatest] => 1
                            [LastModified] => 2019-06-18T12:47:03.000Z
                            [ETag] => "698d51a19d8a121ce581499d7b701668"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1251668577
                                )
                        )
                    )
            [RequestId] => NWQwOGVkZGRfMjViMjU4NjRfODNjN18xMTE5YWI4
        )

)
```

#### 반환 결과 설명

| 매개변수 이름            | 유형   | 설명                                                         | 부모 노드   |
| ------------------- | ------ | ------------------------------------------------------------ | -------- |
| Name                | String | 버킷 이름. 포맷은 BucketName-APPID                           | 없음       |
| Delimiter           | String | 세퍼레이터 설정(예시: `/`을 설정해 폴더 시뮬레이션)                          | 없음       |
| EncodingType        | String | 반환값의 인코딩 방식 규정                                         | 없음       |
| KeyMarker           | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 key 시작 위치 표시 | 없음       |
| VersionIdMarker     | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시 | 없음       |
| NextKeyMarker       | String | IsTruncated가 true이면 그 다음 반환된 객체 리스트 키의 시작 위치 표시 | 없음       |
| NextVersionIdMarker | String | IsTruncated가 true이면 그 다음 반환된 객체 리스트의 VersionId 시작 위치 표시 | 없음       |
| Prefix              | String | 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭  | 없음       |
| MaxKeys             | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                    | 없음       |
| IsTruncated         | Int    | 반환된 객체의 차단 여부 표시                                  | 없음       |
| Versions            | Array  | 여러 버전의 객체 메타데이터를 포함한 리스트                            | 없음       |
| Version             | Array  | 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', 'Size' 등의 정보를 담은 여러 버전의 객체 메타데이터를 포함한 리스트 | Versions |
| CommonPrefixes      | Array  | Prefix로 시작하고 Delimiter로 끝나는 모든 객체를 동일한 종류로 분류      | 없음       |



### 간편한 객체 업로드

#### 기능 설명

객체를 지정 버킷에 업로드합니다(PUT Object). 최대 5GB 미만인 객체의 업로드를 지원합니다. 5GB를 초과하는 경우 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 또는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용하여 업로드하십시오.

#### 방법 모델

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### 요청 예시

#### 예시1: 로컬 파일 업로드

[//]: # ".cssg-snippet-put-object"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
    )); 
    // 요청 완료 
    print_r($result);
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시2: 보관된 파일 업로드

[//]: # ".cssg-snippet-put-object-archive"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'StorageClass' => 'Archive'
    )); 
    // 요청 완료 
    print_r($result); 
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시3: 지정된 Content-type 파일 업로드

[//]: # ".cssg-snippet-put-object-with-content-type"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentType' => 'text/xml'
    )); 
    // 요청 완료 
    print_r($result); 
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 아니오       |
| ACL                  | String      | 객체 ACL 설정, 예시: private, public-read                    | 아니오       |
| Body                 | File/String | 업로드한 콘텐츠                                                   | 예       |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | 아니오       |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                           | 아니오       |
| ContentEncoding      | String | 인코딩 포맷. Content-Encoding 설정                              | 아니오       |
| ContentLanguage      | String | 언어 유형. Content-Language 설정                              | 아니오       |
| ContentLength        | Int         | 전송 길이 설정                                                 | 아니오       |
| ContentType          | String | 콘텐츠 유형. Content-Type 설정                                  | 아니오       |
| Expires              | String      | Content-Expires 설정                                              | 아니오     |
| Metadata             | Array       | 사용자 정의 파일 메타데이터                                       | 아니오     |
DTS| StorageClass         | String      | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참조    | 아니오       |
| ContentMD5           | String      | 업로드 파일의 MD5 값을 인증에 사용하는 것으로 설정                                | 아니오     |
| ServerSideEncryption | String      | 서버 암호화 방법                                               | 아니오     |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ObjectURL] => http://lewzylucd2-1251668577.cos.ap-chengdu.myqcloud.com/123
        )

)

```

#### 반환 결과 설명

| 매개변수 이름  | 유형   | 설명                       | 부모 노드 |
| --------- | ------ | -------------------------- | ------ |
| ETag                 | String      | 업로드된 파일의 MD5 값          | 없음     |
| VersionId | String | 버전 제어 활성화 후 파일의 버전 넘버 | 없음     |

### 객체 메타데이터 조회

#### 기능 설명

객체 메타데이터(HEAD Object)를 조회합니다.

#### 방법 모델

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-head-object"

```php
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| VersionId | String | 버전 제어 활성화 후 지정 파일 상세 버전 지정                             | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [AcceptRanges] => 
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 12:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhMzU3Y2ZfMzFhYzM1MGFfODdhMF8xOTExM2U=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름             | 유형   | 설명                                               | 부모 노드 |
| -------------------- | ------ | -------------------------------------------------- | ------ |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | 없음       |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                           | 없음       |
| ContentEncoding      | String | 인코딩 포맷. Content-Encoding 설정                              | 없음       |
| ContentLanguage      | String | 언어 유형. Content-Language 설정                              | 없음       |
| ContentLength        | Int    | 전송 길이 설정                                       | 없음     |
| ContentType          | String | 콘텐츠 유형. Content-Type 설정                                  | 없음       |
| Metadata             | Array       | 사용자 정의 파일 메타데이터                                       | 없음     |
| StorageClass         | String | 파일의 스토리지 유형(예시: STANDARD, STANDARD_IA, ARCHIVE). 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참조. | 없음     |
| ServerSideEncryption | String | 서버 암호화 방법                                     | 없음     |
| ETag                 | String | 파일의 MD5 값                                      | 없음     |
| Restore              | String | 보관된 파일 복구 정보                                 | 없음     |

### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다(GET Object).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### 요청 예시

#### 예시1: 로컬에 파일 다운로드

[//]: # ".cssg-snippet-get-object"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => 'path/to/localFile',
    )); 
    // 요청 완료
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: range에 따라 파일 콘텐츠 획득

[//]: # ".cssg-snippet-get-object-range"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'Range' => 'bytes=0-10'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 지정 버전 파일 다운로드

[//]: # ".cssg-snippet-get-object-with-versionId"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름                   | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket                     | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key                        | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| SaveAs                     | String | 로컬에 저장한 로컬 파일 경로                                     | 아니오       |
| VersionId                  | String | 버전 제어 활성화 후 지정 파일 상세 버전 지정                             | 아니오       |
| Range                      | String | 다운로드 파일의 범위 설정(포맷: bytes=first-last)                  | 아니오       |
| ResponseCacheControl       | String | 응답 헤더의 Cache-Control 설정                                   | 아니오       |
| ResponseContentDisposition | String | 응답 헤더의 Content-Disposition 설정                             | 아니오       |
| ResponseContentEncoding    | String | 응답 헤더의 Content-Encoding 설정                                | 아니오       |
| ResponseContentLanguage    | String | 응답 헤더의 Content-Language 설정                                | 아니오       |
| ResponseContentType        | String | 응답 헤더의 Content-Type 설정                                    | 아니오       |
| ResponseExpires            | String | 응답 헤더의 Content-Expires 설정                                 | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [DeleteMarker] => 
            [AcceptRanges] => bytes
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 20:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentRange] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [WebsiteRedirectLocation] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )

            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhNDBmYzBfNmNhYjM1MGFfMmUzYzFfMWIzMDYz
        )

)
```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------------------ | ------ |
| Body                 | File/String | 콘텐츠 다운로드                                                     | 없음     |
| ETag                 | String      | 파일의 MD5 값                                                | 없음     |
| Expires              | String      | Content-Expires                                              | 없음     |
| Metadata             | Array       | 사용자 정의 파일 메타데이터                                       | 없음     |
| StorageClass         | String      | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참조 | 없음     |
| ContentMD5           | String      | 업로드 파일의 MD5 값을 인증에 사용하는 것으로 설정                                | 없음     |
| ServerSideEncryption | String      | 서버 암호화 방법                                               | 없음     |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | 없음     |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                           | 없음       |
| ContentEncoding      | String | 인코딩 포맷. Content-Encoding 설정                              | 없음       |
| ContentLanguage      | String      | 언어 유형. Content-Language 설정                              | 없음     |
| ContentLength        | Int         | 전송 길이 설정                                                 | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| Metadata             | Array       | 사용자 정의 파일 메타데이터                                       | 없음     |
| Restore              | String      | 보관된 파일 복구 정보                                            | 없음     |

### 객체 복사 설정

객체를 타깃 경로에 복사합니다(PUT Object - Copy).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### 요청 예시

#### 예시1: 객체 복사

[//]: # ".cssg-snippet-copy-object"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 지정 버전 객체 복사

[//]: # ".cssg-snippet-copy-object-with-versionId"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 스토리지 유형을 아카이브 유형으로 수정

[//]: # ".cssg-snippet-copy-object-update-storage-class"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시4: meta 속성 수정

[//]: # ".cssg-snippet-copy-object-update-metadata"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'MetadataDirective' => 'Replaced',
        'Metadata' => array(
            'key1' => 'value1',
            'key2' => 'value2',
        )
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름          | 유형   | 설명                                                         | 필수 입력 여부 |
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket            | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key               | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| CopySource        | String | Appid, Bucket, Key, Region을 포함한 원본 파일의 복사 경로 설명<br>예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | 예       |
| MetadataDirective | String | 옵션 값은 Copy와 Replaced. Copy로 설정하는 경우 설정된 사용자 메타데이터 정보를 무시하고 바로 파일 복사. Replaced로 설정하는 경우 설정된 메타정보에 따라 메타데이터 수정. 타깃 경로와 루트 경로가 같은 경우 반드시 Replaced로 설정 | 아니오       |

### 단일 객체 삭제

#### 기능 설명

버킷에서 지정 객체(파일/객체)를 삭제합니다.

#### 방법 모델

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-delete-object"

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId' //버킷의 버전 제어가 비활성화된 경우 해당 매개변수 사용 불가
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| VersionId | String | 파일 버전 넘버 삭제                                             | 아니오       |

### 다수의 객체 삭제

#### 기능 설명

버킷에서 다수의 객체(파일/객체)를 일괄 삭제합니다.

#### 방법 모델

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-delete-multi-object"

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
                'VersionId' => 'string' //버킷의 버전 제어가 비활성화된 경우 해당 매개변수 사용 불가
            ),  
            // ... repeated
        ),  
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Objects   | Array  | 객체 리스트 삭제                                                 | 예       |
| Object   | Array  | 삭제한 객체                                                 | 예       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| VersionId | String | 파일 버전 넘버 삭제                                             | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Deleted] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject1
                        )
                )
            [Errors] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject2
                            [Code] => 
                            [Message] => 
                        )
                )
            [RequestId] => NWNhZWYzYWNfMTlhYTk0MGFfNGRjX2MzZTVhOQ==
        )
）
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명                 | 부모 노드         |
| -------- | ------ | -------------------- | -------------- |
| Deleted  | Array  | 삭제 완료한 객체 리스트 | 없음             |
| Errors   | Array  | 삭제 실패한 객체 리스트 | 없음             |
| Key      | String | 객체 키               | Deleted/Errors |
| Code     | String | 실패 에러 코드           | Errors         |
| Message  | String | 실패 에러 정보         | Errors         |

### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-restore-object"

```php
try {
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'Days' => 10,
        'CASJobParameters' => array(
            'Tier' =>'Expedited'
        )    
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름         | 유형   | 설명                                                         | 필수 입력 여부 |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket           | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key              | String | 객체 키                                                       | 예       |
| Days             | String | 임시 사본 만료 기간 설정(단위: 일)                             | 예       |
| CASJobParameters | Array  | 정보 복구                                                     | 예       |
| Tier             | String | CAS 유형의 데이터를 복구하는 경우 Tier는 COS가 지원하는 3가지 복구 모드(Expedited, Standard, Bulk) 중 지정 가능. DEEP ARCHIVE 유형의 데이터를 복구하는 경우 Tier는 COS가 지원하는 2가지 복구 모드(Standard, Bulk) 중 지정 가능 | 예       |

## 멀티파트 작업

다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 파트를 업로드한 후 멀티파트 업로드를 완료합니다.
- 멀티파트 업로드 재개: 업로드된 파트를 조회하고 파트를 업로드한 후 멀티파트 업로드를 완료합니다.
- 업로드된 파트를 삭제합니다.

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-list-multi-upload"

```php
try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'prfixKeyMarker',
        'UploadIdMarker' => 'string',
        'Prefix' => 'prfix',
        'MaxUploads' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름       | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket         | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Delimiter      | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 폴더 시뮬레이션)                | 아니오       |
| EncodingType   | String | 기본 인코딩이 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | 아니오       |
| KeyMarker      | String | 반환된 parts 리스트의 시작 위치 표시                            | 아니오       |
| UploadIdMarker | String | 반환된 parts 리스트의 시작 위치 표시                            | 아니오       |
| Prefix         | String | 기본값 null. parts 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭 | 아니오       |
| MaxUploads     | Int    | 반환되는 최대 parts 수량. 기본값은 최대 1,000개                      | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [EncodingType] => 
            [KeyMarker] => 
            [UploadIdMarker] => 
            [MaxUploads] => 1000
            [Prefix] => 
            [IsTruncated] => 
            [Uploads] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 1551693693b1e6d0e00eec30c534059865ec89c9393028b60bfaf167e9420524b25eeb2940
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-04T10:01:33.000Z
                        )

                    [1] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 155374001100563fe0e9d37964d53077e54e9d392bce78f630359cd3288e62acee2b719534
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-28T02:26:51.000Z
                        )

                )

            [RequestId] => NWNhNDJmNzBfZWFhZDM1MGFfMjYyM2FfMWIyNzhh
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                               | 부모 노드  |
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket       | String | 버킷 이름. 포맷은 BucketName-APPID | 없음      |
| IsTruncated  | Int    | 반환된 객체의 차단 여부 표시        | 없음      |
| Uploads      | Array  | 반환된 멀티파트 리스트                     | 없음      |
| Upload       | Array  | 반환된 멀티파트 속성                     | Uploads |
| Key          | String | 객체 키                           | Upload  |
| UploadId     | String | 객체 멀티파트 업로드 ID                  | Upload  |
| Initiator    | String | 해당 멀티파트 작업자 초기화               | Upload  |
| Owner        | String | 멀티파트 소유자                         | Upload  |
| StorageClass | String | 멀티파트 스토리지 유형                       | Upload  |
| Initiated    | String | 멀티파트 초기화 시간                     | Upload  |


### 멀티파트 업로드 초기화

#### 기능 설명

Multipart Upload 업로드 작업을 초기화합니다(Initiate Multipart Upload).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-init-multi-upload"

```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket               | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key                  | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | 아니오       |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                           | 아니오       |
| ContentEncoding      | String | 인코딩 포맷. Content-Encoding 설정                              | 아니오       |
| ContentLanguage      | String | 언어 유형. Content-Language 설정                              | 아니오       |
| ContentLength | Int    | 전송 길이 설정                                                 | 아니오       |
| ContentType          | String | 콘텐츠 유형. Content-Type 설정                                  | 아니오       |
| Expires              | String      | Content-Expires 설정                                              | 아니오     |
| Metadata             | Array  | 사용자 정의 파일 메타데이터                                       | 아니오       |
| StorageClass         | String | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참조.       |    아니오       |
| ContentMD5           | String | 업로드 파일의 MD5 값을 인증에 사용하는 것으로 설정                                | 아니오       |
| ServerSideEncryption | String | 서버 암호화 방법                                               | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554277569b3e83df05c730104c325eb7b56000449fb7d51300b0728aacde02a6ea7f6c033
            [RequestId] => NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명                               | 부모 노드 |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | String | 버킷 이름. 포맷은 BucketName-APPID | 없음     |
| Key      | String | 객체 키                             | 없음     |
| UploadId | String | 객체 멀티파트 업로드 ID                   | 없음     |



### 멀티파트 업로드

파일을 멀티파트 업로드합니다(Upload Part).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part"

```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', //UploadId는 객체 멀티파트 업로드 ID. 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 
        'PartNumber' => 1, //PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름      | 유형        | 설명                                                         | 필수 입력 여부 |
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket        | String      | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key           | String      | 객체 키                                                       | 예       |
| UploadId      | String      | UploadId는 객체 멀티파트 업로드 ID, 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 | 예       |
| Body          | File/String | 업로드한 콘텐츠                                                   | 예       |
| PartNumber    | Int         | PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합      | 예       |
| ContentLength | Int         | 전송 길이 설정                                                 | 아니오       |
| ContentMD5    | String      | 업로드 파일의 MD5 값을 인증에 사용하는 것으로 설정                                | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명          | 부모 노드 |
| -------- | ------ | ------------- | ------ |
| ETag         | String | 멀티파트 MD5 값                  | 없음     |




### 멀티파트 복사

#### 기능 설명

다른 객체를 멀티파트에 복사합니다(Upload Part-Copy).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part-copy"

```php
try {
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', //예시에서는 처음의 2개 바이트만 복사
        'UploadId' => 'exampleUploadId', //UploadId는 객체 멀티파트 업로드 ID. 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 
        'PartNumber' => 1, //PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름      | 유형   | 설명                                                         | 필수 입력 여부 |
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket        | String | 버킷 이름. 포맷은 BucketName-APPID                           | 예       |
| Key           | String | 객체 키                                                       | 예       |
| UploadId      | String | UploadId는 객체 멀티파트 업로드 ID. 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 | 예       |
| CopySource    | String | Appid, Bucket, Key, Region을 포함한 원본 파일의 복사 경로 설명<br>예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | 예       |
| CopySourceRange    | String | 소스 객체 복사의 범위 설명(포맷: bytes=first-last). 범위를 지정하지 않으면 전체 소스 객체 복사 | 아니오       |
| PartNumber    | Int    | PartNumber는 멀티파트의 일련 번호. COS는 일련 번호에 따라 멀티파트 병합      | 예       |
| ContentLength | Int    | 전송 길이 설정                                                 | 아니오       |
| ContentMD5    | String | 업로드 파일의 MD5 값을 인증에 사용하는 것으로 설정                                | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                           | 부모 노드 |
| ------------ | ------ | ------------------------------ | ------ |
| ETag         | String | 멀티파트 MD5 값                  | 없음     |
| LastModified | String | 반환된 객체의 최종 수정 시간(GMT 포맷) | 없음     |


### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-list-parts"

```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'UploadId' => 'exampleUploadId',
        'PartNumberMarker' => 1,
        'MaxParts' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름         | 유형   | 설명                                    | 필수 입력 여부 |
| ---------------- | ------ | --------------------------------------- | -------- |
| Bucket           | String | 버킷 이름. 포맷은 BucketName-APPID      | 예       |
| Key              | String | 객체 키                                  | 예       |
| UploadId         | String | 객체 멀티파트 업로드 ID                       | 예       |
| PartNumberMarker | Int    | 반환된 parts 리스트의 시작 위치 표시       | 아니오       |
| MaxParts         | Int    | 반환되는 최대 parts 수량. 기본값은 최대 1,000개 | 아니오       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554279643cf19d71bb5fb0d29613e5541131f3a96387d9e168cd939c23a3d608c9eb94707
            [Owner] => Array
                (
                    [ID] => 1250000000
                    [DisplayName] => 1250000000
                )
            [PartNumberMarker] => 1
            [Initiator] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )
            [StorageClass] => Standard
            [MaxParts] => 1000
            [IsTruncated] => 
            [Parts] => Array
                (
                    [0] => Array
                        (
                            [PartNumber] => 2
                            [LastModified] => 2019-04-03T08:21:28.000Z
                            [ETag] => "b948e77469189ac94b98e09755a6dba9"
                            [Size] => 1048576
                        )
                    [1] => Array
                        (
                            [PartNumber] => 3
                            [LastModified] => 2019-04-03T08:21:22.000Z
                            [ETag] => "9e5060e2994ec8463bfbebd442fdff16"
                            [Size] => 1048576
                        )                       
                )
            [RequestId] => NWNhNDZkNTJfOGNiMjM1MGFfMTRlYl8xYmJiOTU=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름         | 유형   | 설명                                    | 부모 노드 |
| ---------------- | ------ | --------------------------------------- | ------ |
| Bucket           | String | 버킷 이름. 포맷은 BucketName-APPID      | 없음     |
| Key              | String | 객체 키                                                       | 없음     |
| UploadId         | String | 객체 멀티파트 업로드 ID                       | 없음     |
| IsTruncated      | Int    | 반환된 객체의 차단 여부 표시             | 없음     |
| PartNumberMarker | Int    | 반환된 parts 리스트의 시작 위치 표시       | 없음     |
| MaxParts         | Int    | 반환되는 최대 parts 수량. 기본값은 최대 1,000개 | 없음     |
| Initiator        | String | 해당 멀티파트 작업자 초기화                    | 없음     |
| Parts            | Array  | 반환된 멀티파트 리스트                          | 없음     |
| Part             | Array  | 반환된 멀티파트 속성                          | Parts  |
| PartNumber       | Int    | 멀티파트 일련 번호                                | Part   |
| LastModified     | String | 멀티파트 마지막 업로드 시간                      | Part   |
| ETag             | String | 파일의 MD5 값                           | Part   |
| Size             | String | 멀티파트 크기                              | Part   |



### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### 요청 예시

[//]: # ".cssg-snippet-complete-multi-upload"

```php
try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
        'Parts' => array(
            array(
                'ETag' => 'exampleETag',
                'PartNumber' => 1,
            )), 
            // ... repeated
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름   | 유형   | 설명                               | 필수 입력 여부 |
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket     | String | 버킷 이름. 포맷은 BucketName-APPID | 예       |
| Key        | String | 객체 키                             | 예       |
| UploadId   | String | 객체 멀티파트 업로드 ID                  | 예       |
| Parts      | Array  | 멀티파트 정보 리스트                       | 예       |
| Part       | Array  | 멀티파트 업로드한 콘텐츠 정보                 | 예       |
| ETag       | String | 멀티파트 MD5 값                     | 예       |
| PartNumber | Int    | 멀티파트 일련 번호                           | 예       |

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 방법 모델

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-abort-multi-upload"

```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| Bucket   | String | 버킷 이름. 포맷은 BucketName-APPID | 예       |
| Key      | String | 객체 키                             | 예       |
| UploadId | String | 객체 멀티파트 업로드 ID                  | 예       |



## 고급 인터페이스(권장)

이 챕터에서는 업로드 및 복사 작업을 캡슐화한 COS의 고급 인터페이스를 소개합니다. 사용자는 상응하는 매개변수만 설정하면 됩니다. 해당 인터페이스는 파일 크기에 따라 간편 업로드(복사)와 멀티파트 업로드(복사)를 결정합니다. 인터페이스 사용 전 [시작하기](https://intl.cloud.tencent.com/document/product/436/12266)에서 안내한 초기화 절차가 완료되었는지 확인하십시오.

### 복합 업로드

#### 기능 설명

해당 인터페이스는 용량이 작은 파일에는 간편 업로드 인터페이스를, 용량이 큰 파일에는 멀티파트 업로드 인터페이스를 호출합니다. 인터페이스 매개변수는 `PUT Object`와 `Upload Part` 인터페이스를 참조하십시오.

#### 요청 예시

#### 예시1: 로컬에 객체 업로드

[//]: # ".cssg-snippet-transfer-upload-file"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $body = fopen('path/to/localFile', 'rb')
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 보관된 객체 업로드

[//]: # ".cssg-snippet-transfer-upload-file-archive"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 멀티파트 크기별로 meta 업로드할 객체 지정

[//]: # ".cssg-snippet-transfer-upload-file-with-meta"

```php
try {
    $result = $cosClient->Upload(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'Metadata' => array(
                'string' => 'string',
            ),
            'PartSize' => 10 * 1024 * 1024
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

### 복합 복사

#### 기능 설명

해당 인터페이스는 용량이 작은 파일에는 객체 복사 인터페이스를, 용량이 큰 파일에는 멀티파트 복사 인터페이스를 호출합니다. 인터페이스 매개변수는 `PUT Object - Copy`와 `Upload Part - Copy` 인터페이스를 참조하십시오.

#### 요청 예시

#### 예시1: 객체 복사

[//]: # ".cssg-snippet-transfer-copy-object"

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceobject', 
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-storage-class"

#### 예시2: COS 유형 변환

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'examplebucket-1250000000', 
            'Key' => 'exampleobject', 
        ),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-metadata"

##### 예시3: COS 속성 수정

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //포맷: BucketName-APPID
        $key = 'exampleobject', //그 외의 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        ),
        $options = array(
            'MetadataDirective' => 'Replaced',
            'Metadata' => array(
                'string' => 'string',
            ),
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```
