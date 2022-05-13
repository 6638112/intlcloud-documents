## 제품 개요

Android용 Tencent Cloud RT-Cube Superplayer Adapter는 타사 또는 독점 플레이어를 사용하여 Tencent Cloud PAAS 리소스에 연결하려는 고객을 위해 VOD에서 제공하는 플레이어 플러그인입니다. 일반적으로 플레이어 기능을 사용자 정의해야 하는 고객이 사용합니다.

## SDK 다운로드[](id:sdkDownload)

Tencent Cloud RT-Cube Superplayer Adapter SDK 및 Android용 Demo는 [TXCPlayerAdapterSDK_Android](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_Android.zip)에서 다운로드할 수 있습니다. 

## 타겟 오디언스

본 문서의 일부 내용은 Tencent Cloud의 독점적 기능이므로, 사용하기 전에 [Tencent Cloud](https://intl.cloud.tencent.com) 관련 서비스를 활성화해 주십시오. 미등록 사용자는 [무료 베타](https://intl.cloud.tencent.com/login) 계정에 가입하실 수 있습니다.

## 통합 가이드[](id:guide)

SDK를 통합하고 TXCPlayerAdapter-release-1.0.0.aar를 libs 디렉터리에 복사하여 종속성을 추가합니다.

```groovy
implementation(name:'TXCPlayerAdapter-release-1.0.0', ext:'aar')
```

난독화를 위한 스크립트 추가:

```xml
-keep class com.tencent.** { *; }
```



### 플레이어 사용[](id:usePlayer)

변수를 선언한 다음 인스턴스를 만듭니다. 플레이어의 메인 클래스는 `ITXCPlayerAssistor`이며, 비디오 생성 후 재생할 수 있습니다.

FileId는 일반적으로 비디오가 업로드된 후 서버에서 반환됩니다.

1. 비디오가 클라이언트에 게시된 후 서버는 클라이언트에 fileId를 반환합니다.
2. 비디오가 서버에 업로드되면 업로드 확인 알림에 해당 fileId가 포함됩니다.


파일이 이미 Tencent Cloud에 있는 경우 [미디어 자산](https://console.cloud.tencent.com/vod/media)으로 이동하여 찾을 수 있습니다. 클릭 후 오른쪽의 비디오 세부 정보에서 관련 매개변수를 볼 수 있습니다.

```java
//psign은 Superplayer 서명입니다. 서명 및 생성 방법에 대한 자세한 내용은 다음 링크를 참고하십시오. https://intl.cloud.tencent.com/document/product/266/38099
private String mFileId, mPSign;
ITXCPlayerAssistor mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

초기화

```java
// 초기화
TXCPlayerAdapter.init(appId); //Tencent Cloud VOD에서 appid 신청 가능
TXCPlayerAdapter.setLogEnable(true); //log 활성화

mSuperPlayerView = findViewById(R.id.sv_videoplayer);  
mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

영상 정보 요청 및 영상 재생

```java
mPlayerAssistor.requestVideoInfo(new ITXCRequestVideoInfoCallback() {

    @Override
    public void onError(int errCode, String msg) {
        Log.d(TAG, "onError msg = " + msg);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Toast.makeText(VideoActivity.this, "onError msg = " + msg, Toast.LENGTH_SHORT).show();
            }
        });
    }

    @Override
    public void onSuccess() {
        Log.d(TAG, "onSuccess");
        TXCStreamingInfo streamingInfo = mPlayerAssistor.getStreamingInfo();
        Log.d(TAG, "streamingInfo = " + streamingInfo);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mPlayerAssistor.getStreamingInfo() != null) {
                  	//비디오 재생
                    mSuperPlayerView.play(mPlayerAssistor.getStreamingInfo().playUrl);
                } else {
                    Toast.makeText(VideoActivity.this, "streamInfo = null", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
});
```

사용 후 Player 폐기

```java
TXCPlayerAdapter.destroy();
```



## SDK API 목록[](id:sdkList)

#### TXCPlayerAdatper 초기화

**설명**

이 API는 매번 어댑터를 초기화하는 데 사용됩니다.

**API**

```java
TXCPlayerAdapter.init(String appId);
```

**매개변수 설명**

appId: appid 입력(서브 애플리케이션을 사용하는 경우 subappid 입력)



#### TXCPlayerAdatper 폐기

**설명**

이 API는 어댑터를 폐기하는 데 사용됩니다. 프로그램 종료 후 호출할 수 있습니다.

**API**

```java
TXCPlayerAdapter.destroy();
```



#### 플레이어의 보조 클래스 생성

**설명**

플레이어의 보조 클래스는 재생 fileId를 가져오고 DRM 암호화 API를 처리하는 데 사용할 수 있습니다.

**API**

```java
ITXCPlayerAssistor playerAssistor = TXCPlayerAdapter.createPlayerAssistor(String fileId, String pSign);
```

**매개변수 설명**

| 매개변수 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| fileId | String | 재생할 비디오의 fileId |
| pSign  | String | Superplayer 서명     |



**플레이어의 보조 클래스 종료**

**설명**

이 API는 보조 클래스를 종료하는 데 사용됩니다. 플레이어 종료 또는 다음 비디오 재생으로 전환 시 호출할 수 있습니다.

**API**

```
TXCPlayerAdapter.destroyPlayerAssistor(ITXCPlayerAssistor assistor);
```



#### 비디오 재생 정보 요청

**설명**

이 API는 Tencent Cloud VOD 서버에서 재생할 동영상의 스트림 정보를 요청하는 데 사용됩니다.

**API**

```java
playerAssistor.requestVideoInfo(ITXCRequestVideoInfoCallback callback);
```

**매개변수 설명**

| 매개변수   | 유형                         | 설명         |
| -------- | ---------------------------- | ------------ |
| callback | ITXCRequestVideoInfoCallback | 비동기 콜백 함수 |





#### 기본 비디오 정보 가져오기

**설명**

이 API는 비디오 정보를 가져오는 데 사용되며 playerAssistor.requestPlayInfo가 다시 호출된 후에만 적용됩니다.

**API**

```java
TXCVideoBasicInfo playerAssistor.getVideoBasicInfo();
```

**매개변수 설명**

TXCVideoBasicInfo의 매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 설명                 |
| ----------- | ------ | -------------------- |
| Name     | String   | 비디오 이름.                  |
| duration    | Float  | 비디오 지속 시간, 단위: 초. |
| description | String | 비디오 설명.           |
| coverUrl    | String | 비디오 커버.           |



#### 비디오 스트림 정보 가져오기

**설명**

이 API는 비디오 스트림 정보 목록을 가져오는 데 사용되며 playerAssistor.requestPlayInfo가 다시 호출된 후에만 적용됩니다.

**API**

```java
TXCStreamingInfo playerAssistor.getStreamimgInfo();
```

**매개변수 설명**

TXCStreamingInfo

| 매개변수     | 유형   | 설명                                       |
| ---------- | ------ | ------------------------------------------ |
| playUrl    | String | 재생 URL.                                 |
| subStreams | List   | SubStreamInfo 유형의 적응 비트 스트림 서브 스트림 정보. |

SubStreamInfo

| 매개변수         | 유형   | 설명                                   |
| -------------- | ------ | -------------------------------------- |
| type           | String | 서브 스트림 유형. 유효 값: video. |
| width          | Int    | 서브 스트림 비디오 너비(px).               |
| height         | Int    | 서브 스트림 비디오 높이(px).               |
| resolutionName | String | 플레이어에 표시되는 서브 스트림 비디오의 사양 이름. |



#### 키프레임 타임스탬프 정보 가져오기

**설명**

이 API는 비디오 키프레임 타임스탬프 정보를 가져오는 데 사용되며 playerAssistor.requestPlayInfo가 다시 호출된 후에만 적용됩니다.

**API**

```java
List<TXCKeyFrameDescInfo> playerAssistor.getKeyFrameDescInfo();
```

**매개변수 설명**

TXCKeyFrameDescInfo

| 매개변수     | 유형   | 설명          |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | ‘지금 시작...’ |



#### 썸네일 정보 가져오기

**설명**

이 API는 썸네일 정보를 가져오는 데 사용되며 playerAssistor.requestPlayInfo가 다시 호출된 후에만 적용됩니다.

**API**

```java
TXCImageSpriteInfo playerAssistor.getImageSpriteInfo();
```

**매개변수 설명**

TCXImageSpriteInfo

| 매개변수    | 유형   | 설명                                  |
| --------- | ------ | ------------------------------------- |
| imageUrls | List   | String 유형의 썸네일 다운로드 URL 배열. |
| webVttUrl | String | 썸네일 VTT 파일 다운로드 URL.            |

