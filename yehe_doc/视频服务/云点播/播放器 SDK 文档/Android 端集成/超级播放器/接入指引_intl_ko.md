## 제품 개요
Android용 Tencent Cloud RT-Cube Superplayer는 Tencent Cloud의 오픈 소스 플레이어 컴포넌트입니다. 품질 모니터링, 비디오 암호화, TESHD, 해상도 전환 및 작은 창 재생을 통합하며 모든 VOD 및 라이브 재생 시나리오에 적합합니다. 전체 기능을 캡슐화하고 상위 계층 UI를 제공하여 인기 있는 비디오 App과 유사한 재생 프로그램을 빠르게 구축할 수 있습니다.

## 버전 지원
본 문서에서 설명된 기능에 대한 Tencent Cloud RT-Cube 지원 현황은 다음과 같습니다.

| 버전 | Smart | Live | UGSV(User Generated Short Video) | TRTC(Tencent Real-Time Communication) | Player | 모든 기능 |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 지원 | -  | -  | -  | -  | &#10003;  | &#10003;                                                            |
| SDK 다운로드 | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=video) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=player) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |


## 준비 작업
1. 완전한 플레이어 기능을 사용하려면 [VOD](https://intl.cloud.tencent.com/product/vod)를 활성화하는 것이 좋습니다. 계정을 등록하지 않으셨다면 먼저 [회원 가입](https://intl.cloud.tencent.com/login) 하십시오. VOD 서비스를 사용하지 않는 경우 이 단계를 건너뛰십시오. 그러나 통합 후에는 기본 플레이어 기능만 사용할 수 있습니다.
2. [Android Studio 공식 웹 사이트](https://developer.android.com/studio)에서 Android Studio를 다운로드하고 설치합니다. 이미 수행한 경우 이 단계를 건너뜁니다.

## 내용 요약
1. Android용 Tencent Cloud RT-Cube Superplayer를 통합하는 방법
2. 플레이어 생성 및 사용 방법


## 통합 준비
### 1단계: 프로젝트 다운로드
Android용 Tencent Cloud RT-Cube Superplayer의 프로젝트 주소는 [SuperPlayer_Android](https://github.com/LiteAVSDK/Player_Android)입니다.

Android용 Tencent Cloud RT-Cube Superplayer는 **[플레이어 컴포넌트 ZIP 패키지 다운로드](#zip)** 또는 **[Git 명령 실행하여 다운로드](#git)**를 통해 다운로드할 수 있습니다.
<dx-tabs>
::: 플레이어 구성 요소 ZIP 패키지 다운로드[](id:zip)
**Code** > **Download ZIP**을 클릭하여 플레이어 컴포넌트 ZIP 패키지를 직접 다운로드할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Git 명령 실행[](id:git)
1. 먼저 컴퓨터에 Git이 설치되어 있는지 확인하십시오. 그렇지 않은 경우 [Git 설치 튜토리얼](https://git-scm.com/downloads)을 참고하여 설치할 수 있습니다.
2. 다음 명령을 실행하여 Superplayer 컴포넌트 프로젝트의 코드를 로컬 시스템에 clone합니다.
```shell
git clone git@github.com:tencentyun/SuperPlayer_Android.git
```
다음 정보가 표시되면 프로젝트 코드가 로컬 시스템에 성공적으로 clone된 것입니다.
```shell
‘SuperPlayer_Android’에 Cloning...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
객체 수신 중: 100% (2637/2637), 571.20 MiB | 3.94 MiB/s, 완료.
delta 처리 중: 100% (1019/1019), 완료.
```
프로젝트 다운로드 후, 소스 코드 압축 해제 후 생성되는 디렉터리는 다음과 같습니다.

| 파일 이름                      | 설명                                                         |
| --------------------------- | ------------------------------------------------------------ |
| LiteAVDemo(Player)          | Android Studio로 가져온 후 바로 실행할 수 있는 Superplayer Demo 프로젝트   |
| app                         | 메인 인터페이스 엔트리                                                   |
| superplayerkit              | 재생, 일시 중지 및 제스처 제어와 같은 일반적인 기능을 제공하는 Superplayer 컴포넌트(SuperPlayerView) |
| superplayerdemo             | Superplayer Demo 코드                                         |
| common                      | 툴 모듈                                                   |
| SDK                         | LiteAVSDK_Player_x.x.x.aar(aar 형식으로 제공되는 SDK) 및 LiteAVSDK_Player_x.x.x.zip(lib 및 jar 형식으로 제공되는 SDK)을 포함한 RT-Cube 플레이어 SDK |
| Player 문서(Android).pdf | Superplayer 사용자 가이드                                           |
:::
</dx-tabs>

### 2단계: 프로젝트 통합
이 단계에서는 플레이어를 통합하는 방법을 설명합니다. 자동 로드를 위해 Gradle을 사용하거나 aar을 수동으로 다운로드하여 현재 프로젝트로 가져오거나 jar 및 so 라이브러리를 가져와 프로젝트를 통합할 수 있습니다.
<dx-tabs>
::: Gradle(AAR)에서 자동 로드
1. SDK + Demo 개발 패키지를 다운로드합니다. 프로젝트 주소는 [Android](https://github.com/LiteAVSDK/Player_Android)입니다.
2. `Demo/superplayerkit` module을 프로젝트에 복사하고 다음과 같이 구성합니다.
   - `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
   ```xml
   include ':superplayerkit'
   ```
   - `superplayerkit` 프로젝트의 build.gradle 파일을 열고 compileSdkVersion, buildToolsVersion, minSdkVersion, targetSdkVersion 및 rootProject.ext.liteavSdk의 상수 값을 수정합니다.
     ![](https://main.qcloudimg.com/raw/fd6bc41bfd8b80fe5e82e3345b6ce73f.png)
   ```xmls
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies{
       //이전 버전을 통합하려면 latest.release를 8.5.290009와 같은 해당 버전 번호로 변경합니다.
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
위에서 설명한 대로 `common` 모듈을 프로젝트로 가져오고 구성합니다.
3. gradle에서 mavenCentral 라이브러리를 구성하면 LiteAVSDK를 자동으로 다운로드되고 업데이트됩니다. `app/build.gradle`을 열고 다음과 같이 구성합니다.
   ![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   
   1. dependencies에 LiteAVSDK_Player 종속성을 추가하십시오.
```xml
dependencies{
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
	 implementation project(':superplayerkit')
	 // Superplayer 댓글 자막 통합을 위한 3rd party 라이브러리
	 implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
}
```
   이전 버전의 LiteAVSDK_Player SDK를 통합해야 하는 경우 [MavenCentral](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player/)에서 확인한 다음 아래 내용에 따라 통합하십시오. 
```xml
dependencies{
	 // LiteAVSDK_Player SDK v8.5.10033 통합
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:8.5.10033'
}
```
   2.  `app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 필요에 따라 구성할 수 있는 armeabi, armeabi-v7a 및 arm64-v8a를 지원합니다).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
   SDK v9.4 이하의 다운로드 캐시 기능(TXVodDownloadManager의 API)을 사용하지 않았고 SDK v9.5 이상에서 다운로드한 파일을 재생할 필요가 없다면 설치 패키지의 크기를 줄이는 데 도움이 되는 기능의 so 파일을 사용합니다. 예를 들어 SDK v9.4 또는 이전 버전에서 TXVodDownloadManager 클래스의 setDownloadPath 및 startDownloadUrl 함수를 사용하여 캐시된 파일을 다운로드했고 TXVodDownloadManager에서 다시 호출한 getPlayPath 경로가 후속 재생을 위해 앱에 저장되어 있는 경우 다음이 필요합니다. libijkhlscache-master.so는 getPlayPath 경로에서 파일을 재생합니다. 그렇지 않으면 필요하지 않습니다. app/build.gradle에 다음을 추가할 수 있습니다.
```xml
packagingOptions {
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
   3. 프로젝트 디렉터리의 build.gradle에 mavenCentral 라이브러리를 추가합니다.
 ```
 repositories {
		 mavenCentral()
 }
 ```
4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) Sync Now를 클릭하여 SDK를 동기화합니다. mavenCentral에 연결할 수 있으면 SDK가 자동으로 다운로드되어 곧 프로젝트에 통합됩니다.
:::
::: Gradle(AAR)에서 수동 다운로드
1. SDK + Demo 개발 패키지를 다운로드합니다. 프로젝트 주소는 [Android](https://github.com/LiteAVSDK/Player_Android)입니다.
2. `SDK/LiteAVSDK_Player_XXX.aar`(XXX는 버전 번호)를 app 아래의 libs 폴더로 가져오고 `Demo/superplayerkit` module을 프로젝트에 복사합니다.
3. `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
```
include ':superplayerkit'
```
4. `superplayerkit` 프로젝트의 build.gradle 파일을 열고 compileSdkVersion, buildToolsVersion, minSdkVersion, targetSdkVersion 및 rootProject.ext.liteavSdk의 상수 값을 수정합니다.
![](https://main.qcloudimg.com/raw/479cb6ed7a29621998d1ee670e091437.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}

dependencies{
	 implementation(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
}
```
위에서 설명한 대로 `common` 모듈을 프로젝트로 가져오고 구성합니다.
   - repositories 구성
```xml
repositories {
	 flatDir {
			 dirs '../app/libs'
	 }
}
```
5. `app/build.gradle`에 종속성을 추가합니다.
```xml
compile(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
implementation project(':superplayerkit')
// Superplayer 댓글 자막 통합을 위한 3rd party 라이브러리
implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
```
6. 프로젝트 `build.gradle`에 다음을 추가합니다.
```xml
allprojects {
	 repositories {
			 flatDir {
					 dirs 'libs'
			 }
	 }
}
```
7. `app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
SDK v9.4 이하의 다운로드 캐시 기능(TXVodDownloadManager의 API)을 사용하지 않았고 SDK v9.5 이상에서 다운로드한 파일을 재생할 필요가 없다면 설치 패키지의 크기를 줄이는 데 도움이 되는 기능의 so 파일을 사용합니다. 예를 들어 SDK v9.4 또는 이전 버전에서 TXVodDownloadManager 클래스의 setDownloadPath 및 startDownloadUrl 함수를 사용하여 캐시된 파일을 다운로드했고 TXVodDownloadManager에서 다시 호출한 getPlayPath 경로가 후속 재생을 위해 앱에 저장되어 있는 경우 다음이 필요합니다. libijkhlscache-master.so는 getPlayPath 경로에서 파일을 재생합니다. 그렇지 않으면 필요하지 않습니다. app/build.gradle에 다음을 추가할 수 있습니다.
```xml
packagingOptions {
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
8. Sync Now를 클릭하여 SDK를 동기화합니다.
:::
::: SDK 통합(jar+so)
aar 라이브러리를 통합하지 않으려면 jar 및 so 라이브러리를 가져와서 LiteAVSDK를 통합하도록 선택할 수 있습니다.
[](id:smallStep_1)
1. 여기에서 [Android](https://github.com/LiteAVSDK/Player_Android)용 SDK + Demo 개발 키트를 다운로드하고 압축을 풉니다. SDK 디렉터리에서 SDK/LiteAVSDK_Player_XXX.zip(XXX는 버전 번호)을 찾습니다. 압축 해제 후 아래와 같이 jar 파일과 so 폴더가 포함된 libs 디렉터리를 얻을 수 있습니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/9ac0f5b1b9b5d15a005fa2226dd960b6.png)
2. `Demo/superplayerkit` module을 프로젝트에 복사하고 `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
```xml
include ':superplayerkit'
```
3. [1단계](#smallStep_1)에서 압축 해제하여 얻은 libs 폴더를 `superplayerkit` 프로젝트 루트 디렉터리에 복사합니다.
4. `superplayerkit/build.gradle` 파일을 수정합니다.
![](https://main.qcloudimg.com/raw/ed66e7d887bc5c28c2eff45807037c23.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}
```
위에서 설명한 대로 `common` 모듈을 프로젝트로 가져오고 구성합니다.
   - sourceSets를 구성하고 so 라이브러리 가져오기 코드를 추가합니다.
```xml
sourceSets{
		 main{
				 jniLibs.srcDirs = [’libs’]
		 }
 }
```
   - repositories를 구성하고 flatDir을 추가하고 로컬 리포지토리의 경로를 지정합니다.
```xml
repositories {
	 flatDir {
			 dirs 'libs'
	 }
}
```
5. ` app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
6. Sync Now를 클릭하여 SDK를 동기화합니다.
:::
</dx-tabs>
이 시점에서 Android용 Tencent Cloud RT-Cube Superplayer 통합을 완료했습니다.


### 3단계: App 권한 설정
AndroidManifest.xml에서 App 권한을 구성합니다. LiteAVSDK에는 다음 권한이 필요합니다.

```java
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD 플레이어 플로팅 창 권한-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--스토리지-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

### 4단계: 난독화 규칙 설정
proguard-rules.pro 파일에서 TRTC SDK 관련 사항을 비난독화 리스트에 추가합니다.
```xml
-keep class com.tencent.** { *; }
```
이제 Android용 Tencent Cloud RT-Cube Superplayer app에 대한 권한 구성을 완료했습니다.

### 5단계: 플레이어 기능 사용
이 단계에서는 플레이어를 만들고 비디오 재생에 사용하는 방법을 설명합니다.
1. **플레이어 생성**[](id:usePlayer)
플레이어의 메인 클래스는 `SuperPlayerView`이며, 동영상을 생성한 후 재생할 수 있습니다. FileID 또는 URL은 재생을 위해 통합될 수 있습니다. 레이아웃 파일에 SuperPlayerView 생성:
```xml
<!-- Superplayer-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```
2. **비디오 재생**[](id:playe)
이 단계에서는 비디오를 재생하는 방법을 설명합니다. Android용 Tencent Cloud RT-Cube Superplayer는 다음과 같이 VOD 및 라이브 재생에 사용할 수 있습니다.
	- VOD 재생: Superplayer는 [FileId](#fileid) 또는 [URL](#url)을 통한 두 가지 VOD 재생 방법을 지원합니다.
	- 라이브 재생: Superplayer는 라이브 재생을 위해 [URL을 통한 재생](#url) 방법을 사용할 수 있습니다. 라이브 오디오/비디오 스트림은 URL을 전달하기만 하면 재생을 위해 풀링할 수 있습니다. Tencent Cloud 라이브 스트리밍 URL 생성 방법에 대한 자세한 내용은 [라이브 방송 URL 직접 조합](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.
<dx-tabs>
::: URL을 통한 VOD 및 라이브 재생[](id:url)
URL은 VOD 파일의 재생 주소 또는 라이브 스트림의 풀 주소일 수 있습니다. 동영상 파일은 URL을 전달하기만 하면 재생할 수 있습니다.
```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073; // AppId 설정
model.url = "http://your_video_url.mp4";   // 재생할 동영상의 url 구성
mSuperPlayerView.playWithModel(model);
```
:::
::: FileID를 통한 VOD 재생[](id:fileid)
비디오 FileId는 일반적으로 비디오 업로드 후 서버에서 반환됩니다.
1. 클라이언트에서 비디오 배포 후 서버가 FileId를 클라이언트로 반환합니다.
2. 비디오가 서버에 업로드되면 해당 FileId가 업로드 확인 알림에 포함됩니다.

Tencent Cloud에 이미 파일이 존재하는 경우에는 [미디어 자산 관리](https://console.cloud.tencent.com/vod/media)에서 해당 파일을 찾아 FileId를 조회할 수 있습니다. 아래 이미지와 같이 ID는 FileId를 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)

>!
>- FileID를 통해 재생하려면 먼저 Adaptive-HLS(10) 트랜스 코딩 템플릿을 사용하여 비디오를 트랜스 코딩하거나 Superplayer 서명 psign을 사용하여 재생할 비디오를 지정해야 합니다. 그렇지 않으면 비디오가 재생되지 않을 수 있습니다. 비디오를 트랜스 코딩하는 방법에 대한 자세한 내용은 [Superplayer로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098)을 참고하십시오. psign을 생성하는 방법에 대한 자세한 내용은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오.
>- FileID를 통한 재생 중 ‘no v4 play info’ 예외가 발생하면 위와 같은 문제가 있을 수 있습니다. 이 경우 상기 지침에 따라 조정하는 것이 좋습니다. [URL](#url)을 통해 재생할 원본 비디오의 재생 링크를 직접 얻을 수도 있습니다.
>- **트랜스 코딩되지 않은 원본 비디오는 재생 중에 호환성 문제가 발생할 수 있으므로 재생을 위해 비디오를 트랜스 코딩하는 것이 좋습니다.**
<dx-codeblock>
:::  java
//링크 도용 방지가 비활성화된 재생 중에 ‘no v4 play info’ 예외가 발생하면 Adaptive-HLS(10) 트랜스 코딩 템플릿을 사용하여 비디오를 트랜스 코딩하거나 URL을 통해 재생할 원본 비디오의 재생 링크를 직접 가져오는 것이 좋습니다.

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppId 설정
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileId 설정
//비공개 암호화 재생을 위해서는 Superplayer의 서명인 psign을 입력해야 합니다. 서명 및 생성 방법에 관한 내용은 다음 링크를 참고하십시오. https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
</dx-tabs>
3. **재생 종료**[](id:exitPlayer)
플레이어가 필요하지 않은 경우 `resetPlayer`을 호출하여 플레이어 내부를 정리하고 메모리를 확보합니다.
```java
mSuperPlayerView.resetPlayer();
```

이제 Android용 Tencent Cloud RT-Cube Superplayer의 플레이어 생성, 비디오 재생 및 재생 종료 기능을 통합했습니다.


[](id:moreFeature)
## 기능 사용[](id:moreFeature)

이 섹션에서는 몇 가지 일반적인 플레이어 기능에 대해 설명합니다. 더 많은 기능은 [Demo](#demo)를 참고하십시오.

### 1. 전체 화면 재생

Superplayer는 전체 화면 재생을 지원하며 제스처, 댓글 자막, 화면 캡처 및 해상도 전환을 통해 화면 잠금, 볼륨 및 밝기 제어를 설정할 수 있습니다. 이 기능은 **[Tencent Cloud RT-Cube App](#qrcode) > 플레이어 > Superplayer**에서 체험해볼 수 있으며, 전체 화면 아이콘을 탭하면 전체 화면 재생 모드로 이동할 수 있습니다.

창 재생 모드에서 다음 API를 호출하여 전체 화면 재생 모드로 들어갈 수 있습니다.

```java
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.FULLSCREEN);
```


<dx-tabs>
::: 창으로 돌아가기
**Back**을 탭하여 창 재생 모드로 돌아갑니다.

```java
//탭 후 트리거되는 API
mControllerCallback.onBackPressed(SuperPlayerDef.PlayerMode.FULLSCREEN);
onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```
:::
::: 화면 잠금[](id:lockscreen)
화면 잠금 작동은 몰입형 재생 상태를 가능하게 합니다.
```java
//탭 후 실행되는 API
toggleLockState();
```
:::
::: 댓글 자막[](id:barrage)
댓글 자막 기능이 활성화되면 사용자가 보낸 텍스트 댓글이 화면에 표시됩니다.
```java
// 1단계: 댓글 자막 View에 댓글 자막 추가
addDanmaku(String content, boolean withBorder);
// 2단계: 댓글 자막 활성화 또는 비활성화
toggleBarrage();
```
:::
::: 화면 캡처[](id:screenshot)
Superplayer는 재생 중 현재 비디오 프레임을 캡처하는 기능을 제공하며 공유를 위해 스크린샷을 저장할 수 있습니다. 이미지 4의 버튼을 탭하여 화면을 캡처하고 캡처한 스크린샷을 mSuperPlayer.snapshot API에 저장할 수 있습니다.
```java
mSuperPlayer.snapshot(new TXLivePlayer.ITXSnapshotListener() {
  @Override
  public void onSnapshot(Bitmap bitmap) {
        //캡처한 스크린샷을 여기에 저장할 수 있습니다.
  }
});
```
:::
::: 해상도 전환[](id:resolution)
HD, SD 및 FHD와 같은 다양한 비디오 재생 해상도를 필요에 따라 선택할 수 있습니다.
```java
//탭 후 트리거된 해상도 view를 표시하기 위한 API
showQualityView();
//해상도 옵션을 탭하기 위한 콜백 API는 다음과 같습니다.
mListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
  @Override
  public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
    // 해상도 ListView 탭 이벤트
    VideoQuality quality = mList.get(position);
    mCallback.onQualitySelect(quality);
  }
});
//최종적으로 선택된 해상도에 대한 콜백
@Override
public void onQualityChange(VideoQuality quality) {
   mFullScreenPlayer.updateVideoQuality(quality);
   mSuperPlayer.switchStream(quality);
}
```
:::
</dx-tabs>


### 2. 플로팅 창 재생
Superplayer는 사용자가 비디오 재생을 중단하지 않고 다른 앱으로 전환할 수 있도록 하는 작은 플로팅 창에서 재생을 지원합니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **플레이어** > **Superplayer**에서 왼쪽 상단 모서리에 있는 **Back**을 탭하여 사용해 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:25%;" />
플로팅 창 재생은 AndroidManifest의 다음 권한에 의존합니다.

```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```
```java
// 플로팅 창으로 전환하여 트리거되는 API
mSuperPlayerView.switchPlayMode(SuperPlayerDef.PlayerMode.FLOAT);
//메인 창으로 돌아가기 위해 플로팅 창을 탭하여 트리거되는 API
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```

### 3. 비디오 썸네일

Superplayer는 첫 번째 비디오 프레임을 재생 콜백 수신 이전에 표시할 비디오 썸네일의 사용자 정의를 지원합니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode)> **플레이어** > **Superplayer** > **썸네일 사용자 정의 데모**에서 사용해 볼 수 있습니다.



* Superplayer가 자동 재생 모드 `PLAY_ACTION_AUTO_PLAY`로 설정되면 비디오가 자동으로 재생되고 첫 번째 비디오 프레임이 로딩되기 전에 미리보기 이미지가 표시됩니다.
* Superplayer가 수동 재생 모드 `PLAY_ACTION_MANUAL_PLAY`로 설정된 경우 사용자가 **재생**을 탭한 후에만 비디오 재생이 시작됩니다. 썸네일은 첫 번째 비디오 프레임이 로딩될 때까지 표시됩니다.

비디오 썸네일은 아래 지침에 따라 URL 또는 로컬 File 주소 사용을 지원합니다. FileID를 통해 비디오를 재생하면 VOD에서 비디오 썸네일을 직접 구성할 수 있습니다.

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = "귀하의 appid";
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "귀하의 fileId"; 
//자동 PLAY_ACTION_AUTO_PLAY 또는 수동 PLAY_ACTION_MANUAL_PLAY로 설정할 수 있는 재생 모드
model.playAction = PLAY_ACTION_MANUAL_PLAY;
//썸네일 url을 설정합니다. coverPictureUrl이 설정되지 않은 경우 VOD 콘솔에서 구성한 썸네일이 자동으로 사용됩니다.
model.coverPictureUrl = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png" 
mSuperPlayerView.playWithModel(model);
```

### 4. 비디오 목록 루프

Superplayer는 비디오 목록 루프를 지원합니다. 즉, 비디오 목록이 제공된 후:

* 목록에 있는 비디오는 반복 재생될 수 있습니다. 다음 비디오는 자동으로 재생되거나 재생 중에 수동으로 전환될 수 있습니다.
* 목록의 마지막 비디오가 끝난 후 목록의 첫 번째 비디오가 자동으로 시작됩니다.

이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **플레이어** > **Superplayer** > **비디오 목록 루프 데모**에서 사용해 볼 수 있습니다.



```java
//1단계: 루프 List 생성<SuperPlayerModel>
ArrayList<SuperPlayerModel> list = new ArrayList<>();
SuperPlayerModel model = new VideoModel();
model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071568"；
list.add(model);

model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071679"；
list.add(model);
//2단계: 루프 API 호출
mSuperPlayerView.playWithModelList(list, true, 0);
```

```java
public void playWithModelList(List<SuperPlayerModel> models, boolean isLoopPlayList, int index);
```

API 매개변수 설명

| 매개변수         | 유형                   | 설명                           |
| -------------- | ---------------------- | ------------------------------ |
| models         | List<SuperPlayerModel> | 루프 데이터 목록                   |
| isLoopPlayList | boolean                | 루프 여부                       |
| index          | int                    | 재생을 시작할 SuperPlayerModel의 인덱스 |

### 5. 비디오 미리보기

Superplayer는 비VIP 회원 미리보기에 적합한 비디오 미리보기 기능을 지원합니다. 비디오 미리보기 지속 시간, 프롬프트 메시지 및 미리보기 최종 화면을 제어하기 위해 다른 매개변수를 전달할 수 있습니다. 이 기능은 [**Tencent Cloud RT-Cube App**](#qrcode) > **플레이어** > **Superplayer** > **미리보기 기능 데모**에서 사용해 볼 수 있습니다.

```java
 방법1:
 //1단계: 비디오 mode 생성
 SuperPlayerModel mode = new SuperPlayerModel();
 //...비디오 소스 정보 추가
 //2단계: 미리보기 정보 mode 생성
 VipWatchModel vipWatchModel = new VipWatchModel("%ss을(를) 미리 보고 VIP 멤버십을 활성화하여 전체 비디오를 볼 수 있습니다",15);
 mode.vipWatchMode = vipWatchModel;
 //3단계: 동영상 재생 메소드 호출
 mSuperPlayerView.playWithModel(mode);

 방법2:
 //1단계: 미리보기 정보 mode 생성
 VipWatchModel vipWatchModel = new VipWatchModel("%ss을(를) 미리 보고 VIP 멤버십을 활성화하여 전체 비디오를 볼 수 있습니다",15);
  //Step 2: 미리보기 기능 설정 메소드 호출
 mSuperPlayerView.setVipWatchModel(vipWatchModel);
```

```java
public VipWatchModel(String tipStr, long canWatchTime)
```

VipWatchModel API 매개변수 설명:

| 매개변수          | 유형     | 설명        |
| ------------ | ------ | --------- |
| tipStr       | String | 프롬프트 메시지 미리보기    |
| canWatchTime | Long   | 초 단위의 미리보기 지속 시간 |

### 6. 동적 워터마크

Superplayer를 사용하면 무단 녹음을 방지하기 위해 재생 화면에 불규칙하게 움직이는 텍스트 워터마크를 추가할 수 있습니다. 워터마크는 전체 화면 재생 모드와 창 재생 모드에서 모두 표시할 수 있습니다. 워터마크 텍스트, 크기 및 색상을 수정할 수 있습니다. 이 기능은 [**Tencent Cloud RT-Cube App** ](#qrcode)> **플레이어** > **Superplayer** > **동적 워터마크** 데모에서 사용해 볼 수 있습니다.



```java
 방법1:
 //1단계: 비디오 mode 생성
 SuperPlayerModel mode = new SuperPlayerModel();
 //...비디오 소스 정보 추가
 //2단계: 워터마크 정보 mode 생성
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
 mode.dynamicWaterConfig = dynamicWaterConfig;
 //3단계: 동영상 재생 메소드 호출
 mSuperPlayerView.playWithModel(mode);

 방법2:
 //1단계: 워터마크 정보 mode 생성
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
  //2단계: 동적 워터마크 기능 설정 메소드 호출
 mSuperPlayerView.setDynamicWatermarkConfig(dynamicWaterConfig);
```

```java
public DynamicWaterConfig(String dynamicWatermarkTip, int tipTextSize, int tipTextColor)
```

API 매개변수 설명

| 매개변수                 | 유형     | 설명     |
| ------------------- | ------ | ------ |
| dynamicWatermarkTip | String | 워터마크 텍스트 정보 |
| tipTextSize         | int    | 텍스트 크기   |
| tipTextColor        | int    | 텍스트 색상   |

[](id:demo)
## Demo 체험

더 많은 기능을 사용하려면 프로젝트 Demo를 직접 실행하거나 QR 코드를 스캔하여 Tencent Cloud RT-Cube App Demo를 다운로드할 수 있습니다.

### 프로젝트 Demo 실행

1. Android Studio의 탐색 모음에서 **File** > **Open**을 선택합니다. 팝업 창에서 **Demo** 프로젝트의 `$SuperPlayer_Android/Demo` 디렉터리를 선택합니다. Demo 프로젝트를 성공적으로 가져온 후 **Run app**을 클릭하여 Demo를 실행합니다.
2. 아래와 같이 Demo를 성공적으로 실행한 후 **플레이어** > **Superplayer**로 이동하여 플레이어 기능을 사용해 보십시오.

[](id:qrcode)
### Tencent Cloud RT-Cube App
**Tencent Cloud RT-Cube App** > **플레이어**에서 Superplayer의 더 많은 기능을 사용해 볼 수 있습니다.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
