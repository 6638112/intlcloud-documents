## 작업 시나리오

Windows CVM에 파일 업로드 시 일반적으로 MSTSC 원격 데스크톱 연결(Microsoft Terminal Services Client) 방식을 사용합니다니다. 본 문서에서는 로컬 Windows 컴퓨터에서 원격 데스크톱 연결을 통해 Windows CVM에 파일을 업로드하는 방법을 안내합니다.

## 전제 조건

Windows CVM이 공용 네트워크에 액세스할 수 있어야 합니다.

## 작업 순서
>? 다음의 작업 순서는 Windows 7 운영 체제를 사용하는 로컬 컴퓨터를 예로 들어 설명합니다. 운영 체제에 따라 세부 작업 순서에 약간의 차이가 있습니다.
>
1. 로컬 컴퓨터에서 단축 키 [Windows + R]을 사용해 [실행] 창을 엽니다.
2. 팝업된 [실행] 창에서 **mstsc**를 입력한 후 [확인]을 클릭하여 [원격 데스크톱 연결] 대화 상자를 엽니다.
3. [원격 데스크톱 연결] 대화 상자에서 CVM 공인 IP를 입력한 후 [옵션]을 클릭합니다. 다음 그림 참조
![](//mc.qcloudimg.com/static/img/80ab67bbac77365528e1e4ebd8fbb023/image.png)
2. [일반] 탭에서 CVM의 공인 IP 주소와 사용자 이름 Administrator를 입력합니다. 다음 그림 참조
![](//mc.qcloudimg.com/static/img/b673c814747e0a3e8c934b5a84dfa89e/image.png)
3. [로컬 리소스] 탭을 선택한 후 [세부 정보]를 클릭합니다. 다음 그림 참조
![](//mccdn.qcloud.com/img56b1c57c38874.png)
4. 팝업된 [로컬 디바이스 및 리소스] 창에서 [드라이버] 모듈을 선택한 후 Windows CVM에 업로드할 파일이 있는 로컬 디스크를 선택한 다음 [확인]을 클릭합니다. 다음 그림 참조
![](//mccdn.qcloud.com/img56b1c582c8471.png)
5. 로컬 설정을 마친 후, [연결]을 클릭하여 Windows CVM에 원격 로그인합니다.
6. Windows CVM에서 [시작]>[컴퓨터]를 클릭한 후 다음과 같이 CVM에 마운트된 로컬 디스크를 확인합니다.
![](https://main.qcloudimg.com/raw/8e59dbca8d7cc7293669bf7adaf8985a.png)
9. 더블 클릭으로 로컬 디스크를 열고, 복사하려는 로컬 파일을 Windows CVM에 복사해 넣으면 파일 업로드가 완료됩니다. 
