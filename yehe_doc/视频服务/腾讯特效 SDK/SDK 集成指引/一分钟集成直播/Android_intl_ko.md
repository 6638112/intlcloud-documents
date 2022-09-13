[](id:step1)
## 1단계: Demo  프로젝트 압축 해제
1. Tencent Effect(TE) SDK와 통합된 [MLVB Demo](https://intl.cloud.tencent.com/document/product/1143/45374)를 다운로드합니다. 이 Demo는 Tencent Effect SDK S1-04 에디션을 기반으로 제작되었습니다.
2. Demo의 SDK 파일을 실제로 사용하는 SDK용 파일로 교체합니다. 구체적 작업은 다음 단계를 따르십시오.
   - xmagic 모듈의 libs 디렉터리에 있는 `.aar` 파일을 SDK의 libs에 있는 `.aar` 파일로 교체하십시오.
   - xmagic 모듈의 `../src/main/assets`에 있는 모든 파일을 SDK의 `assets/`에 있는 파일로 교체합니다. SDK 패키지의 MotionRes 폴더에 파일이 있는 경우 `../src/main/assets` 디렉터리에도 복사합니다.
   - xmagic 모듈의 `../src/main/jniLibs`에 있는 모든 .so 파일을 SDK 패키지의 jniLibs에 있는 .so 파일로 교체합니다(arm64-v8a 및 armeabi-v7a에 대한 `.so` 파일을 얻으려면 jinLibs 폴더에 있는 ZIP 파일의 압축을 풀어야 합니다).
3. Demo 프로젝트의 xmagic 모듈을 실제 항목 프로젝트로 가져옵니다.

[](id:step2)

## 2단계: app 모듈의 build.gradle 열기
1. applicationId를 신청된 테스트 인증과 일치하는 패키지 이름으로 수정합니다.
2. gson 종속성 설정을 추가합니다.
```groovy
configurations  {
all*.exclude  group:  'com.google.code.gson'
}
```

[](id:step3)

## 3단계: SDK 인터페이스 통합
Demo 프로젝트의 ThirdBeautyActivity 클래스를 참고하십시오.
1. **인증**:
```java
 //인증 시 주의사항 및 오류 코드 내용은 https://intl.cloud.tencent.com/document/product/1143/45385#step-1.-authenticate을 참고하십시오
XMagicImpl.checkAuth((errorCode, msg) -> {
            if (errorCode == TELicenseCheck.ERROR_OK) {
                showLoadResourceView();
            } else {
                TXCLog.e(TAG, "인증 실패, 인증 url 및 key를 확인하십시오" + errorCode + " " + msg);
            }
        });
```
2. **소재 초기화**:
```java
   private void showLoadResourceView() {
        if (XmagicLoadAssetsView.isCopyedRes) {
            XmagicResParser.parseRes(getApplicationContext());
            initXMagic();
        } else {
            XmagicLoadAssetsView loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **푸시 설정 실행**:
```java
String userId = String.valueOf(new Random().nextInt(10000));
String pushUrl = AddressUtils.generatePushUrl(streamId, userId, 0);
mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
mLivePusher.enableCustomVideoProcess(true, V2TXLivePixelFormatTexture2D, V2TXLiveBufferTypeTexture);
mLivePusher.setObserver(new V2TXLivePusherObserver() {
	@Override
	public void onGLContextCreated() {
	}

	@Override
	public int onProcessVideoFrame(V2TXLiveDef.V2TXLiveVideoFrame srcFrame, V2TXLiveDef.V2TXLiveVideoFrame dstFrame) {
		if (mXMagic != null) {
			dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
		}
		return srcFrame.texture.textureId;
		}

		@Override
		public void onGLContextDestroyed() {
		if (mXMagic != null) {
			mXMagic.onDestroy();
		}
	}
});
mLivePusher.setRenderView(mPushRenderView);
mLivePusher.startCamera(true);
int ret = mLivePusher.startPush(pushUrl);
mLivePusher.startMicrophone();
```
4. **textureId를 SDK에 불러오기 및 렌더링 처리**:
V2TXLivePusherObserver 인터페이스의`onProcessVideoFrame(V2TXLiveDef.V2TXLiveVideoFrame srcFrame, V2TXLiveDef.V2TXLiveVideoFrame dstFrame)` 메소드에 다음 코드를 추가합니다.
```java
if (mXMagic != null) {
	dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width,srcFrame.height);
}
return srcFrame.texture.textureId;
```
5. **SDK 일시 중지/폐기**:
`onPause()` 는 뷰티 필터 일시 중지에 사용되며, Activity/Fragment 라이프사이클 메소드에서 실행할 수 있습니다. onDestroy 메소드는 GL 스레드에서 호출해야 합니다. (onTextureDestroyed 메소드에서 XMagicImpl 객체의 `onDestroy()` 호출 가능) 자세한 사용법은 Demo를 참고하십시오.  
```java
mXMagic.onPause();   //일시 정지, Activity의 onPause 메소드와 연결
mXMagic.onDestroy();  //폐기, GL 스레드에서 호출
```
6. **레이아웃에 SDK 뷰티 필터 패널 추가**:
```xml
    <RelativeLayout
        android:id="@+id/livepusher_bp_beauty_pannel"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_above="@+id/ll_edit_info" />
```
7. **패널 초기화**:
```java
  private void initXMagic() {
          if (mXMagic == null) {
              mXMagic = new XMagicImpl(this, mBeautyPanelView);
          }else{
              mXMagic.onResume();
          }
      }
```

자세한 내용은 Demo 프로젝트의 `ThirdBeautyActivity.initXMagic();` 메소드를 참고하십시오.
