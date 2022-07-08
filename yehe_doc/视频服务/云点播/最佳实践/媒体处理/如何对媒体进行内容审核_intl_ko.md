규정을 준수하지 않는 콘텐츠는 비즈니스를 법적 위험에 노출시키고 브랜드를 손상시킬 수 있습니다. VOD는 콘텐츠의 규정 준수를 보장하기 위해 [비디오 콘텐츠 심사](https://intl.cloud.tencent.com/document/product/266/33944) 및 [이미지 콘텐츠 심사](https://intl.cloud.tencent.com/document/product/266/33944) 기능을 제공합니다.

## 비디오 콘텐츠 심사 도입
VOD의 [비디오 콘텐츠 심사](https://intl.cloud.tencent.com/document/product/266/33944)는 귀하의 동영상 콘텐츠를 분석하여 콘텐츠 심사 결과를 제공합니다. 개발자는 결과에 따라 오디오/비디오 콘텐츠를 처리할 수 있습니다.

VOD [콘솔](https://intl.cloud.tencent.com/document/product/266/33897) 또는 [비디오 콘텐츠 심사](https://intl.cloud.tencent.com/document/product/266/33944)를 호출하여 비디오 조정 작업을 시작할 수 있습니다.

예를 들어 비디오 App이 VOD 오디오/ 비디오 감사 서비스에 액세스하는 경우 비디오 조정을 시작하기 위해 서버 측 API를 호출하는 프로세스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/99544692ba8d62874a0f718e805f2d57.png)

1. 동영상 App 백엔드는 콘텐츠 공급자를 인증하고 인증이 통과된 후 [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 배포합니다.
2. 콘텐츠 제공자는 공유할 콘텐츠를 VOD에 업로드합니다.
3. VOD는 업로드된 동영상의 FileId 및 재생 URL과 같은 [관련 정보](https://intl.cloud.tencent.com/document/product/266/33950)를 App 백엔드에 알립니다.
4. VOD는 업로드 서명을 생성하는 동안 ‘procedure’ 매개변수로 구성된 동영상 심사 작업을 실행합니다.
5. VOD는 [태스크 플로우 상태 변경](https://intl.cloud.tencent.com/document/product/266/33953) 알림을 통해 App 백엔드로 결과를 보냅니다.
 - 심사 결과가 ‘block’인 경우 콘텐츠가 비준수일 가능성이 높습니다. 콘텐츠를 차단하는 것이 좋습니다.
 - 심사 결과가 ‘pass’인 경우 콘텐츠가 비준수일 가능성이 낮습니다. 바로 통과시키는 것이 좋습니다.
 - 심사 결과가 ‘review’인 경우 수동 평가를 권장합니다.
6. App 백엔드는 ‘통과’ 태그가 지정된 동영상과 수동 검토를 통과한 ‘검토’ 태그 동영상을 게시합니다.
7. 콘텐츠 소비자는 App 백엔드에서 게시된 동영상의 재생 URL을 요청합니다.
8. 콘텐츠 소비자는 URL을 통해 VOD를 통해 동영상 재생을 가속화합니다.

4 - 6단계에서는 7단계에서 얻은 비디오가 규정을 준수하는지 확인합니다.

>! 여기에서 프로세스는 ‘게시 전 심사’ 접근 방식을 취합니다(즉, 심사를 통과한 동영상만 게시할 수 있습니다). 필요에 따라 ‘게시 후 심사’ 모드를 사용할 수도 있습니다(즉, 동영상이 성공적으로 업로드되면 즉시 게시되며 심사 후 부적절한 것으로 확인되면 제거됩니다).

