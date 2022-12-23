
Tencent의 오디오/비디오 기술 및 첨단 인프라에 대한 다년간의 경험을 바탕으로 Tencent Cloud Video on Demand(VOD)는 오디오/비디오 캡처 업로드, 오디오/비디오 스토리지, 자동화 트랜스 코딩 처리, 재생 가속화, 미디어 자산 관리 및 고객과의 오디오/비디오 통신을 위한 원스톱 VPaaS(Video Platform as a Service) 솔루션을 제공합니다. VOD는 고품질 영상을 빠르고 유연하게 전달할 수 있는 안정적이고 안정적인 배포 기능을 통해, 고객이 비즈니스에 집중하고, 필요에 따라 서비스를 선택하며, 시장 변화에 민첩하게 대응할 수 있도록 합니다.


## 제품 아키텍처
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8fQI183_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16717824542449.png" width="750"><br><br>><br>
클라우드 비디오 스토리지(Cloud Video Storage), 비디오 트랜스코딩 서비스(Video Transcoding Service) 및 비디오 재생 가속(Video Playback Acceleration)은 Tencent Cloud 비디오 솔루션의 핵심 컴포넌트입니다.

- **클라우드 비디오 스토리지**
  VOD 콘솔 또는 SDK를 통해 비디오 콘텐츠를 업로드하거나 가져오고, VOD의 미디어 자산 관리 백그라운드에 미디어 파일을 저장하고, 콜드/핫 백업 스토리지, 미디어 자산 관리, 비디오 정보 검색과 같은 작업을 수행할 수 있습니다.
- **비디오 트랜스코딩 서비스**
  [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)에서는 획득한 소스 영상 데이터에 대해 부적절한 정보 인식 및 콘텐츠 인식을 수행할 수 있습니다. 트랜스 코딩, 화면 캡처, 워터마크 추가, 비디오 암호화, 비디오 썸네일 생성 등 작업도 진행할 수 있습니다.
- **비디오 재생 가속**
  VOD는 중국 전역의 수천 개의 CDN 가속 노드를 통해, 오디오/비디오 자원을 배포 및 관리하여 여러 채널에서 유연하고 부드러운 시청 경험을 제공합니다. 자체개발 또는 Tencent Cloud의 플레이어 SDK를 기존 비즈니스와 통합할 수 있습니다.
