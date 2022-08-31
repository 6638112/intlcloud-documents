
## 작업 시나리오
데이터 일관성 검증 동안 DTS는 원본 데이터베이스와 대상 데이터베이스 간의 테이블 데이터를 비교하고 비교 결과와 불일치 세부 정보를 출력하여 일관성 없는 데이터를 빠르게 처리할 수 있도록 합니다. 데이터 일관성 검증 작업은 독립적이며 원본 데이터베이스 또는 기타 DTS 작업의 일반 비즈니스에 영향을 미치지 않습니다.

데이터 일관성 검증 작업은 해당 DTS 작업이 **증분 동기화** 단계에 있는 경우에만 생성할 수 있습니다.

>?현재 데이터 일관성 검사를 지원하는 연결은 다음과 같습니다.
>- MySQL/MariaDB/Percona/TDSQL MySQL > MySQL 
>- MySQL/MariaDB/Percona/TDSQL MySQL > MariaDB
>- MySQL/MariaDB/Percona  > TDSQL-C MySQL
>- MySQL/MariaDB/Percona/TDSQL MySQL  > TDSQL MySQL
>- MySQL/MariaDB/Percona/TDSQL TDStore  > TDSQL TDStore 

## 주의 사항
- 데이터 일관성은 원본 데이터베이스에서 대상 데이터베이스로 마이그레이션된 데이터만 비교합니다. 마이그레이션 중에 대상 데이터베이스에 데이터를 쓰는 경우 작성된 데이터는 일관성 검증에 포함되지 않습니다.
- 데이터 일관성 검증 작업은 원본 데이터베이스의 부하를 증가시킬 수 있습니다. 따라서 사용량이 적은 시간에 이러한 작업을 수행해야 합니다.
- 데이터 일관성 검증 작업은 반복적으로 실행할 수 있지만 하나의 DTS 인스턴스는 한 번에 하나의 작업만 시작할 수 있습니다.
- 검증할 테이블에는 기본 키 또는 고유 키가 있어야 합니다. 그렇지 않으면 확인하는 동안 DTS에서 건너뜁니다.
- 데이터 일관성 검증 작업이 완료되기 전에 DTS 작업 **완료** 또는 **종료**를 선택하면 확인 작업이 실패합니다.

## 제한
현재 검증 작업은 DDL 작업에서 감지할 수 없습니다. 마이그레이션 중에 원본 데이터베이스에서 DDL 작업을 수행하면 확인 결과가 실제 데이터와 일치하지 않으며 정확한 비교 결과를 얻으려면 다른 확인 작업을 시작해야 합니다.

## 데이터 일관성 검증 작업 생성
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인합니다.
2. **데이터 마이그레이션** 페이지에서 확인하려는 마이그레이션 작업을 선택하고 작업 ID를 클릭하여 **작업 세부 정보** 페이지로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0af144b0e8cb179934b28c2c45d567e2.png)
3. 탭을 전환하고 **데이터 일관성 검증**을 클릭합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/976fc2ce2f0374756b923134dda370d9.png" style="zoom:50%;" />

4. **데이터 일관성 검증 생성**을 클릭합니다.
>?데이터 일관성 검증 생성을 클릭합니다. 데이터 일관성 검증 작업은 해당 DTS 작업이 **증분 동기화** 단계에 있는 경우에만 생성할 수 있습니다. 버튼이 회색으로 표시되면 DTS 작업 상태가 요구 사항을 충족하지 않는 것입니다. 예를 들어 작업이 **증분 동기화** 단계에 들어가지 않았거나 실패했거나 종료되었습니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ee3616aae11c9f83adf25c902db03c09.png)
5. 팝업 창에서 **확인**을 클릭합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/b785c2ca36159ead67d9a72bc9c910e9.png" style="zoom:90%;" />

6. 데이터 일관성 검증 매개변수를 구성한 후 **데이터 비교 시작**을 클릭합니다.
마이그레이션 객체에 대해 **모든 마이그레이션 객체** 또는 **사용자 정의 선택**할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/33f22832c023c6e5c823482cba5ae8fe.png" style="zoom:90%;" />

## 데이터 일관성 검증 결과 조회
1. 마이그레이션 작업 홈페이지의 **마지막 검증 결과** 열에서 **더 보기**를 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/47b3914523ff745c3acd2d9852dd0a1b.png)
2. **조회**를 클릭하면 검증 결과를 볼 수 있습니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d29df913b865c78894eb626162540a2c.png)
    데이터가 일관되면 결과는 다음과 같습니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d3240dd21121889c53285e590fc32b13.png)

